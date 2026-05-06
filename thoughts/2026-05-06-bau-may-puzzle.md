---
layout: single
title: "Bau Lab May Mech Interp Puzzle"
date: 2026-05-06
categories: thoughts
toc: true
classes: no-left-sidebar
author_profile: false
toc_sticky: true
permalink: /thoughts/bau-may-puzzle/
---

In this post I analyze the puzzle from [puzzles.baulab.info](https://puzzles.baulab.info) — reverse-engineering a 9,600 parameter attention-only transformer trained to count unique tokens. See [this Colab notebook](https://colab.research.google.com/drive/1vKbwqBBDfj5DFW8ELp6zqCJf_KtWM2ME?usp=sharing) for the corresponding code.

## Task

Given a sequence of 10 tokens drawn from a vocabulary of 10 symbols, predict the number of distinct symbols. The released model hits 100% accuracy on every count from 1 through 10 on a held-out test set. Reverse-engineer the algorithm it learned.

| | |
|---|---|
| **Input symbols** | 10 (rendered as `a` – `j`) |
| **Sequence length** | 10 input tokens |
| **Layers** | 2 |
| **Heads per layer** | 4 |
| **`d_model`** | 32 |
| **Parameters** | 9,600 |
| **Vocab** | 22 tokens (10 input symbols + `BOS` + `ANS` + 10 count tokens `#1`–`#10`) |
| **Positional embeddings** | none |
| **Causal mask** | yes |

Attention-only: no MLPs, no LayerNorm, no positional embeddings.

```
token_embedding
    → attention layer 1 (4 heads, causal mask) + residual
    → attention layer 2 (4 heads, causal mask) + residual
    → linear unembed → logits
```

---

# Submission
The model partitions the 10-symbol vocabulary into four groups, each handled by a dedicated mechanism:

| Token group | Handled by | Mechanism |
|-------------|-----------|-----------|
| `b` | L1 head 0 | Self-attends in L0 → distinctive residual → detected directly |
| `f` | L1 head 1 | Mostly self-attends in L0 → invisible to anchor circuit → detected directly |
| `a, h, d, g` | L1 head 2 | L0 heads write anchor OVs into subsequent positions → fingerprint read at last position |
| `c, e, i, j` | L1 head 3 | L0 heads write ceij tokens to ANS → destructive interference with query → BOS attenuation |

The four L1 heads contribute independently and additively to the final count logits. Below, we provide proof that the algorithm is split into these four groups, then explain each group's mechanism in detail.

## The Four-Way Partition

Each Layer 1 head is causally necessary for exactly its token group — performing mean ablation drops accuracy to 0% when those tokens are present, but leaves accuracy at 100% when they are absent. Furthermore, the prediction drops by approximately the number of unique tokens in that group.

![](/thoughts/images/result0.png)

## Mechanism 1: Counting `b`

`b` has strongly negative key scores in all four Layer 0 heads, causing it to always self-attend rather than accumulate information from other tokens. This gives `b` a uniquely large and distinctive residual after Layer 0. Layer 1 head 0 then attends directly to `b` if present (else falls back to BOS), and the difference in value outputs between these two cases produces a clean +1 rightward shift in the count logits.

**Key results:**
- `b` attends only to itself or BOS in Layer 0 (1.000), other tokens never attend to `b` (0.000)  
- L1 head 0 attends to `b` if present, else BOS (1.000 both ways)
- OV(`b`) − OV(BOS) is consistently rightward, encoding +1 to the count

![](/thoughts/images/result1.png)

## Mechanism 2: Counting `f`

`f` mostly self-attends in Layer 0 (62% self-attention) but unlike `b` it also reads some anchor content. Crucially however, `f` has strongly negative key scores in Layer 1 head 2, so it is still invisible to the anchor counting circuit (0.000 attention from head 2). Layer 1 head 1 detects `f` directly: it attends to `f` if present, else falls back to `{g,d,h}`, and the difference in value outputs encodes +1 to the count.

**Key results:**
- `f` mostly self-attends in Layer 0 (62%)
- L1 head 2 never attends to `f` (0.000) — `f` is invisible to the anchor circuit
- L1 head 1 attends to `f` if present, else g/d/h — proven 1.000 in both cases
- OV(`f`) − OV(g/d/h) projects rightward, encoding exactly +1

![](/thoughts/images/result2.png)

## Mechanism 3: Counting `a`, `h`, `d`, `g`

Each Layer 0 head is dedicated to one anchor token (head 0→`a`, head 1→`h`, head 2→`d`, head 3→`g`). When an anchor is present, every subsequent non-b/f/ANS token attends to it with probability 1.000, causing the anchor's OV vector to be written into all subsequent residuals. This creates an accumulated fingerprint encoding which anchors appeared. Layer 1 head 2 is biased toward later positions (which have richer fingerprints via higher key scores), and its value circuit produces a rightward logit shift proportional to how many unique anchors were present.

**Key results:**
- Every non-b/f token after an anchor attends to it: 1.000 for all four heads
- Forcing L1 head 2 to attend to last non-b/f position gives 1.000 accuracy; first position gives 0.002 — the last position always contains the full fingerprint
- Head 2 logit contribution scales with anchor count (0→4 anchors produces monotonically increasing rightward shift)

![](/thoughts/images/result3.png)

## Mechanism 4: Counting `c`, `e`, `i`, `j`

Each Layer 0 head writes one designated secondary token to the ANS position (head 0→`i`, head 1→`j`, head 2→`c`, head 3→`e`). These OV vectors accumulate in the ANS residual, which becomes the query for all Layer 1 heads. Each ceij token's OV contribution points approximately opposite to the baseline ANS query (~0.98 cosine similarity with −q_base), causing destructive interference that progressively cancels the query magnitude. This reduces ANS's attention to BOS in Layer 1 head 3. Since BOS provides a strong low-count baseline signal, attenuating it raises the predicted count by approximately +1 per unique ceij token present.

**Key results:**
- Each L0 head writes one ceij token to ANS: head 0→`i`, head 1→`j`, head 2→`c`, head 3→`e` — forcing this assignment gives 1.000 accuracy
- Each ceij token's query shift is ~0.98 anti-parallel to the baseline query (destructive interference)
- q·k_BOS drops monotonically with ceij count: 19.2 → 11.6 → 8.9 → 6.3 → 3.6
- BOS logit contribution shrinks with each additional ceij token, reducing the low-count bias

![](/thoughts/images/result4.png)

# Final Summary

This model solves unique token counting through a clean four-way partition of the vocabulary, with each subset handled by a dedicated Layer 1 head using information prepared by Layer 0.

The key insight is that Layer 0 serves a different role for each group:
- **b, f**: isolated from the rest of the circuit by self-attention, leaving distinctive residuals for direct detection
- **a, h, d, g**: each head propagates its anchor's presence forward through the sequence via OV writes, accumulating a fingerprint at later positions
- **c, e, i, j**: each head writes its designated secondary token into the ANS residual, which then alters the query for Layer 1

Layer 1 then reads off these signals independently:
- **Head 0, 1**: binary detectors for b and f, contributing exactly +1 when present
- **Head 2**: reads the anchor fingerprint from the last non-b/f position, contributing +1 per unique anchor
- **Head 3**: its baseline query points toward BOS (low-count bias); each ceij token destructively interferes with this query, attenuating BOS attention and contributing +1 per unique ceij token

The four contributions combine additively to produce the correct total count, achieving 100% accuracy across all counts 1–10. The solution exhibits perfect coverage with zero redundancy — every token in the vocabulary is accounted for by exactly one mechanism.

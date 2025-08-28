---
layout: single
permalink: /cbdebug/
hide_masthead: true
---
<p align="center">
  <img src="/assets/image/cbdebug/CBDebugLogo.png" alt="CBDebug Logo" width="500"/>
</p>

<div align="center">
    <h1>Debugging Concept Bottleneck Models through Removal and Retraining</h1>
    <h3><a href="https://ericenouen.github.io/">Eric Enouen</a>, <a href="https://sainyamgalhotra.com/">Sainyam Galhotra</a></h3>
    <h4>Cornell University</h4>
</div>


<!--{% include button.html href="[Link to your paper's PDF]" text="Paper" style="info" icon="fas fa-file-alt" %}-->

<!--{% include button.html url="https://github.com/ericenouen/interpdebug" label="Code" class="default" icon="fas fa-code" %}-->

<!--{% include button.html href="[Link to a demo or examples page]" text="Examples" style="default" icon="fas fa-images" %}-->

## **Abstract**

Concept Bottleneck Models (CBMs) use a set of human-interpretable concepts to predict the final task label, enabling domain experts to not only validate the CBM's predictions, but also intervene on incorrect concepts at test time. However, these interventions fail to address systemic misalignment between the CBM and the expert's reasoning, such as when the model learns shortcuts from biased data. To address this, we present a general interpretable debugging framework for CBMs that follows a two-step process of *Removal* and *Retraining*. In the *Removal* step, experts use concept explanations to identify and remove any undesired concepts. In the *Retraining* step, we introduce `CBDebug`, a novel method that leverages the interpretability of CBMs as a bridge for converting concept-level user feedback into sample-level auxiliary labels. These labels are then used to apply supervised bias mitigation and targeted augmentation, reducing the model’s reliance on undesired concepts. We evaluate our framework with both real and automated expert feedback, and find that `CBDebug` significantly outperforms prior retraining methods across multiple CBM architectures (PIP-Net, Post-hoc CBM) and benchmarks with known spurious correlations (Waterbirds, MetaShift, CelebA).

---

## **Concept Bottleneck Debugging Framework**
<p align="center">
  <img src="/assets/image/cbdebug/CBDebugRemovalRetrain.png" alt="Removal Retrain Figure" width="800"/>
</p>

Our debugging framework incorporates a domain expert’s knowledge into a concept bottleneck. 

**Removal:** The user inspects concept explanations and selects undesired concepts to remove, such as background concepts in bird classification. 

**Retraining:** The concept extractor and inference layer are retrained based on this feedback, updating the CBM to remove dependence on undesired concepts while maintaining reliance on task-relevant concepts.

---

## **CBDebug**

<p align="center">
  <img src="/assets/image/cbdebug/CBDebugMethod.png" alt="CBDebug Main Figure" width="800"/>
</p>

Overview of `CBDebug` (Concept Bottleneck Debugger), which consists of three main steps. First, the encoder \( \phi \) computes the concept activations for undesired concepts in \( \texttt{spurious} \) to generate the approximated auxiliary label \( \hat{\mathbf{V}} \). Second, permutation weighting utilizes \( \hat{\mathbf{V}} \) and the class label \( \mathbf{Y} \) to compute the odds of the sample being drawn from the unconfounded distribution, generating weights \( \mathbf{U} \). Third, augmentation is performed on \( \mathbf{X} \) based on the undesired concepts \( \texttt{spurious} \) and weights \( \mathbf{U} \) to generate \( \mathbf{X}_{\text{aug}} \). Finally, we retrain \( \{\phi, h\} \) on \( (\mathbf{X}_{\text{aug}}, \mathbf{Y}) \) weighted by \( \mathbf{U} \) and return \( \{\phi', h'\} \).

---

## **Experiments**

We show improved worst-group accuracy across popular subpopulation shift datasets, with both real and automated feedback.

With our data balancing scheme, we can effectively retrain the model based on user feedback to remove reliance on spurious correlations and replace those with more robust concepts for the classification task.

<p align="center">
  <img src="/assets/image/cbdebug/CBDebugResults.png" alt="cbdebug_results" width="600"/>
</p>

---

## **Conclusion**
- We present an interpretable debugging framework for CBMs, extending prior frameworks to a more general architecture and enabling domain experts to globally edit model reasoning.
- We introduce `CBDebug`, a retraining approach that first approximates sample-level auxiliary labels from concept-level feedback, then reweights and augments the dataset to reduce reliance on undesired concepts and better align the model with expert reasoning.
- We validate our framework across multiple CBMs (PIP-Net, Post-hoc CBM) and datasets with known spurious correlations (Waterbirds, Metashift, CelebA). `CBDebug` most effectively leverages user feedback on spurious concepts, outperforming prior work on ProtoPNets and improving worst-group accuracy by up to 26% over the original model, with strong results even when feedback is automated with an LLM.

---

## **Cite this Work**
```bibtex
@inproceedings{enouendebugging,
  title={Debugging Concept Bottlenecks through Intervention: Shortcut Removal and Retraining},
  author={Enouen, Eric and Galhotra, Sainyam},
  booktitle={Workshop on Spurious Correlation and Shortcut Learning: Foundations and Solutions}
}
```

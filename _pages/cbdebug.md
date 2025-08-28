---
name: true
title: false
layout: default
permalink: /cbdebug/
hide_header: true
---
<p align="center">
  <img src="https://github.com/user-attachments/assets/45a11903-3fd5-49fd-8ce5-775dfe298102" alt="CBDebug Logo" width="500"/>
</p>

<div align="center">
    <h1>Debugging Concept Bottleneck Models through Removal and Retraining</h1>
    <h3><a href="https://ericenouen.github.io/">Eric Enouen</a>, <a href="https://sainyamgalhotra.com/">Sainyam Galhotra</a></h3>
    <h4>Cornell University</h4>
</div>


{% include button.html href="[Link to your paper's PDF]" text="Paper" style="info" icon="fas fa-file-alt" %}

{% include button.html href="[Link to your code on GitHub]" text="Code" style="default" icon="fas fa-code" %}

{% include button.html href="[Link to a demo or examples page]" text="Examples" style="default" icon="fas fa-images" %}

## **Abstract**

[A short, one-paragraph abstract that explains the problem, your proposed solution (using your CBM), and the main results. This is often the same as the paper's abstract.]

---

## **Concept Bottleneck Debugging Framework**

---

## **CBDebug**

<p align="center">
  <img src="assets/CBDebug.png" alt="CBDebug Main Figure" width="800"/>
</p>

**CBDebug (Concept Bottleneck Debugger)** is a framework for debugging concept bottleneck models using human feedback. A domain expert first identifies and removes spurious concepts learned by the model, then CBDebug retrains the model based on this feedback using a reweighting and augmentation scheme to force the model to rely on more robust, meaningful concepts.

With our data balancing scheme, we can effectively retrain the model based on user feedback to remove reliance on spurious correlations and replace those with more robust concepts for the classification task.

<p align="center">
  <img src="https://github.com/user-attachments/assets/025e449a-490d-4000-af02-8c22c211a3d9" alt="cbdebug_results" width="600"/>
</p>

---

---

## **Experiments**

---

## **Conclusion**

---

## **Cite this Work**
```bibtex
@inproceedings{enouendebugging,
  title={Debugging Concept Bottlenecks through Intervention: Shortcut Removal and Retraining},
  author={Enouen, Eric and Galhotra, Sainyam},
  booktitle={Workshop on Spurious Correlation and Shortcut Learning: Foundations and Solutions}
}
```

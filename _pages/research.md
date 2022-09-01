---
layout: home
title: "Research Projects"
author_profile: true
permalink: /research/
---

#### A Predictor-Corrector Method for fair Graph Spam Detection
June 2021 - May 2022

My first research opportunity was through an REU at Lehigh University under the supervision of Sihong Xie. I worked on a multi-objective optimization method for fair graphical models, that balanced performance metric(s) simultaneously with fairness metric(s) to find the tradeoff curve of solutions, called the pareto front.

![Pareto front](https://github.com/ericenouen/ericenouen.github.io/blob/master/assets/image/ParetoFront.png?raw=true =100x100)

Specifically, we used the predictor-corrector method described in this work: [Efficient Continuous Pareto Exploration in Multi-Task Learning](https://arxiv.org/abs/2006.16434) to more efficiently explore the pareto front.

The goal of the project was to create a better pareto front, a tradeoff curve between objectives, for any fairness vs. accuracy problem. We utilized a predictor corrector method to increase the algorithm's speed for finding points on this pareto front, and worked on using krylov recycling to save subspace information between each step to generate a pareto front even faster.

Preprint not yet available.

#### Data-free Model Extraction
June 2022 - August 2022

Next, I got the chance to work under Lin Tan at Purdue University through another REU.

Model extraction is the process of stealing the performance of a black-box model, and our goal was to improve the query efficiency of these algorithms.

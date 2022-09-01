---
layout: home
title: "Research Projects"
author_profile: true
permalink: /research/
---

#### Data-free Model Extraction
June 2022 - August 2022

Next, I got the chance to work under Lin Tan at Purdue University through another REU.

Model extraction is the process of stealing the performance of a black-box model, and our goal was to improve the query efficiency of these algorithms.


#### A Predictor-Corrector Method for fair Graph Spam Detection
June 2021 - May 2022

My first research opportunity was through an REU at Lehigh University under the supervision of Sihong Xie. I worked on a multi-objective optimization method for fair graphical models, that balanced performance metric(s) simultaneously with fairness metric(s) to find the tradeoff curve of solutions, called the pareto front.

![Pareto front](https://github.com/ericenouen/ericenouen.github.io/blob/master/assets/image/ParetoFront.png?raw=true)

(Picture from _A computational multi-objective optimization method to improve energy efficiency and thermal comfort in dwellings_)

Previous methods optimize multiple solutions at once to get closer and closer to the pareto front, however, we used the predictor-corrector method described in this work: [Efficient Continuous Pareto Exploration in Multi-Task Learning](https://arxiv.org/abs/2006.16434) to more efficiently explore the pareto front by exploring from one or multiple solutions on the pareto front to find more optimal solutions. We also applied Krylov recycling methods to their technique to reuse computation between exploration steps.

Preprint not yet available.

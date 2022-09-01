---
layout: home
title: "Research Projects"
author_profile: true
permalink: /research/
---

#### Data-free Model Extraction
June 2022 - August 2022

On this project, I participated in an REU at Purdue University under the supervision of Lin Tan. I worked on developing a data-free model extraction attack, which attempts to copy the functionality of a black-box _victim_ model into a _clone model_ through a query interface. We built off of a prior model extraction paper: [Data-Free Model Extraction](https://arxiv.org/abs/2011.14779). This work uses a generator to synthetically create samples that are used to teach the clone model to better match the victim.

In this work we introduced a novel loss that utilized two different clone models and maximized the disagreement between them to find better samples to query the victim model with. We were able to improve both the query efficiency and final accuracy of previous work by a significant margin, and our paper is currently under review by AAAI-23.


#### A Predictor-Corrector Method for fair Graph Spam Detection
June 2021 - May 2022

My first REU was at Lehigh University under the supervision of Sihong Xie. I worked on a multi-objective optimization method for fair graphical models, that balanced performance metric(s) simultaneously with fairness metric(s) to find the tradeoff curve of solutions, called the pareto front.

![Pareto front](https://github.com/ericenouen/ericenouen.github.io/blob/master/assets/image/ParetoFront.png?raw=true)

(Picture from _A computational multi-objective optimization method to improve energy efficiency and thermal comfort in dwellings_)

Previous methods optimize multiple solutions at once to get closer and closer to the pareto front, however, we used the predictor-corrector method described in this work: [Efficient Continuous Pareto Exploration in Multi-Task Learning](https://arxiv.org/abs/2006.16434) to more efficiently explore the pareto front by exploring from one or multiple solutions on the pareto front to find more optimal solutions. We also applied Krylov recycling methods to their technique to reuse computation between exploration steps.

Preprint not yet available.

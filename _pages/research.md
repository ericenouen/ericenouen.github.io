---
layout: home
title: "Research Projects"
author_profile: true
permalink: /research/
---
<div class="warning" style='background-color:#E9D8FD; color: #69337A; border-left: solid #805AD5 4px; border-radius: 4px; padding:0.7em;'>
<span>
<p style='margin-top:1em; text-align:left'>
<b>Purdue University</b></p>
<p style='margin-left:1em;'>
June 2022 - May 2023

On this project, I participated in an REU at Purdue University under the supervision of Lin Tan. I worked on developing a data-free model extraction attack, which attempts to copy the functionality of a black-box _victim_ model into a _clone model_ through a query interface. We built off of a prior model extraction paper: [Data-Free Model Extraction](https://arxiv.org/abs/2011.14779) which uses a generator to synthetically create samples to teach the clone model to better match the victim. This clone model can be used for both avoiding paying per query as well as staging further adversarial attacks, and can even be used to extract training data from the victim model.

In this work we introduced a novel loss that utilized two different clone models and maximized the disagreement between them to find better samples to query the victim model with. We were able to improve both the query efficiency and final accuracy of previous work by a significant margin.

This [paper](https://www.cs.purdue.edu/homes/lintan/publications/disguide-aaai23.pdf) has been accepted to AAAI 2023 where I am second author.
</p>
</div>

<div class="warning" style='background-color:#E9D8FD; color: #69337A; border-left: solid #805AD5 4px; border-radius: 4px; padding:0.7em;'>
<span>
<p style='margin-top:1em; text-align:left'>
<b>Lehigh University</b></p>
<p style='margin-left:1em;'>
June 2021 - May 2022

On this project, I participated in an REU at Lehigh University under the supervision of Sihong Xie. I worked on a multi-objective optimization method for fair graphical models, that balanced performance metric(s) simultaneously with fairness metric(s) to find the tradeoff curve of solutions, called the pareto front.

![Pareto front](https://github.com/ericenouen/ericenouen.github.io/blob/master/assets/image/ParetoFront.png?raw=true) [1]

Previous methods optimize multiple solutions at once to get closer and closer to the pareto front, however, we used the predictor-corrector method described in this work: [Efficient Continuous Pareto Exploration in Multi-Task Learning](https://arxiv.org/abs/2006.16434) to more efficiently explore the pareto front by exploring from one or multiple solutions on the pareto front to find more optimal solutions.

This [paper](http://www.cse.lehigh.edu/~sxie/paper/bigdata2022.pdf) has been accepted to IEEE BigData 2022 where I am co-first author.

[1] Picture from _A computational multi-objective optimization method to improve energy efficiency and thermal comfort in dwellings_
</p>
</div>

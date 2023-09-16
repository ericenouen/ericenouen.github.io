---
layout: home
title: "Research Projects"
author_profile: true
permalink: /research/
---

<style>
div.polaroid {
  width: 800px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  text-align: center;
}

div.container {
  padding: 10px;
}
.alignleft {
	float: left;
}
.alignright {
	float: right;
}
</style>

<body>


<div class="polaroid" style='background-color:#C41230; color: #FFFFFF; border-left: solid #000000 4px; border-radius: 4px; padding:0.7em;'>
<p class="alignleft"><b>Carnegie Mellon University</b></p>
<p class="alignright"><span style="color:#000000">June 2023 - Present</span></p>
<div style="clear: both;"></div>
<p style='margin-left:1em;'>
I worked under Artur Dubrawski on a federated learning approach that provides better explanations for stakeholders. We introduce Prototype-Informed Cross-Silo Router (PICSR) which utilizes a mixture of experts approach to combine local models derived from multiple silos. By utilizing a router to select the best silo for each sample, we can analyze in more detail the differences among institutions. Additionally, we directly embed the decision process in a sample's similarity to a prototype (mean sample) initialized from each silo.

<div>
<img src="https://github.com/ericenouen/ericenouen.github.io/blob/master/assets/image/PICSR_CoreAlgorithm.png?raw=true" alt="Description of the full algorithm for PICSR">
</div>
 
</p></div>
<br>

<div class="polaroid" style='background-color:#CFB991; color: #000000; border-left: solid #8E6F3E 4px; border-radius: 4px; padding:0.7em;'>
<div>
  <p class="alignleft"><b>Purdue University</b></p>
  <p class="alignright"><span style="color:#8E6F3E">June 2022 - May 2023</span></p>
</div>
<div style="clear: both;"></div>
<p style='margin-left:1em;'>
Under the supervision of Lin Tan, I worked on developing a data-free model extraction attack, which attempts to copy the functionality of a black-box <em>victim</em> model into a <em>clone</em> model through a query interface. This clone model can be used for both avoiding paying per query as well as staging further adversarial attacks, and can even be used to extract training data from the victim model.

<div>
<img src="https://github.com/ericenouen/ericenouen.github.io/blob/master/assets/image/Disguide.svg?raw=true" alt="Description of the full algorithm for DisGUIDE">
</div>

Prior work used a generator to synthetically create samples to teach the clone model to better match the victim. However, they used a gradient estimation method on the victim model to train the generator. We introduced a novel loss that utilized two different clone models and maximized the disagreement between them to find better samples to query the victim model with. We were able to improve both the query efficiency and final accuracy of previous work by a significant margin.

This <a href="https://www.cs.purdue.edu/homes/lintan/publications/disguide-aaai23.pdf">paper</a> has been accepted to <b>AAAI 2023</b> where I am second author.
</p></div>
<br>

<div class="polaroid" style='background-color:#653819; color: #FFFFFF; border-left: solid #FED141 4px; border-radius: 4px; padding:0.7em;'>
<div>
  <p class="alignleft"><b>Lehigh University</b></p>
  <p class="alignright"><span style="color:#FED141">June 2021 - May 2022</span></p>
</div>
<div style="clear: both;"></div>
<p style='margin-left:1em;'>
I worked under Sihong Xie on a multi-objective optimization method for fair graphical models, that balanced performance metric(s) simultaneously with fairness metric(s) to find the tradeoff curve of solutions, called the pareto front.

<div>
<img src="https://github.com/ericenouen/ericenouen.github.io/blob/master/assets/image/Lehigh_Pareto.png?raw=true" alt="Pareto Front">
</div>

Previous methods maintain a list of solutions to optimize together towards the pareto front, however, we utilized a <a href="https://arxiv.org/abs/2006.16434">predictor-corrector method</a> to more efficiently explore the pareto front by starting from one optimal point and generating new pareto optimal solutions from it.

This <a href="http://www.cse.lehigh.edu/~sxie/paper/bigdata2022.pdf">paper</a> has been accepted to <b>IEEE BigData 2022</b> where I am co-first author.

</p></div>

</body>

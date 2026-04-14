---
layout: home
title: "Research Thoughts"
author_profile: true
permalink: /thoughts/
---
{% raw %}{% for post in site.posts %}
  <div style="margin-bottom: 2em;">
    <h2>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </h2>
    
    <p style="color: gray; font-size: 0.9em;">
      {{ post.date | date: "%B %d, %Y" }}
    </p>

    <p>
      {{ post.excerpt }}
    </p>

    <a href="{{ post.url }}">Read more →</a>
  </div>
{% endfor %}{% endraw %}

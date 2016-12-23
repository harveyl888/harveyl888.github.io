---
layout: archive
title: "Blog Posts"
date: 2016-11-23
excerpt: "Some short, some long"
---

{% for post in site.categories.blog %}
<div class="row">
  <img src="/images/blogpost.jpg" alt="" style="width:200px;height:125px; display: inline-block;">
  <div style="display: inline-block;">
    <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>
		<a href="{{ post.url }}"><h3 style="margin: 0px;">{{ post.title }}</h3></a>
	  {{ post.excerpt }}
  </div>
</div>
{% endfor %}

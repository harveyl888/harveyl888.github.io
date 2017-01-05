---
layout: archive
title: "Blog Posts"
date: 2016-11-23
excerpt: "Some short, some long"
---

{% for post in site.categories.blog %}
<div class="row">
  {% if post.date %}<span class="entry-date date published"><time datetime="{{ post.date | date: "%Y-%m-%d" }}" itemprop="datePublished">{{ post.date | date: "%B %d, %Y" }}</time></span>{% endif %}
   <h3 class="post-title" itemprop="name" style="margin: 0px;"><a href="{{ site.url }}{{ post.url }}">{{ post.title }}</a></h3>
   <p class="post-excerpt" itemprop="description">{{ post.excerpt | strip_html | truncate: 120 }}</p>
</div>
{% endfor %}

---
layout: archive
title: "Long Posts"
date: 2016-11-23
excerpt: "Long, thoughtful posts"
---

<div class="tiles">
{% for post in site.categories.longposts %}
  {% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->
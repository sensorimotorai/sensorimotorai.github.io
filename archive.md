---
layout: single
title: Archive
permalink: /archive/
toc: false
---

{% assign grouped = site.posts | group_by_exp: "post", "post.date | date: '%Y-%m'" %}
<ul>
  {% for group in grouped %}
    {% assign ym = group.name %}
    <li id="{{ ym }}">
      <h3>{{ ym | date: "%B %Y" }}</h3>
      <ul>
        {% for post in group.items %}
          <li><a href="{{ post.url }}">{{ post.title }}</a> - {{ post.date | date: "%b %d, %Y" }}</li>
        {% endfor %}
      </ul>
    </li>
  {% endfor %}
</ul>

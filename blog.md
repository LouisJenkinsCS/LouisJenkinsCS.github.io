---
layout: page
title: Blog
permalink: /blog
---

This blog will feature various content from my personal thoughts to technical
information and results from past or on-going research, even to venting about any
frustration I am feeling. The blog posts can be seen below.

**Note: This Blog is under heavy construction.**

<ul>
  {% assign sorted = (site.posts | sort: 'date') | reverse %}
  {% for post in sorted %}
  <li>
    <a href="{{ post.url }}">{{ post.title }}</a>
  </li>
  {% endfor %}
</ul>

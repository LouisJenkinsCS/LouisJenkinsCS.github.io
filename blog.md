---
layout: page
title: Blog
permalink: /blog
---

{% for post in site.posts %}
  <center>
    <h2>
      {{post.title}}
    </h2>
  </center>
  {{post.content}}

  <b>Posted on {{post.date | date: "%B %d, %Y"}}</b>
{% endfor %}

---
layout: default
title: Categories
permalink: /categories/
---

<h1>カテゴリ一覧</h1>

{% for category in site.categories %}
  <section id="{{ category[0] | slugify }}">
    <h2>{{ category[0] }}</h2>
    <ul>
      {% for post in category[1] %}
        <li>
          <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
          <small>（{{ post.date | date: "%Y-%m-%d" }}）</small>
        </li>
      {% endfor %}
    </ul>
  </section>
{% endfor %}

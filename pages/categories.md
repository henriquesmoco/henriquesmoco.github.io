---
layout: categories
title: Categories
description: List my posts by category
keywords: Categories
comments: false
menu: Categories
permalink: /categories/
---

<section class="container">
{% assign sorted_categories = site.categories | sort %}
{% for category in sorted_categories %}
<h3 id="{{ category[0] }}">{{ category | first }}</h3>
<ul>
    {% for post in category.last %}
    <li class="post-list-item">
    <span class="posts-info">{{ post.date | date:"%Y-%m-%d" }}</span>
    <a href="{{ site.url }}{{ post.url }}" >{{ post.title }}</a>
    </li>
    {% endfor %}
</ul>
{% endfor %}
</section>
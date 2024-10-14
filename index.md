---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
menu: Home
---

<section class="posts">
  {% for post in site.posts %}
    <article class="post">

      <h3><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h3>

      <p class="post-description">
        {{ post.excerpt | strip_html | strip }}
      </p>

      <span class="post-info">
        <i class="fa fa-calendar" aria-hidden="true"></i> {{ post.date | date: "%Y/%m/%d" }}
      </span>

      {% for cat in post.categories %}
      <span class="post-info">
        <i class="fa fa-folder-o" aria-hidden="true"></i>
        <a href="{{ site.url }}/categories/#{{ cat }}" title="{{ cat }}">{{ cat }}</a>
      </span>
      {% endfor %}

    </article>
  {% endfor %}
</section>
---
layout: default
permalink: /blog/
title: Blog
nav: true
nav_order: 1
pagination:
  enabled: true
  collection: posts
  permalink: /page/:num/
  per_page: 5
  sort_field: date
  sort_reverse: true
  trail:
    before: 1 # The number of links before the current page
    after: 3 # The number of links after the current page
---

<div class="post">

  {% assign blog_name_size = site.blog_name | size %}
  {% assign blog_description_size = site.blog_description | size %}

  {% if blog_name_size > 0 or blog_description_size > 0 %}

  <div class="fuwari-banner">
    <div class="fuwari-banner-content">
      {% if site.title == 'blank' %}
        <h1>{{ site.first_name }} {{ site.last_name }}'s {{ site.blog_name }}</h1>
      {% else %}
        <h1>{{ site.title }}</h1>
      {% endif %}
      <p>{{ site.blog_description }}</p>
    </div>
  </div>
  {% endif %}

{% assign featured_posts = site.posts | where: "featured", "true" %}
{% if featured_posts.size > 0 %}
<br>

<div class="container featured-posts">
{% assign is_even = featured_posts.size | modulo: 2 %}
<div class="row row-cols-{% if featured_posts.size <= 2 or is_even == 0 %}2{% else %}3{% endif %}">
{% for post in featured_posts %}
<div class="col mb-4">
<a href="{{ post.url | relative_url }}">
<div class="card hoverable">
<div class="row g-0">
<div class="col-md-12">
<div class="card-body">
<div class="float-right">
<i class="fa-solid fa-thumbtack fa-xs"></i>
</div>
<h3 class="card-title text-lowercase">{{ post.title }}</h3>
<p class="card-text">{{ post.description }}</p>

                    {% if post.external_source == blank %}
                      {% assign read_time = post.content | number_of_words | divided_by: 180 | plus: 1 %}
                    {% else %}
                      {% assign read_time = post.feed_content | strip_html | number_of_words | divided_by: 180 | plus: 1 %}
                    {% endif %}
                    {% assign year = post.date | date: "%Y" %}

                    <p class="post-meta">
                      {{ read_time }} min read &nbsp; &middot; &nbsp;
                      <a href="{{ year | prepend: '/blog/' | relative_url }}">
                        <i class="fa-solid fa-calendar fa-sm"></i> {{ year }} </a>
                    </p>
                  </div>
                </div>
              </div>
            </div>
          </a>
        </div>
      {% endfor %}
      </div>
    </div>
    <hr>

{% endif %}

  <ul class="fuwari-post-list">

    {% if page.pagination.enabled %}
      {% assign postlist = paginator.posts %}
    {% else %}
      {% assign postlist = site.posts %}
    {% endif %}

    {% for post in postlist %}

    {% if post.external_source == blank %}
      {% assign read_time = post.content | number_of_words | divided_by: 180 | plus: 1 %}
    {% else %}
      {% assign read_time = post.feed_content | strip_html | number_of_words | divided_by: 180 | plus: 1 %}
    {% endif %}

    <li class="fuwari-post-card">

      <h3 class="fuwari-post-title">
        {% if post.redirect == blank %}
          <a class="post-title" href="{{ post.url | relative_url }}">{{ post.title }}</a>
        {% elsif post.redirect contains '://' %}
          <a class="post-title" href="{{ post.redirect }}" target="_blank">{{ post.title }} <i class="fa-solid fa-arrow-up-right-from-square fa-2xs"></i></a>
        {% else %}
          <a class="post-title" href="{{ post.redirect | relative_url }}">{{ post.title }}</a>
        {% endif %}
      </h3>

      {% if post.description %}
      <p class="fuwari-post-desc">{{ post.description }}</p>
      {% endif %}

      <div class="fuwari-meta">
        <span class="fuwari-pill">
          <i class="fa-regular fa-calendar fa-xs"></i> {{ post.date | date: '%b %d, %Y' }}
        </span>
        <span class="fuwari-pill">
          <i class="fa-regular fa-clock fa-xs"></i> {{ read_time }} min read
        </span>
        {% for tag in post.tags %}
          <a class="fuwari-pill fuwari-pill-tag" href="{{ tag | slugify | prepend: '/blog/tag/' | relative_url }}">
            # {{ tag }}</a>
        {% endfor %}
        {% for category in post.categories %}
          <a class="fuwari-pill fuwari-pill-tag" href="{{ category | slugify | prepend: '/blog/category/' | relative_url }}">
            <i class="fa-solid fa-tag fa-2xs"></i> {{ category }}</a>
        {% endfor %}
      </div>

    </li>

    {% endfor %}

  </ul>

  {% if page.pagination.enabled %}
  {% include pagination.liquid %}
  {% endif %}

</div>

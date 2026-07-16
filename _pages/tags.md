---
layout: page
title: Tags
permalink: /tags/
---

{% assign all_tags = site.notes | map: "tags" | flatten | compact | uniq | sort %}

<div class="tags">
  {% for tag in all_tags %}
  <a class="internal-link tag" href="{{ site.baseurl }}/tags/#{{ tag | slugify }}">{{ tag }}</a>
  {% endfor %}
</div>

{% for tag in all_tags %}
<h3 id="{{ tag | slugify }}">{{ tag }}</h3>

<ul>
  {% assign tagged_notes = site.notes | where_exp: "note", "note.tags contains tag" | sort: "date" | reverse %}
  {% for note in tagged_notes %}
    <li>{{ note.date | date: "%Y-%m-%d" }} &mdash; <a class="internal-link" href="{{ site.baseurl }}{{ note.url }}">{{ note.title }}</a></li>
  {% endfor %}
</ul>
{% endfor %}

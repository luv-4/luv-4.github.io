---
title: "일반화 프로그래밍"
excerpt: "With C++"
layout: archive
permalink: categories/generic
author_profile: true
entries_layout: grid
sidebar_main: true
header:
  overlay_image: /assets/images/back.jpg
  overlay_filter: linear-gradient(to right, rgba(0, 0, 0, 0.9) 25%, rgba(0, 0, 0, 0))
---

{% assign posts = site.categories.Generic %}

<div class="grid__wrapper">
{% for post in posts %} {% include archive-single.html type="grid"
  %} {% endfor %}
</div>

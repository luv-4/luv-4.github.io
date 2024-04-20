---
title: "일반화 프로그래밍"
excerpt: "with C++"
layout: archive
permalink: categories/generic
author_profile: true
entries_layout: grid
sidebar_main: true
header:
  overlay_image: /assets/images/background.png
  overlay_filter: 0.1 # same as adding an opacity of 0.5 to a black background
---

{% assign posts = site.categories._pages/categories/category-etc.md %}

<div class="grid__wrapper">
{% for post in posts %} {% include archive-single.html type="grid"
  %} {% endfor %}
</div>

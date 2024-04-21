---
title: "술"
excerpt: "취미생활"
layout: archive
permalink: categories/alcohol
author_profile: true
sidebar_main: true
header:
  overlay_image: /assets/images/back.jpg
  overlay_filter: linear-gradient(to right, rgba(0, 0, 0, 0.9) 25%, rgba(0, 0, 0, 0))
---

{% assign posts = site.categories.Alcohol %}

<div class="grid__wrapper">

{% for post in posts %} {% include archive-single.html type="grid"
  %} {% endfor %}

</div>
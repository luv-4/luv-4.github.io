---
title: "요리"
excerpt: "취미생활"
layout: archive
permalink: categories/cooking
author_profile: true
sidebar_main: true
header:
  overlay_image: /assets/images/background.png
  overlay_filter: 0.1 # same as adding an opacity of 0.5 to a black background
---

{% assign posts = site.categories.Cooking %}

<div class="grid__wrapper">

{% for post in posts %} {% include archive-single.html type="grid"
  %} {% endfor %}

</div>
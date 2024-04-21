---
title: "月기장"
excerpt: "한 달에 한 번 쓰는 일기장"
layout: archive
permalink: categories/diary
author_profile: true
sidebar_main: true
header:
  overlay_image: /assets/images/back.jpg
  overlay_filter: linear-gradient(to right, rgba(0, 0, 0, 0.9) 25%, rgba(0, 0, 0, 0))
---

{% assign posts = site.categories.Diary %}

<div class="grid__wrapper">

{% for post in posts %} {% include archive-single.html type="grid"
  %} {% endfor %}

</div>
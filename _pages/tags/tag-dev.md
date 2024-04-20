---
title: "개발"
excerpt: "개발과 관련된 글들"
layout: archive
permalink: tags/dev
author_profile: true
sidebar_main: true
header:
  overlay_image: /assets/images/background.png
  overlay_filter: 0.1 # same as adding an opacity of 0.5 to a black background
---

{% assign posts = site.tags.Dev %}

<div class="grid__wrapper">

{% for post in posts %} {% include archive-single.html type="grid"
  %} {% endfor %}

</div>

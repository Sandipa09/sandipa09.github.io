---
layout: archive
title: "Gallery"
permalink: /gallery/
author_profile: true
---

{% for post in site.gallery %}
  {% include archive-single.html %}
{% endfor %}
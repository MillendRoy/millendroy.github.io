---
layout: page
title: art gallery
permalink: /gallery/
description: A collection of sketches and paintings.
nav: true
nav_order: 4
---

<style>
.collage {
  column-count: 3;
  column-gap: 12px;
}
.collage img {
  width: 100%;
  display: block;
  margin-bottom: 12px;
  border: 2px solid #222;
  break-inside: avoid;
}
@media (max-width: 900px) {
  .collage { column-count: 2; }
}
@media (max-width: 500px) {
  .collage { column-count: 1; }
}
</style>

<div class="collage">
  {% for item in site.data.gallery %}
    <img src="{{ item.image | relative_url }}" alt="{{ item.alt }}" loading="lazy">
  {% endfor %}
</div>
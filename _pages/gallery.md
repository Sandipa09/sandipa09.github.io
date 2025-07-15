---
layout: single
title: "Gallery"
permalink: /gallery/
author_profile: true
---

<div class="photo-gallery">
  {% for gallery_item in site.gallery %}
    <div class="gallery-section">
      <h2>{{ gallery_item.title }}</h2>
      <p>{{ gallery_item.description }}</p>
      
      <article class="gallery">
        {% for image in gallery_item.images %}
          <img src="{{ image | absolute_url }}" alt="{{ gallery_item.title }}" tabindex="0" />
        {% endfor %}
      </article>
      
      {% if gallery_item.content != "" %}
        <div class="gallery-text">
          {{ gallery_item.content }}
        </div>
      {% endif %}
    </div>
  {% endfor %}
</div>

<style>
.gallery {
  --size: 100px;
  display: grid;
  grid-template-columns: repeat(6, var(--size));
  grid-auto-rows: var(--size);
  margin-bottom: var(--size);
  place-items: start center;
  gap: 5px;
}

.gallery:has(:hover) img:not(:hover),
.gallery:has(:focus) img:not(:focus) {
  filter: brightness(0.5) contrast(0.5);
}

.gallery img {
  object-fit: cover;
  width: calc(var(--size) * 2);
  height: calc(var(--size) * 2);
  clip-path: path("M90,10 C100,0 100,0 110,10 190,90 190,90 190,90 200,100 200,100 190,110 190,110 110,190 110,190 100,200 100,200 90,190 90,190 10,110 10,110 0,100 0,100 10,90Z");
  transition: clip-path 0.25s, filter 0.75s;
  grid-column: auto / span 2;
  border-radius: 5px;
}

.gallery img:nth-child(5n - 1) { 
  grid-column: 2 / span 2;
}

.gallery img:hover,
.gallery img:focus {
  clip-path: path("M0,0 C0,0 200,0 200,0 200,0 200,100 200,100 200,100 200,200 200,200 200,200 100,200 100,200 100,200 100,200 0,200 0,200 0,100 0,100 0,100 0,100 0,100Z");
  z-index: 1;
  transition: clip-path 0.25s, filter 0.25s;
}

.gallery img:focus {
  outline: 1px dashed black;
  outline-offset: -5px;
}

.gallery-section {
  margin-bottom: 60px;
  border-bottom: 1px solid #eee;
  padding-bottom: 40px;
}

.gallery-text {
  margin-top: 30px;
  font-size: 1.1em;
  line-height: 1.6;
}
</style>
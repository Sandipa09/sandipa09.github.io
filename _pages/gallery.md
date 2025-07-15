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
      
      <div class="image-grid">
        {% for image in gallery_item.images %}
          <div class="image-item">
            <img src="{{ image | absolute_url }}" alt="{{ gallery_item.title }}">
          </div>
        {% endfor %}
      </div>
      
      {% if gallery_item.content != "" %}
        <div class="gallery-text">
          {{ gallery_item.content }}
        </div>
      {% endif %}
    </div>
  {% endfor %}
</div>

<style>
.image-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 15px;
  margin: 20px 0;
}

.image-item img {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-radius: 8px;
}

.gallery-section {
  margin-bottom: 40px;
  border-bottom: 1px solid #eee;
  padding-bottom: 20px;
}
</style>
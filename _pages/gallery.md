---
layout: single
title: "Gallery"
permalink: /gallery/
author_profile: true
---

<!-- Splide CSS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@splidejs/splide@4.1.4/dist/css/splide.min.css">

<div class="photo-gallery">
  {% for gallery_item in site.gallery %}
    <div class="gallery-section {% cycle 'left', 'right' %}">
      <div class="gallery-content">
        <div class="gallery-info">
          <h2>{{ gallery_item.title }}</h2>
          <p>{{ gallery_item.description }}</p>
          {% if gallery_item.content != "" %}
            <div class="gallery-text">
              {{ gallery_item.content }}
            </div>
          {% endif %}
        </div>
        
        <div class="carousel-container">
          <!-- Debug info -->
          <p>Debug: {{ gallery_item.images.size }} images found</p>
          
          <section class="splide" id="splide-{{ forloop.index }}">
            <div class="splide__track">
              <ul class="splide__list">
                {% for image in gallery_item.images %}
                  <li class="splide__slide">
                    <img src="{{ image | absolute_url }}" alt="{{ gallery_item.title }}" />
                    <p>Debug: {{ image }}</p>
                  </li>
                {% endfor %}
              </ul>
            </div>
          </section>
        </div>
      </div>
    </div>
  {% endfor %}
</div>

<style>
.carousel-container {
  flex: 1;
  max-width: 500px;
  border: 2px solid red; /* Debug border */
}

.splide {
  border: 2px solid blue; /* Debug border */
  min-height: 300px;
}

.splide__slide {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 300px;
  border: 1px solid green; /* Debug border */
}

.splide__slide img {
  width: 100%;
  max-width: 400px;
  height: 250px;
  object-fit: cover;
  border-radius: 10px;
  display: block;
}

.gallery-section {
  margin-bottom: 60px;
  border-bottom: 1px solid #eee;
  padding-bottom: 40px;
}

.gallery-content {
  display: flex;
  align-items: flex-start;
  gap: 40px;
}

.gallery-info {
  flex: 1;
  min-width: 300px;
}

.gallery-section.left .gallery-content {
  flex-direction: row;
}

.gallery-section.right .gallery-content {
  flex-direction: row-reverse;
}

.gallery-text {
  margin-top: 20px;
  font-size: 1.1em;
  line-height: 1.6;
}

/* Responsive design */
@media (max-width: 768px) {
  .gallery-content {
    flex-direction: column !important;
  }
  
  .gallery-info {
    min-width: auto;
  }
  
  .carousel-container {
    max-width: 100%;
  }
}
</style>

<!-- Splide JS -->
<script src="https://cdn.jsdelivr.net/npm/@splidejs/splide@4.1.4/dist/js/splide.min.js"></script>

<script>
document.addEventListener('DOMContentLoaded', function () {
  console.log('DOM loaded, initializing carousels...');
  
  {% for gallery_item in site.gallery %}
    console.log('Initializing carousel {{ forloop.index }}');
    
    const splideElement = document.getElementById('splide-{{ forloop.index }}');
    if (splideElement) {
      console.log('Found element:', splideElement);
      
      try {
        new Splide('#splide-{{ forloop.index }}', {
          type: 'loop',
          autoplay: false,  // Disable autoplay for debugging
          arrows: true,
          pagination: true,
          perPage: 1,
          gap: 0
        }).mount();
        
        console.log('Carousel {{ forloop.index }} mounted successfully');
      } catch (error) {
        console.error('Error mounting carousel {{ forloop.index }}:', error);
      }
    } else {
      console.error('Could not find element splide-{{ forloop.index }}');
    }
  {% endfor %}
});
</script>
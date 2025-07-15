---
layout: single
title: "Gallery"
permalink: /gallery/
author_profile: true
---

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
          <div class="carousel-wrapper">
            <div class="carousel-slides" id="carousel-{{ forloop.index }}">
              {% for image in gallery_item.images %}
                <div class="slide {% if forloop.first %}active{% endif %}">
                  <img src="{{ image | absolute_url }}" alt="{{ gallery_item.title }}" />
                </div>
              {% endfor %}
            </div>
          </div>
          
          <!-- Carousel Dots -->
          <div class="carousel-dots">
            {% for image in gallery_item.images %}
              <span class="dot{% if forloop.first %} active{% endif %}" onclick="currentSlide({{ forloop.index }}, {{ forloop.parentloop.index }})"></span>
            {% endfor %}
          </div>
        </div>
      </div>
    </div>
  {% endfor %}
</div>

<style>
.carousel-container {
  flex: 1;
  max-width: 500px;
}

.carousel-wrapper {
  position: relative;
  overflow: hidden;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
}

.carousel-slides {
  display: flex;
  transition: transform 0.5s ease;
}

.slide {
  min-width: 100%;
  display: none;
}

.slide.active {
  display: block;
}

.slide img {
  width: 100%;
  height: 350px;
  object-fit: cover;
  border-radius: 10px;
}

/* Carousel Dots */
.carousel-dots {
  text-align: center;
  margin-top: 15px;
}

.dot {
  cursor: pointer;
  height: 12px;
  width: 12px;
  margin: 0 5px;
  background-color: #bbb;
  border-radius: 50%;
  display: inline-block;
  transition: background-color 0.3s ease;
}

.dot:hover {
  background-color: #717171;
}

.dot.active {
  background-color: #333;
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

<script>
function currentSlide(slideIndex, carouselIndex) {
  const carouselContainer = document.querySelectorAll('.carousel-container')[carouselIndex - 1];
  const slides = carouselContainer.querySelectorAll('.slide');
  const dots = carouselContainer.querySelectorAll('.dot');
  
  // Hide all slides and remove active from dots
  slides.forEach(slide => slide.classList.remove('active'));
  dots.forEach(dot => dot.classList.remove('active'));
  
  // Show selected slide and activate corresponding dot
  slides[slideIndex - 1].classList.add('active');
  dots[slideIndex - 1].classList.add('active');
}
</script>
---
layout: single
title: "Gallery"
permalink: /gallery/
author_profile: true
---

<!-- Swiper CSS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/swiper@11/swiper-bundle.min.css" />

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
          {% if gallery_item.images.size > 1 %}
            <!-- Multiple images: Use Swiper -->
            <div class="swiper gallery-swiper">
              <div class="swiper-wrapper">
                {% for image in gallery_item.images %}
                  <div class="swiper-slide">
                    <img src="{{ image | absolute_url }}" alt="{{ gallery_item.title }}" />
                  </div>
                {% endfor %}
              </div>
              <div class="swiper-pagination"></div>
              <div class="swiper-button-next"></div>
              <div class="swiper-button-prev"></div>
            </div>
          {% else %}
            <!-- Single image: Just display it -->
            <div class="single-image">
              {% for image in gallery_item.images %}
                <img src="{{ image | absolute_url }}" alt="{{ gallery_item.title }}" />
              {% endfor %}
            </div>
          {% endif %}
        </div>
      </div>
    </div>
  {% endfor %}
</div>

<style>
.carousel-container {
  flex: 1;
  max-width: 500px;
  position: relative;
}

.gallery-swiper {
  width: 100%;
  height: 300px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  overflow: hidden;
  background: #fff;
}

.swiper-slide {
  display: flex;
  align-items: center;
  justify-content: center;
  background: #f8f8f8;
}

.swiper-slide img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* Single image styling */
.single-image {
  background: #fff;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.single-image img {
  width: 100%;
  height: 300px;
  object-fit: cover;
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

/* Swiper custom styling */
.swiper-pagination {
  bottom: 10px !important;
}

.swiper-pagination-bullet {
  background: rgba(255, 255, 255, 0.8);
  width: 12px;
  height: 12px;
  margin: 0 5px !important;
  opacity: 0.8;
}

.swiper-pagination-bullet-active {
  background: #fff;
  opacity: 1;
}

.swiper-button-next,
.swiper-button-prev {
  background: rgba(0, 0, 0, 0.5);
  width: 40px !important;
  height: 40px !important;
  border-radius: 50%;
  color: white !important;
  margin-top: -20px !important;
}

.swiper-button-next:hover,
.swiper-button-prev:hover {
  background: rgba(0, 0, 0, 0.8);
}

.swiper-button-next::after,
.swiper-button-prev::after {
  font-size: 16px !important;
  font-weight: bold;
}

.swiper-button-next {
  right: 10px !important;
}

.swiper-button-prev {
  left: 10px !important;
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
    max-width: 100%; /* Allow full width on mobile */
    width: 100%; /* Ensure it takes full width */
  }
  
  .gallery-swiper {
    height: 250px;
  }
  
  .single-image img {
    height: 250px;
    width: 100%; /* Ensure full width */
  }
  
  .swiper-button-next,
  .swiper-button-prev {
    width: 35px !important;
    height: 35px !important;
    margin-top: -17.5px !important;
  }
  
  .swiper-button-next::after,
  .swiper-button-prev::after {
    font-size: 14px !important;
  }
  
  .swiper-pagination-bullet {
    width: 14px;
    height: 14px;
    margin: 0 8px !important;
  }
}

@media (max-width: 480px) {
  .gallery-swiper {
    height: 200px;
  }
  
  .single-image {
    width: 100%; /* Ensure single image container is full width */
  }
  
  .single-image img {
    height: 200px;
    width: 100%; /* Ensure full width on small mobile */
  }
  
  .gallery-content {
    gap: 20px;
  }
  
  .gallery-section {
    margin-bottom: 40px;
  }
  
  .swiper-button-next,
  .swiper-button-prev {
    width: 30px !important;
    height: 30px !important;
    margin-top: -15px !important;
  }
  
  .swiper-button-next::after,
  .swiper-button-prev::after {
    font-size: 12px !important;
  }
}
</style>

<!-- Swiper JS -->
<script src="https://cdn.jsdelivr.net/npm/swiper@11/swiper-bundle.min.js"></script>

<script>
document.addEventListener('DOMContentLoaded', function() {
  // Initialize all Swiper instances
  const swipers = document.querySelectorAll('.gallery-swiper');
  
  swipers.forEach(function(swiperEl) {
    const swiper = new Swiper(swiperEl, {
      slidesPerView: 1,
      spaceBetween: 0,
      loop: true,
      autoplay: false, // Disabled by default
      speed: 400,
      
      // Pagination
      pagination: {
        el: swiperEl.querySelector('.swiper-pagination'),
        clickable: true,
      },
      
      // Navigation arrows
      navigation: {
        nextEl: swiperEl.querySelector('.swiper-button-next'),
        prevEl: swiperEl.querySelector('.swiper-button-prev'),
      },
      
      // Touch settings for better mobile experience
      touchRatio: 1,
      touchAngle: 45,
      simulateTouch: true,
      
      // Responsive breakpoints (optional - Swiper handles most automatically)
      breakpoints: {
        320: {
          slidesPerView: 1,
        },
        768: {
          slidesPerView: 1,
        },
        1024: {
          slidesPerView: 1,
        },
      }
    });
    
    // Add hover autoplay for non-touch devices only
    if (!('ontouchstart' in window)) {
      swiperEl.addEventListener('mouseenter', function() {
        swiper.autoplay.start();
        swiper.params.autoplay.delay = 2000;
      });
      
      swiperEl.addEventListener('mouseleave', function() {
        swiper.autoplay.stop();
      });
    }
  });
});
</script>
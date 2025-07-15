---
layout: single
title: "Gallery"
permalink: /gallery/
author_profile: true
---

<!-- Glide.js CSS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@glidejs/glide/dist/css/glide.core.min.css">
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@glidejs/glide/dist/css/glide.theme.min.css">

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
            <!-- Multiple images: Use Glide -->
            <div class="glide gallery-glide" data-gallery="gallery-{{ forloop.index }}">
              <div class="glide__track" data-glide-el="track">
                <ul class="glide__slides">
                  {% for image in gallery_item.images %}
                    <li class="glide__slide">
                      <img src="{{ image | absolute_url }}" alt="{{ gallery_item.title }}" />
                    </li>
                  {% endfor %}
                </ul>
              </div>
              
              <div class="glide__arrows" data-glide-el="controls">
                <button class="glide__arrow glide__arrow--left" data-glide-dir="<">‹</button>
                <button class="glide__arrow glide__arrow--right" data-glide-dir=">">›</button>
              </div>
              
              <div class="glide__bullets" data-glide-el="controls[nav]">
                {% for image in gallery_item.images %}
                  <button class="glide__bullet" data-glide-dir="={{ forloop.index0 }}"></button>
                {% endfor %}
              </div>
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

.gallery-glide {
  width: 100%;
  height: 300px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  overflow: hidden;
  background: #fff;
  position: relative;
}

.glide__slide {
  display: flex;
  align-items: center;
  justify-content: center;
  background: #f8f8f8;
  height: 300px;
}

.glide__slide img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* Single image styling - match glide dimensions */
.single-image {
  width: 100%;
  height: 300px;
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
  height: 100%;
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

/* Custom Glide styling */
.glide__arrows {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 100%;
  pointer-events: none;
  z-index: 10;
}

.glide__arrow {
  position: absolute;
  background: rgba(0, 0, 0, 0.5);
  color: white;
  border: none;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  font-size: 18px;
  cursor: pointer;
  pointer-events: auto;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background 0.3s;
}

.glide__arrow:hover {
  background: rgba(0, 0, 0, 0.8);
}

.glide__arrow--left {
  left: 10px;
}

.glide__arrow--right {
  right: 10px;
}

.glide__bullets {
  position: absolute;
  bottom: 15px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 8px;
  z-index: 10;
}

.glide__bullet {
  background: rgba(255, 255, 255, 0.6);
  border: none;
  border-radius: 50%;
  width: 12px;
  height: 12px;
  cursor: pointer;
  transition: background 0.3s;
}

.glide__bullet--active {
  background: white;
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
    width: 100%;
  }
  
  .gallery-glide {
    height: 250px;
  }
  
  .glide__slide {
    height: 250px;
  }
  
  .single-image {
    height: 250px;
    width: 100%;
  }
  
  .glide__arrow {
    width: 35px;
    height: 35px;
    font-size: 16px;
  }
  
  .glide__bullet {
    width: 14px;
    height: 14px;
  }
}

@media (max-width: 480px) {
  .gallery-glide {
    height: 200px;
  }
  
  .glide__slide {
    height: 200px;
  }
  
  .single-image {
    height: 200px;
    width: 100%;
  }
  
  .gallery-content {
    gap: 20px;
  }
  
  .gallery-section {
    margin-bottom: 40px;
  }
  
  .glide__arrow {
    width: 30px;
    height: 30px;
    font-size: 14px;
  }
}
</style>

<!-- Glide.js JavaScript -->
<script src="https://cdn.jsdelivr.net/npm/@glidejs/glide/dist/glide.min.js"></script>

<script>
(function() {
  'use strict';
  
  function initializeGalleries() {
    console.log('🚀 Starting gallery initialization...');
    
    // Check if Glide is available
    if (typeof Glide === 'undefined') {
      console.error('❌ Glide.js is not loaded!');
      return;
    }
    
    console.log('✅ Glide.js is loaded');
    
    // Find all gallery elements
    const galleries = document.querySelectorAll('.gallery-glide');
    console.log('Found', galleries.length, 'galleries');
    
    if (galleries.length === 0) {
      console.log('No galleries found');
      return;
    }
    
    galleries.forEach(function(gallery, index) {
      const galleryId = gallery.getAttribute('data-gallery') || 'gallery-' + index;
      console.log('Initializing gallery:', galleryId);
      
      try {
        // Create Glide instance
        const glide = new Glide(gallery, {
          type: 'carousel',
          startAt: 0,
          perView: 1,
          focusAt: 'center',
          gap: 0,
          autoplay: false,
          hoverpause: true,
          animationDuration: 400,
          animationTimingFunc: 'ease',
          keyboard: true,
          swipeThreshold: 80,
          dragThreshold: 120
        });
        
        // Store reference
        gallery._glide = glide;
        
        // Mount the glide
        glide.mount();
        
        console.log('✅ Gallery', galleryId, 'initialized successfully');
        
        // Test if controls work
        const arrows = gallery.querySelectorAll('.glide__arrow');
        const bullets = gallery.querySelectorAll('.glide__bullet');
        console.log('Found', arrows.length, 'arrows and', bullets.length, 'bullets');
        
        // Add hover autoplay for desktop only
        if (!('ontouchstart' in window)) {
          gallery.addEventListener('mouseenter', function() {
            glide.update({ autoplay: 2000 });
            glide.play();
          });
          
          gallery.addEventListener('mouseleave', function() {
            glide.pause();
            glide.update({ autoplay: false });
          });
        }
        
      } catch (error) {
        console.error('❌ Error initializing gallery', galleryId, ':', error);
      }
    });
  }
  
  // Try multiple initialization methods
  if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', initializeGalleries);
  } else {
    initializeGalleries();
  }
  
  // Also try with a delay in case Jekyll is slow
  setTimeout(initializeGalleries, 500);
  
})();
</script>
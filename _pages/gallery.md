---
layout: single
title: "Gallery"
permalink: /gallery/
author_profile: true
---

<!-- Flickity CSS -->
<link rel="stylesheet" href="https://unpkg.com/flickity@2/dist/flickity.min.css">

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
            <!-- Multiple images: Use carousel -->
            <div class="carousel" data-flickity='{ "cellAlign": "left", "contain": true, "autoPlay": false, "pauseAutoPlayOnHover": false, "wrapAround": true }'>
              {% for image in gallery_item.images %}
                <div class="carousel-cell">
                  <img src="{{ image | absolute_url }}" alt="{{ gallery_item.title }}" />
                </div>
              {% endfor %}
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
}

.carousel {
  background: #fff;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  overflow: hidden; /* Ensure content stays within bounds */
}

.carousel-cell {
  width: 100%;
  height: 300px;
  margin-right: 10px;
  background: #f8f8f8;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  /* Prevent flickity from resizing cells incorrectly */
  flex-shrink: 0;
}

.carousel-cell img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 10px;
  /* Prevent image dragging issues on mobile */
  -webkit-user-drag: none;
  -khtml-user-drag: none;
  -moz-user-drag: none;
  -o-user-drag: none;
  user-drag: none;
}

/* Single image styling */
.single-image {
  background: #fff;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  display: flex;
  align-items: center;
  justify-content: center;
}

.single-image img {
  width: 100%;
  height: 300px;
  object-fit: cover;
  border-radius: 10px;
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

/* Flickity custom styling */
.flickity-page-dots {
  bottom: -30px;
}

.flickity-page-dots .dot {
  width: 12px;
  height: 12px;
  background: #bbb;
  border-radius: 50%;
  margin: 0 5px;
}

.flickity-page-dots .dot.is-selected {
  background: #333;
}

.flickity-prev-next-button {
  background: rgba(0, 0, 0, 0.5);
  color: white;
  border-radius: 50%;
  width: 40px;
  height: 40px;
}

.flickity-prev-next-button:hover {
  background: rgba(0, 0, 0, 0.8);
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
  
  /* Mobile-specific carousel fixes */
  .carousel {
    margin: 0;
    width: 100%;
  }
  
  .carousel-cell {
    height: 250px; /* Slightly smaller on mobile */
    margin-right: 5px; /* Reduce margin on mobile */
  }
  
  /* Improve touch interaction */
  .flickity-viewport {
    -webkit-overflow-scrolling: touch;
  }
  
  /* Adjust navigation buttons for mobile */
  .flickity-prev-next-button {
    width: 35px;
    height: 35px;
    top: 50%;
    transform: translateY(-50%);
  }
  
  .flickity-prev-next-button.previous {
    left: 10px;
  }
  
  .flickity-prev-next-button.next {
    right: 10px;
  }
  
  /* Make dots more touch-friendly */
  .flickity-page-dots .dot {
    width: 14px;
    height: 14px;
    margin: 0 8px;
  }
}

/* Extra small devices */
@media (max-width: 480px) {
  .carousel-cell {
    height: 200px;
  }
  
  .single-image img {
    height: 200px;
  }
  
  .gallery-content {
    gap: 20px;
  }
  
  .gallery-section {
    margin-bottom: 40px;
  }
}
</style>

<!-- Flickity JS -->
<script src="https://unpkg.com/flickity@2/dist/flickity.pkgd.min.js"></script>

<script>
document.addEventListener('DOMContentLoaded', function() {
  // Initialize all carousels
  const carousels = document.querySelectorAll('.carousel');
  
  carousels.forEach(function(carousel) {
    const isMobile = window.innerWidth <= 768;
    
    const flkty = new Flickity(carousel, {
      cellAlign: 'left',
      contain: true,
      autoPlay: false,
      pauseAutoPlayOnHover: false,
      wrapAround: true,
      // Mobile-specific options
      friction: isMobile ? 0.8 : 0.28,
      selectedAttraction: isMobile ? 0.2 : 0.025,
      freeScrollFriction: isMobile ? 0.8 : 0.075,
      // Prevent issues with touch devices
      accessibility: true,
      setGallerySize: false
    });
    
    // Only add hover behavior on non-touch devices
    if (!('ontouchstart' in window)) {
      // Start autoplay on hover with 2 second interval
      carousel.addEventListener('mouseenter', function() {
        flkty.options.autoPlay = 2000;  // Set autoplay interval
        flkty.playPlayer();
      });
      
      // Stop autoplay when mouse leaves
      carousel.addEventListener('mouseleave', function() {
        flkty.pausePlayer();
        flkty.options.autoPlay = false;  // Disable autoplay
      });
    }
    
    // Handle resize events
    window.addEventListener('resize', function() {
      flkty.resize();
    });
  });
});
</script>
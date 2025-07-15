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
            <div class="swiper gallery-swiper" data-gallery-index="{{ forloop.index }}">
              <div class="swiper-wrapper">
                {% for image in gallery_item.images %}
                  <div class="swiper-slide">
                    <img src="{{ image | absolute_url }}" alt="{{ gallery_item.title }}" />
                  </div>
                {% endfor %}
              </div>
              <div class="swiper-pagination" data-gallery="{{ forloop.index }}"></div>
              <div class="swiper-button-next" data-gallery="{{ forloop.index }}"></div>
              <div class="swiper-button-prev" data-gallery="{{ forloop.index }}"></div>
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

/* Single image styling - match swiper dimensions */
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
    max-width: 100%;
  }
  
  .gallery-swiper {
    height: 250px;
  }
  
  .single-image img {
    height: 250px;
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
  
  .single-image img {
    height: 200px;
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
// More robust loading and initialization
(function() {
  let initAttempts = 0;
  const maxAttempts = 50; // 5 seconds total
  
  function checkAndInit() {
    initAttempts++;
    console.log(`Init attempt ${initAttempts}: Swiper available = ${typeof Swiper !== 'undefined'}, DOM ready = ${document.readyState}`);
    
    // Check if Swiper is loaded and DOM is ready
    if (typeof Swiper !== 'undefined' && document.readyState !== 'loading') {
      console.log('✅ Ready to initialize swipers');
      initializeSwipers();
      return true;
    }
    
    // Keep trying if we haven't exceeded max attempts
    if (initAttempts < maxAttempts) {
      console.log('⏳ Not ready yet, retrying in 100ms...');
      setTimeout(checkAndInit, 100);
    } else {
      console.error('❌ Failed to initialize after', maxAttempts, 'attempts');
    }
    
    return false;
  }

  // Function to initialize swipers
  function initializeSwipers() {
    console.log('🚀 Initializing swipers...');
    
    const swipers = document.querySelectorAll('.gallery-swiper');
    console.log('Found', swipers.length, 'swiper elements');
    
    if (swipers.length === 0) {
      console.log('No swiper elements found, will retry...');
      // Reset attempts and try again
      initAttempts = Math.max(0, initAttempts - 10);
      setTimeout(checkAndInit, 500);
      return;
    }
    
    let successCount = 0;
    
    swipers.forEach(function(swiperEl, index) {
      console.log(`Initializing swiper ${index + 1}...`);
      
      // Skip if already initialized
      if (swiperEl.swiper) {
        console.log(`Swiper ${index + 1} already initialized`);
        successCount++;
        return;
      }
      
      // Check if this swiper has the required structure
      const wrapper = swiperEl.querySelector('.swiper-wrapper');
      const slides = swiperEl.querySelectorAll('.swiper-slide');
      
      if (!wrapper || slides.length === 0) {
        console.warn(`Swiper ${index + 1} missing structure - wrapper: ${!!wrapper}, slides: ${slides.length}`);
        return;
      }
      
      try {
        const galleryIndex = swiperEl.getAttribute('data-gallery-index');
        console.log(`Creating swiper ${index + 1} with gallery index: ${galleryIndex}`);
        
        const swiper = new Swiper(swiperEl, {
          slidesPerView: 1,
          spaceBetween: 0,
          loop: slides.length > 1, // Only loop if more than 1 slide
          speed: 400,
          
          // Autoplay configuration
          autoplay: {
            delay: 2000,
            disableOnInteraction: false,
            pauseOnMouseEnter: true,
          },
          
          // Pagination - use unique selector for this gallery
          pagination: {
            el: `[data-gallery="${galleryIndex}"].swiper-pagination`,
            clickable: true,
            dynamicBullets: true,
          },
          
          // Navigation arrows - use unique selectors for this gallery
          navigation: {
            nextEl: `[data-gallery="${galleryIndex}"].swiper-button-next`,
            prevEl: `[data-gallery="${galleryIndex}"].swiper-button-prev`,
          },
          
          // Touch settings for better mobile experience
          touchRatio: 1,
          touchAngle: 45,
          simulateTouch: true,
          allowTouchMove: true,
          
          // Enable keyboard control
          keyboard: {
            enabled: true,
          },
          
          // Prevent issues
          watchOverflow: true,
          observer: true,
          observeParents: true,
        });
        
        console.log(`✅ Swiper ${index + 1} created successfully - slides: ${swiper.slides.length}`);
        
        // Stop autoplay initially
        swiper.autoplay.stop();
        
        // Add hover autoplay for non-touch devices only
        if (!('ontouchstart' in window)) {
          swiperEl.addEventListener('mouseenter', function() {
            swiper.autoplay.start();
          });
          
          swiperEl.addEventListener('mouseleave', function() {
            swiper.autoplay.stop();
          });
        }
        
        successCount++;
        
      } catch (error) {
        console.error(`❌ Error initializing swiper ${index + 1}:`, error);
      }
    });
    
    console.log(`🎉 Initialization complete: ${successCount}/${swipers.length} swipers created`);
  }

  // Start the initialization process immediately
  checkAndInit();

  // Also try on DOM events as backup
  if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', checkAndInit);
  }
  
  window.addEventListener('load', checkAndInit);
  
  // Final fallback after page fully loads
  setTimeout(function() {
    if (typeof Swiper !== 'undefined') {
      console.log('🔄 Final fallback initialization attempt...');
      initializeSwipers();
    }
  }, 2000);
})();
</script>
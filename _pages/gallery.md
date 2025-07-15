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
          <section class="splide" id="splide-{{ forloop.index }}">
            <div class="splide__track">
              <ul class="splide__list">
                {% for image in gallery_item.images %}
                  <li class="splide__slide">
                    <img src="{{ image | absolute_url }}" alt="{{ gallery_item.title }}" />
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
}

.splide__slide img {
  width: 100%;
  height: auto;
  max-height: 400px;
  object-fit: contain;
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

/* Custom Splide styling */
.splide {
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
}

.splide__pagination {
  bottom: -40px;
}

.splide__pagination__page {
  background-color: #bbb;
  width: 12px;
  height: 12px;
  margin: 0 5px;
  transition: background-color 0.3s ease;
}

.splide__pagination__page:hover {
  background-color: #717171;
}

.splide__pagination__page.is-active {
  background-color: #333;
}

/* Arrow styling */
.splide__arrows {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}

.splide__arrow {
  background-color: rgba(0, 0, 0, 0.5);
  color: white;
  border: none;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.splide__arrow:hover {
  background-color: rgba(0, 0, 0, 0.8);
}

.splide__arrow--prev {
  left: 10px;
}

.splide__arrow--next {
  right: 10px;
}

.splide__arrow svg {
  width: 20px;
  height: 20px;
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
  
  .splide__arrow {
    width: 35px;
    height: 35px;
  }
}
</style>

<!-- Splide JS -->
<script src="https://cdn.jsdelivr.net/npm/@splidejs/splide@4.1.4/dist/js/splide.min.js"></script>

<script>
document.addEventListener('DOMContentLoaded', function () {
  const splideInstances = [];
  
  {% for gallery_item in site.gallery %}
    const splide{{ forloop.index }} = new Splide('#splide-{{ forloop.index }}', {
      type: 'loop',
      autoplay: false,  // Start with autoplay off
      interval: 3000,   // 3 seconds between slides
      arrows: true,
      pagination: true,
      perPage: 1,
      gap: 0,
      pauseOnHover: true,  // Pause when hovering
      pauseOnFocus: true,  // Pause when focused
      breakpoints: {
        768: {
          arrows: true,
        }
      }
    }).mount();
    
    splideInstances.push(splide{{ forloop.index }});
  {% endfor %}
  
  // Intersection Observer to start autoplay when section comes into view
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      const splideElement = entry.target.querySelector('.splide');
      if (splideElement) {
        const splideId = splideElement.id;
        const index = parseInt(splideId.replace('splide-', '')) - 1;
        const splideInstance = splideInstances[index];
        
        if (entry.isIntersecting) {
          // Start autoplay with a 2-second delay when section comes into view
          setTimeout(() => {
            if (splideInstance && splideInstance.Components.Autoplay) {
              splideInstance.Components.Autoplay.play();
            }
          }, 2000);
        } else {
          // Stop autoplay when section leaves view
          if (splideInstance && splideInstance.Components.Autoplay) {
            splideInstance.Components.Autoplay.pause();
          }
        }
      }
    });
  }, {
    threshold: 0.5  // Trigger when 50% of the section is visible
  });
  
  // Observe all gallery sections
  document.querySelectorAll('.gallery-section').forEach((section) => {
    observer.observe(section);
  });
});
</script>
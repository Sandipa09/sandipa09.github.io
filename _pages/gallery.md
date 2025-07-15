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
            <div class="carousel" data-flickity='{ "cellAlign": "left", "contain": true, "autoPlay": false, "pauseAutoPlayOnHover": false }'>
              {% for image in gallery_item.images %}
                <div class="carousel-cell">
                  <img src="{{ image | absolute_url }}" alt="{{ gallery_item.title }}" />
                </div>
              {% endfor %}
            </div>
          {% else %}
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
/* Ensure spacing and responsiveness */
.photo-gallery {
  max-width: 100%;
  padding: 0 1rem;
}

/* Layout */
.gallery-section {
  margin-bottom: 60px;
  border-bottom: 1px solid #eee;
  padding-bottom: 40px;
}

.gallery-content {
  display: flex;
  flex-wrap: wrap;
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

/* Carousel styling */
.carousel-container {
  flex: 1;
  max-width: 500px;
}

.carousel {
  background: #fff;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
}

.carousel-cell {
  width: 100%;
  margin-right: 10px;
  background: #f8f8f8;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.carousel-cell img {
  width: 100%;
  height: auto;
  max-width: 100%;
  object-fit: cover;
  border-radius: 10px;
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
  height: auto;
  max-width: 100%;
  object-fit: cover;
  border-radius: 10px;
}

/* Gallery text */
.gallery-text {
  margin-top: 20px;
  font-size: 1.1em;
  line-height: 1.6;
}

/* Flickity custom */
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

/* Responsive Design */
@media (max-width: 768px) {
  .gallery-section.left .gallery-content,
  .gallery-section.right .gallery-content {
    flex-direction: column;
    gap: 20px;
  }

  .gallery-info,
  .carousel-container {
    width: 100%;
    min-width: unset;
  }

  .carousel-cell,
  .single-image img {
    height: auto;
  }

  .flickity-prev-next-button {
    width: 35px;
    height: 35px;
  }

  .flickity-page-dots {
    bottom: -25px;
  }

  .flickity-page-dots .dot {
    width: 10px;
    height: 10px;
  }
}

@media (max-width: 480px) {
  .gallery-content {
    gap: 15px;
  }

  .gallery-text {
    font-size: 1em;
  }
}
</style>

<!-- Flickity JS -->
<script src="https://unpkg.com/flickity@2/dist/flickity.pkgd.min.js"></script>
<script>
document.addEventListener('DOMContentLoaded', function() {
  const carousels = document.querySelectorAll('.carousel');
  carousels.forEach(function(carousel) {
    const flkty = new Flickity(carousel, {
      cellAlign: 'left',
      contain: true,
      autoPlay: false,
      pauseAutoPlayOnHover: false
    });

    // Add hover autoplay for desktop
    if (window.innerWidth > 768) {
      carousel.addEventListener('mouseenter', function() {
        flkty.options.autoPlay = 2000;
        flkty.playPlayer();
      });

      carousel.addEventListener('mouseleave', function() {
        flkty.pausePlayer();
        flkty.options.autoPlay = false;
      });
    }
  });
});
</script>

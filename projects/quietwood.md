---
layout: default
title: Quietwood, NH
permalink: /projects/quietwood
sections:
  - slug: screenshots
    title: Screenshots
    description: In-game views and atmospheric scenes.
  - slug: development
    title: Development Images
    description: Roblox Studio work, asset modeling, and building progress.
# Add custom captions here matching the image filename:
captions:
  # Screenshots
  parkandofficechair.png: "park around the market district. someone felt like taking an outdoor office to the next level"

  # Development Images
  evilquietwood.png: "was trying to make fake postcards for the art museum by changing the lighting. accidentally brought quietwood into the fourth circle"
  fakenightlighting.png: "after a finished a building, i tried making a 'render' with fake lighting. my friend hated it"
  justagamequietwoodcomparison.png: "size comparison of quietwood's current size to another game we never finished. next two photos are also based on these two maps fused together"
  justaquietwood-thewall.png: "unfinished suburban house next to a monolithic wall my friend made circa 2020"
  justaquietwood.png: "Place, Japan"
  lightingbug-quietwood.gif: "a relic from when i was trying to debug why the lights wouldn't work properly. turns out our day/night cycle wasn't made with the input delay in mind"
  lightingworking-qtwd.mp4: "the glorious moment when i finally got lighting working. unfortunately, the clouds didn't change color in this version, but they do now!"
  oldclocktower.png: "the older clock tower. both variations were made by my friend, but the first one was extremely misaligned and a real pain to make interiors for"
  quietwoodnoeffects.png: "another image from when i was trying to change the lighting. turns out removing all of it make the place look really wrong. if you thought our lighting work in the game was minimal, think again"
  rangelightingbug-quietwood.gif: "one of my first tries to debug the lighting system. thank goodness there was a way better solution than if statements with ranges"
  
---
{% assign quietwood_images = site.static_files | where_exp: "file", "file.path contains 'assets/images/quietwood/'" %}
{% assign image_files = "" | split: "," %}
{% for file in quietwood_images %}
  {% assign ext = file.extname | downcase %}
  {% if ext == '.jpg' or ext == '.jpeg' or ext == '.png' or ext == '.gif' or ext == '.webp' or ext == '.svg' or ext == '.mp4' %}
    {% assign image_files = image_files | push: file %}
  {% endif %}
{% endfor %}
{% assign image_files = image_files | sort: "path" %}

<style>
.quietwood-intro {
  max-width: 800px;
  margin: 0 auto 2rem;
  text-align: center;
}

.quietwood-section {
  margin-bottom: 3rem;
}

.quietwood-section h2 {
  text-align: center;
  margin-bottom: 0.5rem;
}

.quietwood-section p {
  max-width: 700px;
  margin: 0.5rem auto 1.5rem;
  text-align: center;
}

.gallery-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1.5rem;
}

.gallery-thumb {
  display: block;
  border: 1px solid #333333;
  overflow: hidden;
  box-shadow: 0 8px 20px rgba(0,0,0,0.25);
  transition: transform 0.2s ease, box-shadow 0.2s ease, border-color 0.2s ease;
  cursor: zoom-in;
}

.gallery-thumb:hover {
  transform: translateY(-4px);
  border-color: #38bdf8;
  box-shadow: 0 12px 24px rgba(0,0,0,0.35);
}

.gallery-thumb img,
.gallery-thumb video {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.gallery-empty {
  text-align: center;
  color: #888888;
  padding: 2rem;
  border: 1px dashed #333333;
  background-color: #0a0a0a;
}

.gallery-empty code {
  color: #38bdf8;
  background-color: #1a1a1a;
  padding: 2px 6px;
}

.lightbox {
  display: none;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.85);
  align-items: center;
  justify-content: center;
  padding: 2rem;
  box-sizing: border-box;
  z-index: 9999;
  cursor: zoom-out;
}

.lightbox:target {
  display: flex;
}

.lightbox__content {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: fit-content;
  max-width: 90vw;
  max-height: 90vh;
  cursor: default;
}

.lightbox img,
.lightbox video {
  max-width: 90vw;
  max-height: 80vh;
  box-shadow: 0 16px 40px rgba(0,0,0,0.45);
  display: block;
}

.lightbox__caption {
  margin: 10px 0 0 0;
  font-size: 0.85rem;
  color: #cccccc;
  line-height: 1.4;
  font-family: monospace, monospace;
  text-align: center;
}

.lightbox__close {
  position: absolute;
  top: 1.5rem;
  right: 1.5rem;
  color: #fff;
  font-size: 2rem;
  text-decoration: none;
}

@media (max-width: 640px) {
  .gallery-grid {
    gap: 1rem;
  }
}
</style>

# Quietwood, NH
<div class="quietwood-intro">
  <p>Passion project / build started co-created by a friend and I. Essentially a ground-up reimagining of an early roleplay game we made, this time centered in a New England river valley. Heavy inspiration from small town America and specific towns like Cambridge and Burlington.</p>
</div>

{% for section in page.sections %}
  {% assign section_path = '/assets/images/quietwood/' | append: section.slug | append: '/' %}
  {% assign section_images = image_files | where_exp: "file", "file.path contains section_path" %}
  {% assign section_id = section.slug | slugify: 'pretty' %}
  <section class="quietwood-section" id="{{ section_id }}">
    <h2>{{ section.title }}</h2>
    {% if section.description %}
      <p>{{ section.description }}</p>
    {% endif %}

    {% if section_images.size > 0 %}
      <div class="gallery-grid">
        {% for image in section_images %}
          {% assign image_index = forloop.index0 | plus: 1 %}
          {% assign lightbox_id = section_id | append: '-' | append: image_index %}
          {% assign alt_text = image.basename | replace: '-', ' ' | replace: '_', ' ' | capitalize %}
          {% assign ext = image.extname | downcase %}
          <a class="gallery-thumb" href="#{{ lightbox_id }}">
            {% if ext == '.mp4' %}
              <video src="{{ image.path | relative_url }}" autoplay loop muted playsinline></video>
            {% else %}
              <img src="{{ image.path | relative_url }}" alt="{{ alt_text }}">
            {% endif %}
          </a>
          {% assign caption = page.captions[image.name] | default: page.captions[image.basename] | default: "Sample" %}
          <div class="lightbox" id="{{ lightbox_id }}">
            <a class="lightbox__close" href="#gallery-close" aria-label="Close">&times;</a>
            <div class="lightbox__content">
              {% if ext == '.mp4' %}
                <video src="{{ image.path | relative_url }}" autoplay loop muted playsinline></video>
              {% else %}
                <img src="{{ image.path | relative_url }}" alt="{{ alt_text }}">
              {% endif %}
              <p class="lightbox__caption">{{ caption }}</p>
            </div>
          </div>
        {% endfor %}
      </div>
    {% else %}
      <p class="gallery-empty">Add images to <code>assets/images/quietwood/{{ section.slug }}/</code> to populate this section.</p>
    {% endif %}
  </section>
{% endfor %}

<div id="gallery-close"></div>

<script>
document.addEventListener('DOMContentLoaded', function () {
  const lightboxes = document.querySelectorAll('.lightbox');
  lightboxes.forEach(function (lightbox) {
    lightbox.addEventListener('click', function (event) {
      if (event.target === lightbox) {
        window.location.hash = '#gallery-close';
      }
    });
  });

  document.addEventListener('keydown', function (event) {
    if (event.key === 'Escape') {
      const activeLightbox = document.querySelector('.lightbox:target');
      if (activeLightbox) {
        event.preventDefault();
        window.location.hash = '#gallery-close';
      }
    }
  });
});
</script>


---
layout: page
title: Scroll Story
permalink: /scroll-story/
---

<div id="scroll-story-container">
  <section id="story-intro" class="story-section">
    <div class="story-content fade-in">
      <h1>A Life in Posts</h1>
      <p class="story-subtitle">Journey through Samuel R. Delany's curated moments</p>
      <div class="scroll-indicator">
        <span>↓ Scroll to explore ↓</span>
      </div>
    </div>
  </section>

  {% assign sorted_items = site.sf | sort: '_date' %}
  {% assign decades = "1940s,1950s,1960s,1970s,2010s" | split: "," %}

  {% for decade in decades %}
    {% assign decade_year = decade | slice: 0, 3 | append: '0' %}
    {% assign decade_start = decade_year %}
    {% assign decade_end_num = decade_year | plus: 10 %}
    {% assign decade_end = decade_end_num | append: '' %}
    {% assign decade_items = '' | split: '' %}
    {% for item in sorted_items %}
      {% if item._date >= decade_start and item._date < decade_end %}
        {% assign decade_items = decade_items | push: item %}
      {% endif %}
    {% endfor %}

    {% if decade_items.size > 0 %}
    <section class="decade-section story-section" data-decade="{{ decade }}">
      <div class="decade-intro parallax-bg">
        <h2 class="decade-title">{{ decade }}</h2>
      </div>

      {% for item in decade_items %}
      <div class="story-item" data-pid="{{ item.pid }}">
        <div class="story-item-inner">
          <div class="story-item-media parallax-media">
            <div class="media-wrapper">
              <img src="{{ item.full | relative_url }}" alt="{{ item.label }}" class="story-image">
              <div class="media-overlay">
                <span class="item-date">{{ item._date }}</span>
              </div>
            </div>
          </div>

          <div class="story-item-text fade-up">
            <h3>{{ item.label }}</h3>
            <p class="item-subject">{{ item.subject }}</p>

            {% if item.writing and item.writing != '' %}
            <div class="item-writing">
              {% assign words = item.writing | split: " " %}
              {% for word in words %}
                <span class="word-reveal" style="--delay: {{ forloop.index }};">{{ word }}</span>
              {% endfor %}
            </div>
            {% endif %}

            <a href="{{ item.url | relative_url }}" class="story-link">Explore this moment →</a>
          </div>
        </div>
      </div>
      {% endfor %}
    </section>
    {% endif %}
  {% endfor %}

  <section id="story-outro" class="story-section">
    <div class="story-content fade-in">
      <h2>Continue Exploring</h2>
      <div class="outro-links">
        <a href="{{ '/collection/' | relative_url }}" class="outro-link">Full Collection</a>
        <a href="{{ '/timeline/' | relative_url }}" class="outro-link">Timeline View</a>
        <a href="{{ '/network/' | relative_url }}" class="outro-link">Network Graph</a>
      </div>
    </div>
  </section>
</div>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#scroll-story-container {
  width: 100%;
  background: #000;
  color: #fff;
  overflow-x: hidden;
}

.story-section {
  min-height: 100vh;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 4rem 2rem;
}

/* Intro Section */
#story-intro {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  text-align: center;
}

#story-intro h1 {
  font-size: 5rem;
  font-weight: 900;
  margin-bottom: 1rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
}

.story-subtitle {
  font-size: 1.5rem;
  opacity: 0.9;
  margin-bottom: 3rem;
}

.scroll-indicator {
  font-size: 1.2rem;
  animation: bounce 2s infinite;
}

@keyframes bounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(20px); }
}

/* Decade Sections */
.decade-section {
  flex-direction: column;
  padding: 0;
  background: #000;
}

.decade-intro {
  width: 100%;
  min-height: 50vh;
  display: flex;
  align-items: center;
  justify-content: center;
  position: sticky;
  top: 0;
  z-index: 1;
}

.decade-title {
  font-size: 8rem;
  font-weight: 900;
  text-transform: uppercase;
  letter-spacing: 0.2em;
  background: linear-gradient(45deg, #667eea, #764ba2, #f093fb);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  opacity: 0.2;
}

/* Story Items */
.story-item {
  width: 100%;
  min-height: 100vh;
  position: relative;
  z-index: 2;
}

.story-item-inner {
  max-width: 1400px;
  margin: 0 auto;
  padding: 4rem 2rem;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}

.story-item:nth-child(even) .story-item-inner {
  grid-template-columns: 1fr 1fr;
}

.story-item:nth-child(odd) .story-item-inner {
  grid-template-columns: 1fr 1fr;
  direction: rtl;
}

.story-item:nth-child(odd) .story-item-text {
  direction: ltr;
}

.story-item-media {
  position: relative;
  transform-style: preserve-3d;
}

.media-wrapper {
  position: relative;
  overflow: hidden;
  border: 3px solid #fff;
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.5);
  transform: translateZ(0);
}

.story-image {
  width: 100%;
  height: auto;
  display: block;
  transition: transform 0.5s ease;
}

.story-item:hover .story-image {
  transform: scale(1.05);
}

.media-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  padding: 1rem;
  background: linear-gradient(to bottom, rgba(0,0,0,0.8), transparent);
}

.item-date {
  font-family: monospace;
  font-size: 1.5rem;
  font-weight: bold;
  color: #fff;
  text-shadow: 2px 2px 4px rgba(0,0,0,0.5);
}

.story-item-text {
  padding: 2rem;
}

.story-item-text h3 {
  font-size: 2.5rem;
  margin-bottom: 1rem;
  color: #667eea;
  line-height: 1.2;
}

.item-subject {
  font-size: 1.2rem;
  font-style: italic;
  color: #999;
  margin-bottom: 2rem;
}

.item-writing {
  font-size: 1.1rem;
  line-height: 2;
  margin-bottom: 2rem;
  color: #ddd;
}

.word-reveal {
  display: inline-block;
  opacity: 0;
  transform: translateY(20px);
  animation: reveal 0.5s ease forwards;
  animation-delay: calc(var(--delay) * 0.02s);
}

@keyframes reveal {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.story-link {
  display: inline-block;
  padding: 1rem 2rem;
  background: transparent;
  border: 2px solid #667eea;
  color: #667eea;
  text-decoration: none;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  transition: all 0.3s ease;
}

.story-link:hover {
  background: #667eea;
  color: #000;
  transform: translateX(10px);
}

/* Outro Section */
#story-outro {
  background: linear-gradient(135deg, #764ba2 0%, #667eea 100%);
  text-align: center;
}

#story-outro h2 {
  font-size: 3rem;
  margin-bottom: 3rem;
}

.outro-links {
  display: flex;
  gap: 2rem;
  justify-content: center;
  flex-wrap: wrap;
}

.outro-link {
  display: inline-block;
  padding: 1.5rem 3rem;
  background: #fff;
  color: #667eea;
  text-decoration: none;
  font-weight: bold;
  font-size: 1.2rem;
  border-radius: 50px;
  transition: all 0.3s ease;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

.outro-link:hover {
  transform: translateY(-5px);
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.5);
  background: #000;
  color: #fff;
}

/* Scroll Animations */
.fade-in {
  opacity: 0;
  transform: translateY(50px);
  transition: all 1s ease;
}

.fade-in.visible {
  opacity: 1;
  transform: translateY(0);
}

.fade-up {
  opacity: 0;
  transform: translateY(100px);
  transition: all 0.8s ease;
}

.fade-up.visible {
  opacity: 1;
  transform: translateY(0);
}

.parallax-bg {
  transition: transform 0.5s ease-out;
}

.parallax-media {
  transition: transform 0.3s ease-out;
}

/* Responsive */
@media (max-width: 1024px) {
  .story-item-inner {
    grid-template-columns: 1fr !important;
    direction: ltr !important;
    gap: 2rem;
  }

  .decade-title {
    font-size: 4rem;
  }

  #story-intro h1 {
    font-size: 3rem;
  }

  .story-item-text h3 {
    font-size: 2rem;
  }
}

@media (max-width: 768px) {
  .decade-title {
    font-size: 3rem;
  }

  #story-intro h1 {
    font-size: 2rem;
  }

  .story-item-text h3 {
    font-size: 1.5rem;
  }

  .item-writing {
    font-size: 1rem;
  }
}
</style>

<script>
document.addEventListener('DOMContentLoaded', function() {
  // Intersection Observer for scroll animations
  const observerOptions = {
    threshold: 0.2,
    rootMargin: '0px 0px -100px 0px'
  };

  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible');
      }
    });
  }, observerOptions);

  // Observe all animated elements
  document.querySelectorAll('.fade-in, .fade-up').forEach(el => {
    observer.observe(el);
  });

  // Parallax effects on scroll
  let ticking = false;

  function updateParallax() {
    const scrolled = window.pageYOffset;

    // Parallax backgrounds
    document.querySelectorAll('.parallax-bg').forEach(el => {
      const rect = el.getBoundingClientRect();
      const elementTop = rect.top + scrolled;
      const elementHeight = rect.height;
      const viewportHeight = window.innerHeight;

      if (rect.top < viewportHeight && rect.bottom > 0) {
        const scrollPercent = (scrolled - elementTop + viewportHeight) / (viewportHeight + elementHeight);
        const parallaxAmount = (scrollPercent - 0.5) * 100;
        el.style.transform = `translateY(${parallaxAmount}px)`;
      }
    });

    // Parallax media
    document.querySelectorAll('.parallax-media').forEach(el => {
      const rect = el.getBoundingClientRect();
      if (rect.top < window.innerHeight && rect.bottom > 0) {
        const centerY = rect.top + rect.height / 2;
        const distanceFromCenter = (window.innerHeight / 2 - centerY) / window.innerHeight;
        const parallaxAmount = distanceFromCenter * 50;
        el.style.transform = `translateY(${parallaxAmount}px) scale(${1 + Math.abs(distanceFromCenter) * 0.1})`;
      }
    });

    ticking = false;
  }

  function requestTick() {
    if (!ticking) {
      window.requestAnimationFrame(updateParallax);
      ticking = true;
    }
  }

  window.addEventListener('scroll', requestTick);

  // Initial update
  updateParallax();

  // Reveal words in writing sections when they come into view
  const wordObserver = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        const words = entry.target.querySelectorAll('.word-reveal');
        words.forEach(word => {
          word.style.animation = 'reveal 0.5s ease forwards';
        });
        wordObserver.unobserve(entry.target);
      }
    });
  }, { threshold: 0.3 });

  document.querySelectorAll('.item-writing').forEach(el => {
    wordObserver.observe(el);
  });
});
</script>

---
layout: page
title: Explore
permalink: /explore/
---

<div id="explore-container">
  <section class="explore-hero">
    <h1>Speculative Reimaginings</h1>
    <p class="hero-subtitle">Multiple ways to experience Samuel R. Delany's curated posts</p>
  </section>

  <section class="explore-grid">
    <a href="{{ '/timeline/' | relative_url }}" class="explore-card card-timeline">
      <div class="card-inner">
        <div class="card-icon">📅</div>
        <h2>Timeline</h2>
        <p>Journey through seven decades of posts, photographs, and commentary arranged chronologically with interactive filters</p>
        <span class="card-cta">Explore Timeline →</span>
      </div>
      <div class="card-bg"></div>
    </a>

    <a href="{{ '/browse/' | relative_url }}" class="explore-card card-browse">
      <div class="card-inner">
        <div class="card-icon">🔍</div>
        <h2>Reimagined Browse</h2>
        <p>Switch between grid, list, text-only, and image-only views. Filter by type, era, and content with live statistics</p>
        <span class="card-cta">Start Browsing →</span>
      </div>
      <div class="card-bg"></div>
    </a>

    <a href="{{ '/network/' | relative_url }}" class="explore-card card-network">
      <div class="card-inner">
        <div class="card-icon">🕸️</div>
        <h2>Network of Ideas</h2>
        <p>Interactive force-directed graph showing temporal and thematic connections between posts</p>
        <span class="card-cta">View Network →</span>
      </div>
      <div class="card-bg"></div>
    </a>

    <a href="{{ '/typography/' | relative_url }}" class="explore-card card-typography">
      <div class="card-inner">
        <div class="card-icon">✍️</div>
        <h2>Typography Experiments</h2>
        <p>Delany's words presented through five experimental typographic styles: kinetic, concrete poetry, spectacle, drift, and layers</p>
        <span class="card-cta">Experiment →</span>
      </div>
      <div class="card-bg"></div>
    </a>

    <a href="{{ '/scroll-story/' | relative_url }}" class="explore-card card-scroll">
      <div class="card-inner">
        <div class="card-icon">📜</div>
        <h2>Scroll Story</h2>
        <p>A narrative journey with parallax effects, word-by-word reveals, and scroll-triggered animations</p>
        <span class="card-cta">Begin Journey →</span>
      </div>
      <div class="card-bg"></div>
    </a>

    <a href="{{ '/themes/' | relative_url }}" class="explore-card card-themes">
      <div class="card-inner">
        <div class="card-icon">💡</div>
        <h2>Thematic Analysis</h2>
        <p>Deep dive into recurring themes, temporal patterns, word clouds, and conceptual connections</p>
        <span class="card-cta">Analyze Themes →</span>
      </div>
      <div class="card-bg"></div>
    </a>
  </section>

  <section class="explore-classic">
    <h2>Classic Views</h2>
    <div class="classic-links">
      <a href="{{ '/collection/' | relative_url }}" class="classic-link">
        <span>📚</span>
        <span>Full Collection</span>
      </a>
      <a href="{{ '/search/' | relative_url }}" class="classic-link">
        <span>🔍</span>
        <span>Search</span>
      </a>
      <a href="{{ '/exhibits/a/' | relative_url }}" class="classic-link">
        <span>🖼️</span>
        <span>Exhibits</span>
      </a>
    </div>
  </section>
</div>

<style>
#explore-container {
  max-width: 1600px;
  margin: 0 auto;
  padding: 2rem;
  background: #0a0a0a;
  min-height: 100vh;
}

.explore-hero {
  text-align: center;
  padding: 5rem 2rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  margin: -2rem -2rem 4rem;
  color: white;
  position: relative;
  overflow: hidden;
}

.explore-hero::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: repeating-linear-gradient(
    45deg,
    transparent,
    transparent 10px,
    rgba(255,255,255,0.05) 10px,
    rgba(255,255,255,0.05) 20px
  );
  animation: slide 20s linear infinite;
}

@keyframes slide {
  0% { transform: translate(0, 0); }
  100% { transform: translate(50px, 50px); }
}

.explore-hero h1 {
  font-size: 4rem;
  font-weight: 900;
  margin-bottom: 1rem;
  position: relative;
  z-index: 1;
  text-transform: uppercase;
  letter-spacing: 0.1em;
}

.hero-subtitle {
  font-size: 1.5rem;
  opacity: 0.9;
  position: relative;
  z-index: 1;
}

.explore-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: 2rem;
  margin-bottom: 4rem;
}

.explore-card {
  position: relative;
  height: 350px;
  overflow: hidden;
  text-decoration: none;
  color: white;
  border-radius: 12px;
  transition: all 0.5s ease;
  border: 3px solid transparent;
}

.explore-card:hover {
  transform: translateY(-10px) scale(1.02);
  border-color: white;
  box-shadow: 0 20px 60px rgba(0,0,0,0.5);
}

.card-inner {
  position: relative;
  z-index: 2;
  padding: 3rem;
  height: 100%;
  display: flex;
  flex-direction: column;
  background: rgba(0, 0, 0, 0.4);
  transition: background 0.3s ease;
}

.explore-card:hover .card-inner {
  background: rgba(0, 0, 0, 0.6);
}

.card-bg {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 1;
  transition: transform 0.5s ease;
}

.explore-card:hover .card-bg {
  transform: scale(1.1);
}

.card-timeline .card-bg {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}

.card-browse .card-bg {
  background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
}

.card-network .card-bg {
  background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
}

.card-typography .card-bg {
  background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%);
}

.card-scroll .card-bg {
  background: linear-gradient(135deg, #fa709a 0%, #fee140 100%);
}

.card-themes .card-bg {
  background: linear-gradient(135deg, #30cfd0 0%, #330867 100%);
}

.card-icon {
  font-size: 4rem;
  margin-bottom: 1rem;
  filter: drop-shadow(2px 2px 4px rgba(0,0,0,0.3));
}

.explore-card h2 {
  font-size: 2rem;
  margin-bottom: 1rem;
  font-weight: 900;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.explore-card p {
  font-size: 1.1rem;
  line-height: 1.6;
  margin-bottom: 2rem;
  flex-grow: 1;
  opacity: 0.95;
}

.card-cta {
  font-size: 1.1rem;
  font-weight: bold;
  opacity: 0.9;
  transition: transform 0.3s ease;
  display: inline-block;
}

.explore-card:hover .card-cta {
  transform: translateX(10px);
  opacity: 1;
}

.explore-classic {
  text-align: center;
  padding: 3rem 2rem;
  background: #1a1a1a;
  border-radius: 12px;
  border: 2px solid #333;
}

.explore-classic h2 {
  font-size: 2.5rem;
  margin-bottom: 2rem;
  color: #667eea;
}

.classic-links {
  display: flex;
  justify-content: center;
  gap: 2rem;
  flex-wrap: wrap;
}

.classic-link {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  padding: 2rem;
  background: #2a2a2a;
  border: 2px solid #444;
  border-radius: 8px;
  text-decoration: none;
  color: white;
  min-width: 150px;
  transition: all 0.3s ease;
}

.classic-link:hover {
  border-color: #667eea;
  background: #333;
  transform: translateY(-5px);
}

.classic-link span:first-child {
  font-size: 3rem;
}

.classic-link span:last-child {
  font-size: 1.1rem;
  font-weight: bold;
}

@media (max-width: 1024px) {
  .explore-hero h1 {
    font-size: 2.5rem;
  }

  .hero-subtitle {
    font-size: 1.2rem;
  }

  .explore-grid {
    grid-template-columns: 1fr;
  }

  .explore-card {
    height: 300px;
  }

  .card-inner {
    padding: 2rem;
  }

  .explore-card h2 {
    font-size: 1.5rem;
  }

  .explore-card p {
    font-size: 1rem;
  }
}

@media (max-width: 768px) {
  .explore-hero h1 {
    font-size: 2rem;
  }

  .classic-links {
    flex-direction: column;
    align-items: stretch;
  }
}
</style>

<script>
document.addEventListener('DOMContentLoaded', function() {
  // Add hover effects and animations
  const cards = document.querySelectorAll('.explore-card');

  cards.forEach(card => {
    card.addEventListener('mouseenter', function() {
      this.style.zIndex = '10';
    });

    card.addEventListener('mouseleave', function() {
      this.style.zIndex = '1';
    });
  });

  // Add parallax effect on scroll
  let ticking = false;

  function updateParallax() {
    const scrolled = window.pageYOffset;

    cards.forEach((card, index) => {
      const speed = 0.5 + (index * 0.1);
      const yPos = -(scrolled * speed * 0.01);
      const bg = card.querySelector('.card-bg');
      if (bg) {
        bg.style.transform = `translateY(${yPos}px) scale(1)`;
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
});
</script>

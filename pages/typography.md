---
layout: page
title: Typography Experiments
permalink: /typography/
---

<div id="typo-container">
  <div id="typo-header">
    <h1>Reimagining Text</h1>
    <p>Samuel R. Delany's words presented through experimental typography</p>
  </div>

  <div id="typo-controls">
    <button class="typo-style-btn active" data-style="kinetic">Kinetic</button>
    <button class="typo-style-btn" data-style="concrete">Concrete Poetry</button>
    <button class="typo-style-btn" data-style="spectacle">Spectacle</button>
    <button class="typo-style-btn" data-style="drift">Drift</button>
    <button class="typo-style-btn" data-style="layers">Layers</button>
  </div>

  <div id="typo-posts">
    {% for item in site.sf %}
      {% if item.writing and item.writing != '' %}
      <article class="typo-post" data-pid="{{ item.pid }}">
        <div class="typo-post-header">
          <span class="typo-date">{{ item._date }}</span>
          <h2 class="typo-title">{{ item.label }}</h2>
          <p class="typo-subject">{{ item.subject }}</p>
        </div>

        <div class="typo-content kinetic-style">
          {% assign sentences = item.writing | split: ". " %}
          {% for sentence in sentences %}
            <p class="typo-sentence" data-index="{{ forloop.index }}">{{ sentence }}.</p>
          {% endfor %}
        </div>

        <div class="typo-content concrete-style" style="display: none;">
          {% assign words = item.writing | split: " " %}
          <div class="concrete-canvas">
            {% for word in words %}
              <span class="concrete-word" data-length="{{ word.size }}">{{ word }}</span>
            {% endfor %}
          </div>
        </div>

        <div class="typo-content spectacle-style" style="display: none;">
          <div class="spectacle-text">{{ item.writing }}</div>
          <div class="spectacle-overlay"></div>
        </div>

        <div class="typo-content drift-style" style="display: none;">
          {% assign words = item.writing | split: " " %}
          {% for word in words %}
            <span class="drift-word">{{ word }}</span>
          {% endfor %}
        </div>

        <div class="typo-content layers-style" style="display: none;">
          <div class="layer layer-1">{{ item.writing }}</div>
          <div class="layer layer-2">{{ item.writing }}</div>
          <div class="layer layer-3">{{ item.writing }}</div>
        </div>

        <div class="typo-footer">
          <a href="{{ item.url | relative_url }}" class="typo-link">View Original →</a>
        </div>
      </article>
      {% endif %}
    {% endfor %}
  </div>
</div>

<style>
#typo-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
  background: #000;
  color: #fff;
  min-height: 100vh;
}

#typo-header {
  text-align: center;
  padding: 4rem 2rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  margin: -2rem -2rem 3rem;
  position: relative;
  overflow: hidden;
}

#typo-header::before {
  content: '';
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: repeating-linear-gradient(
    45deg,
    transparent,
    transparent 10px,
    rgba(255,255,255,0.03) 10px,
    rgba(255,255,255,0.03) 20px
  );
  animation: slide 20s linear infinite;
}

@keyframes slide {
  0% { transform: translate(0, 0); }
  100% { transform: translate(50px, 50px); }
}

#typo-header h1 {
  font-size: 4rem;
  margin: 0 0 1rem;
  position: relative;
  z-index: 1;
  font-weight: 900;
  text-transform: uppercase;
  letter-spacing: 0.1em;
}

#typo-header p {
  font-size: 1.3rem;
  position: relative;
  z-index: 1;
  opacity: 0.9;
}

#typo-controls {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 3rem;
  flex-wrap: wrap;
  position: sticky;
  top: 0;
  background: #000;
  padding: 1rem 0;
  z-index: 100;
  border-bottom: 2px solid #667eea;
}

.typo-style-btn {
  background: #1a1a1a;
  color: #fff;
  border: 2px solid #667eea;
  padding: 0.75rem 1.5rem;
  cursor: pointer;
  font-size: 1rem;
  font-weight: bold;
  transition: all 0.3s ease;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.typo-style-btn:hover {
  background: #667eea;
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(102, 126, 234, 0.4);
}

.typo-style-btn.active {
  background: #667eea;
  box-shadow: 0 0 20px rgba(102, 126, 234, 0.6);
}

.typo-post {
  margin-bottom: 6rem;
  padding: 3rem;
  background: #1a1a1a;
  border: 2px solid #333;
  position: relative;
}

.typo-post::before {
  content: '';
  position: absolute;
  top: -2px;
  left: -2px;
  right: -2px;
  bottom: -2px;
  background: linear-gradient(45deg, #667eea, #764ba2, #f093fb, #4facfe);
  z-index: -1;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.typo-post:hover::before {
  opacity: 0.3;
}

.typo-post-header {
  margin-bottom: 2rem;
  padding-bottom: 1rem;
  border-bottom: 2px solid #333;
}

.typo-date {
  display: inline-block;
  background: #667eea;
  color: #fff;
  padding: 0.25rem 0.75rem;
  font-family: monospace;
  font-size: 0.9rem;
  font-weight: bold;
}

.typo-title {
  margin: 1rem 0 0.5rem;
  font-size: 2rem;
  color: #667eea;
}

.typo-subject {
  font-style: italic;
  color: #999;
  margin: 0;
}

.typo-content {
  min-height: 300px;
  padding: 2rem 0;
}

/* KINETIC STYLE - Words move and scale */
.kinetic-style .typo-sentence {
  font-size: 1.2rem;
  line-height: 2;
  margin: 1rem 0;
  animation: kinetic-float 3s ease-in-out infinite;
  animation-delay: calc(var(--index) * 0.2s);
}

.kinetic-style .typo-sentence:nth-child(odd) {
  animation-name: kinetic-float-alt;
}

@keyframes kinetic-float {
  0%, 100% { transform: translateY(0) scale(1); }
  50% { transform: translateY(-10px) scale(1.02); }
}

@keyframes kinetic-float-alt {
  0%, 100% { transform: translateX(0) scale(1); }
  50% { transform: translateX(10px) scale(1.02); }
}

/* CONCRETE POETRY STYLE - Words as visual shapes */
.concrete-canvas {
  position: relative;
  min-height: 500px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  gap: 0.5rem;
}

.concrete-word {
  display: inline-block;
  font-size: calc(0.8rem + var(--length) * 0.1rem);
  color: rgba(255, 255, 255, 0.8);
  transform: rotate(calc(var(--length) * 5deg));
  transition: all 0.3s ease;
  cursor: pointer;
}

.concrete-word:hover {
  color: #667eea;
  transform: rotate(0deg) scale(1.5);
  z-index: 10;
}

/* SPECTACLE STYLE - Inspired by Debord */
.spectacle-text {
  font-size: 1.5rem;
  line-height: 2;
  text-align: justify;
  position: relative;
  z-index: 1;
  mix-blend-mode: difference;
  color: #fff;
}

.spectacle-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(
    45deg,
    transparent 25%,
    rgba(102, 126, 234, 0.1) 25%,
    rgba(102, 126, 234, 0.1) 50%,
    transparent 50%,
    transparent 75%,
    rgba(102, 126, 234, 0.1) 75%
  );
  background-size: 20px 20px;
  animation: spectacle-scan 10s linear infinite;
  pointer-events: none;
}

@keyframes spectacle-scan {
  0% { transform: translateX(-100%); }
  100% { transform: translateX(100%); }
}

/* DRIFT STYLE - Words drift across screen */
.drift-style {
  position: relative;
  overflow: hidden;
  min-height: 600px;
}

.drift-word {
  position: absolute;
  font-size: 1.2rem;
  animation: drift 20s linear infinite;
  animation-delay: calc(var(--index, 0) * -0.5s);
  white-space: nowrap;
  opacity: 0.7;
}

.drift-word:hover {
  animation-play-state: paused;
  opacity: 1;
  color: #667eea;
  font-size: 1.5rem;
}

@keyframes drift {
  0% {
    transform: translate(100vw, calc(var(--index, 0) * 50px));
  }
  100% {
    transform: translate(-100vw, calc(var(--index, 0) * 50px));
  }
}

/* LAYERS STYLE - Overlapping text layers */
.layers-style {
  position: relative;
  min-height: 400px;
}

.layer {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  font-size: 1.1rem;
  line-height: 1.8;
  opacity: 0.4;
  mix-blend-mode: screen;
}

.layer-1 {
  color: #667eea;
  transform: translate(-3px, -3px);
  animation: layer-shift-1 5s ease-in-out infinite;
}

.layer-2 {
  color: #f093fb;
  transform: translate(0, 0);
  animation: layer-shift-2 5s ease-in-out infinite;
}

.layer-3 {
  color: #4facfe;
  transform: translate(3px, 3px);
  animation: layer-shift-3 5s ease-in-out infinite;
}

@keyframes layer-shift-1 {
  0%, 100% { transform: translate(-3px, -3px); }
  50% { transform: translate(-6px, 3px); }
}

@keyframes layer-shift-2 {
  0%, 100% { transform: translate(0, 0); }
  50% { transform: translate(3px, -3px); }
}

@keyframes layer-shift-3 {
  0%, 100% { transform: translate(3px, 3px); }
  50% { transform: translate(-3px, 6px); }
}

.layers-style:hover .layer {
  animation-play-state: paused;
  opacity: 0.7;
}

.typo-footer {
  margin-top: 2rem;
  padding-top: 1rem;
  border-top: 1px solid #333;
  text-align: center;
}

.typo-link {
  display: inline-block;
  color: #667eea;
  text-decoration: none;
  padding: 0.75rem 1.5rem;
  border: 2px solid #667eea;
  transition: all 0.3s ease;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  font-weight: bold;
}

.typo-link:hover {
  background: #667eea;
  color: #000;
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(102, 126, 234, 0.4);
}

@media (max-width: 768px) {
  #typo-header h1 {
    font-size: 2.5rem;
  }

  .typo-post {
    padding: 1.5rem;
  }

  .drift-style {
    min-height: 400px;
  }
}
</style>

<script>
document.addEventListener('DOMContentLoaded', function() {
  const styleButtons = document.querySelectorAll('.typo-style-btn');
  const posts = document.querySelectorAll('.typo-post');

  // Initialize drift style word positions
  posts.forEach(post => {
    const driftStyle = post.querySelector('.drift-style');
    if (driftStyle) {
      const words = driftStyle.querySelectorAll('.drift-word');
      words.forEach((word, index) => {
        word.style.setProperty('--index', index);
        word.style.top = Math.random() * 80 + '%';
        word.style.left = Math.random() * 100 + '%';
      });
    }

    // Initialize concrete word lengths
    const concreteStyle = post.querySelector('.concrete-style');
    if (concreteStyle) {
      const words = concreteStyle.querySelectorAll('.concrete-word');
      words.forEach(word => {
        word.style.setProperty('--length', word.dataset.length);
      });
    }

    // Initialize kinetic sentences
    const kineticStyle = post.querySelector('.kinetic-style');
    if (kineticStyle) {
      const sentences = kineticStyle.querySelectorAll('.typo-sentence');
      sentences.forEach(sentence => {
        sentence.style.setProperty('--index', sentence.dataset.index);
      });
    }
  });

  // Style switching
  styleButtons.forEach(button => {
    button.addEventListener('click', function() {
      const style = this.dataset.style;

      // Update active button
      styleButtons.forEach(b => b.classList.remove('active'));
      this.classList.add('active');

      // Switch styles for all posts
      posts.forEach(post => {
        const contents = post.querySelectorAll('.typo-content');
        contents.forEach(content => {
          content.style.display = 'none';
        });

        const activeContent = post.querySelector(`.${style}-style`);
        if (activeContent) {
          activeContent.style.display = 'block';
        }
      });
    });
  });
});
</script>

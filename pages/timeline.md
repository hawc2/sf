---
layout: page
title: Timeline
permalink: /timeline/
---

<div id="timeline-container">
  <div id="timeline-controls">
    <button class="timeline-btn" data-range="all">All Years</button>
    <button class="timeline-btn" data-range="1940s">1940s</button>
    <button class="timeline-btn" data-range="1950s">1950s</button>
    <button class="timeline-btn" data-range="1960s">1960s</button>
    <button class="timeline-btn" data-range="1970s">1970s</button>
    <button class="timeline-btn" data-range="2010s">2010s</button>
  </div>

  <div id="timeline-view">
    <div class="timeline-line"></div>
    <div id="timeline-items">
      {% assign sorted_items = site.sf | sort: '_date' %}
      {% for item in sorted_items %}
        <div class="timeline-item"
             data-year="{{ item._date }}"
             data-decade="{{ item._date | slice: 0, 3 }}0s"
             data-type="{% if item.writing != '' %}post{% else %}photo{% endif %}">
          <div class="timeline-marker"></div>
          <div class="timeline-content">
            <div class="timeline-date">{{ item._date }}</div>
            <div class="timeline-image">
              <a href="{{ item.url | relative_url }}">
                <img src="{{ item.thumbnail | relative_url }}" alt="{{ item.label }}">
              </a>
            </div>
            <div class="timeline-info">
              <h3><a href="{{ item.url | relative_url }}">{{ item.label }}</a></h3>
              <p class="timeline-subject">{{ item.subject }}</p>
              {% if item.writing %}
                <div class="timeline-excerpt">
                  {{ item.writing | truncatewords: 30 }}
                </div>
              {% endif %}
            </div>
          </div>
        </div>
      {% endfor %}
    </div>
  </div>
</div>

<style>
#timeline-container {
  width: 100%;
  padding: 2rem 0;
}

#timeline-controls {
  text-align: center;
  margin-bottom: 3rem;
  position: sticky;
  top: 0;
  background: white;
  z-index: 100;
  padding: 1rem 0;
  border-bottom: 2px solid #333;
}

.timeline-btn {
  background: #f4f4f4;
  border: 2px solid #333;
  padding: 0.5rem 1rem;
  margin: 0.25rem;
  cursor: pointer;
  font-family: inherit;
  font-size: 0.9rem;
  transition: all 0.3s ease;
}

.timeline-btn:hover,
.timeline-btn.active {
  background: #333;
  color: white;
}

#timeline-view {
  position: relative;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
}

.timeline-line {
  position: absolute;
  left: 50%;
  top: 0;
  bottom: 0;
  width: 4px;
  background: linear-gradient(to bottom, #333 0%, #666 50%, #999 100%);
  transform: translateX(-50%);
}

#timeline-items {
  position: relative;
}

.timeline-item {
  position: relative;
  margin-bottom: 4rem;
  opacity: 1;
  transition: all 0.5s ease;
}

.timeline-item.hidden {
  opacity: 0;
  height: 0;
  margin: 0;
  overflow: hidden;
}

.timeline-item:nth-child(odd) .timeline-content {
  margin-left: 0;
  margin-right: auto;
  padding-right: 3rem;
  text-align: right;
}

.timeline-item:nth-child(even) .timeline-content {
  margin-left: auto;
  margin-right: 0;
  padding-left: 3rem;
  text-align: left;
}

.timeline-marker {
  position: absolute;
  left: 50%;
  top: 2rem;
  width: 20px;
  height: 20px;
  background: #333;
  border: 4px solid white;
  border-radius: 50%;
  transform: translateX(-50%);
  z-index: 10;
  box-shadow: 0 0 0 4px #333;
  transition: all 0.3s ease;
}

.timeline-item:hover .timeline-marker {
  width: 30px;
  height: 30px;
  background: #ff6b6b;
}

.timeline-content {
  width: 45%;
  background: #f9f9f9;
  border: 2px solid #333;
  padding: 1.5rem;
  box-shadow: 4px 4px 0 rgba(0,0,0,0.1);
  transition: all 0.3s ease;
}

.timeline-item:hover .timeline-content {
  box-shadow: 8px 8px 0 rgba(0,0,0,0.2);
  transform: scale(1.02);
}

.timeline-date {
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 1rem;
  color: #333;
  font-family: monospace;
}

.timeline-image {
  margin: 1rem 0;
  border: 2px solid #333;
  overflow: hidden;
}

.timeline-image img {
  width: 100%;
  height: auto;
  display: block;
  transition: transform 0.3s ease;
}

.timeline-image:hover img {
  transform: scale(1.05);
}

.timeline-info h3 {
  margin: 1rem 0 0.5rem;
  font-size: 1.2rem;
}

.timeline-info h3 a {
  color: #333;
  text-decoration: none;
  border-bottom: 2px solid transparent;
  transition: border-color 0.3s ease;
}

.timeline-info h3 a:hover {
  border-bottom-color: #333;
}

.timeline-subject {
  font-style: italic;
  margin-bottom: 1rem;
  color: #666;
}

.timeline-excerpt {
  font-size: 0.9rem;
  line-height: 1.6;
  color: #444;
  margin-top: 1rem;
  padding-top: 1rem;
  border-top: 1px solid #ddd;
}

/* Responsive design */
@media (max-width: 768px) {
  .timeline-line {
    left: 2rem;
  }

  .timeline-item:nth-child(odd) .timeline-content,
  .timeline-item:nth-child(even) .timeline-content {
    width: calc(100% - 5rem);
    margin-left: 4rem;
    padding-left: 1rem;
    text-align: left;
  }

  .timeline-marker {
    left: 2rem;
  }
}
</style>

<script>
document.addEventListener('DOMContentLoaded', function() {
  const buttons = document.querySelectorAll('.timeline-btn');
  const items = document.querySelectorAll('.timeline-item');

  buttons.forEach(button => {
    button.addEventListener('click', function() {
      const range = this.dataset.range;

      // Update active button
      buttons.forEach(b => b.classList.remove('active'));
      this.classList.add('active');

      // Filter items
      items.forEach(item => {
        if (range === 'all') {
          item.classList.remove('hidden');
        } else {
          if (item.dataset.decade === range) {
            item.classList.remove('hidden');
          } else {
            item.classList.add('hidden');
          }
        }
      });
    });
  });

  // Set 'all' as default
  buttons[0].classList.add('active');
});
</script>

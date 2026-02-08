---
layout: page
title: Reimagined Browse
permalink: /browse/
---

<div id="browse-container">
  <div id="browse-modes">
    <h2>Explore by Mode</h2>
    <div class="mode-selector">
      <button class="mode-btn active" data-mode="grid">Grid View</button>
      <button class="mode-btn" data-mode="list">List View</button>
      <button class="mode-btn" data-mode="text">Text Only</button>
      <button class="mode-btn" data-mode="images">Images Only</button>
    </div>
  </div>

  <div id="browse-filters">
    <h3>Filter Content</h3>
    <div class="filter-group">
      <label>Type:</label>
      <button class="filter-btn active" data-filter="type" data-value="all">All</button>
      <button class="filter-btn" data-filter="type" data-value="commentary">With Commentary</button>
      <button class="filter-btn" data-filter="type" data-value="photos">Photos Only</button>
    </div>
    <div class="filter-group">
      <label>Era:</label>
      <button class="filter-btn active" data-filter="era" data-value="all">All</button>
      <button class="filter-btn" data-filter="era" data-value="past">Past (pre-2000)</button>
      <button class="filter-btn" data-filter="era" data-value="recent">Recent (2000+)</button>
    </div>
    <div class="filter-group">
      <label>Content:</label>
      <button class="filter-btn active" data-filter="content" data-value="all">All</button>
      <button class="filter-btn" data-filter="content" data-value="books">Books</button>
      <button class="filter-btn" data-filter="content" data-value="personal">Personal</button>
    </div>
  </div>

  <div id="items-container" class="grid-mode">
    {% assign sorted_items = site.sf | sort: '_date' | reverse %}
    {% for item in sorted_items %}
      {% assign has_writing = false %}
      {% if item.writing and item.writing != '' %}
        {% assign has_writing = true %}
      {% endif %}

      {% assign era = 'past' %}
      {% if item._date >= '2000' %}
        {% assign era = 'recent' %}
      {% endif %}

      {% assign content_type = 'personal' %}
      {% if item.subject contains 'Book' or item.subject contains 'Cover' %}
        {% assign content_type = 'books' %}
      {% endif %}

      <div class="browse-item"
           data-type="{% if has_writing %}commentary{% else %}photos{% endif %}"
           data-era="{{ era }}"
           data-content="{{ content_type }}"
           data-year="{{ item._date }}">

        <div class="item-image">
          <a href="{{ item.url | relative_url }}">
            <img src="{{ item.thumbnail | relative_url }}" alt="{{ item.label }}">
            <div class="item-overlay">
              <span class="item-year">{{ item._date }}</span>
            </div>
          </a>
        </div>

        <div class="item-details">
          <h3><a href="{{ item.url | relative_url }}">{{ item.label }}</a></h3>
          <p class="item-subject">{{ item.subject }}</p>
          {% if has_writing %}
            <div class="item-writing">
              <p>{{ item.writing | truncatewords: 50 }}</p>
              <a href="{{ item.url | relative_url }}" class="read-more">Read full post →</a>
            </div>
          {% endif %}
        </div>
      </div>
    {% endfor %}
  </div>

  <div id="stats-panel">
    <div class="stat">
      <span class="stat-number" id="visible-count">{{ site.sf | size }}</span>
      <span class="stat-label">items visible</span>
    </div>
    <div class="stat">
      <span class="stat-number">{{ site.sf | size }}</span>
      <span class="stat-label">total items</span>
    </div>
  </div>
</div>

<style>
#browse-container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 2rem;
}

#browse-modes {
  text-align: center;
  margin-bottom: 2rem;
  padding: 2rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border-radius: 8px;
}

#browse-modes h2 {
  margin: 0 0 1rem;
  font-size: 2rem;
}

.mode-selector {
  display: flex;
  justify-content: center;
  gap: 1rem;
  flex-wrap: wrap;
}

.mode-btn {
  background: white;
  color: #667eea;
  border: none;
  padding: 0.75rem 1.5rem;
  font-size: 1rem;
  font-weight: bold;
  border-radius: 25px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
}

.mode-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 12px rgba(0,0,0,0.2);
}

.mode-btn.active {
  background: #333;
  color: white;
}

#browse-filters {
  background: #f9f9f9;
  padding: 1.5rem;
  border-radius: 8px;
  margin-bottom: 2rem;
  border: 2px solid #333;
}

#browse-filters h3 {
  margin: 0 0 1rem;
  font-size: 1.3rem;
}

.filter-group {
  margin-bottom: 1rem;
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.filter-group label {
  font-weight: bold;
  margin-right: 0.5rem;
  min-width: 80px;
}

.filter-btn {
  background: white;
  border: 2px solid #ddd;
  padding: 0.5rem 1rem;
  cursor: pointer;
  transition: all 0.3s ease;
  border-radius: 4px;
  font-size: 0.9rem;
}

.filter-btn:hover {
  border-color: #333;
}

.filter-btn.active {
  background: #333;
  color: white;
  border-color: #333;
}

#items-container {
  margin-bottom: 2rem;
}

/* Grid Mode */
#items-container.grid-mode {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2rem;
}

#items-container.grid-mode .browse-item {
  border: 2px solid #333;
  background: white;
  transition: all 0.3s ease;
}

#items-container.grid-mode .browse-item:hover {
  transform: translateY(-5px);
  box-shadow: 8px 8px 0 rgba(0,0,0,0.2);
}

#items-container.grid-mode .item-details {
  padding: 1rem;
}

#items-container.grid-mode .item-writing {
  display: none;
}

/* List Mode */
#items-container.list-mode {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

#items-container.list-mode .browse-item {
  display: grid;
  grid-template-columns: 300px 1fr;
  gap: 2rem;
  border: 2px solid #333;
  background: white;
  padding: 1rem;
}

#items-container.list-mode .item-writing {
  display: block;
  margin-top: 1rem;
  padding-top: 1rem;
  border-top: 1px solid #ddd;
}

/* Text Only Mode */
#items-container.text-mode {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

#items-container.text-mode .browse-item {
  border-left: 4px solid #333;
  padding-left: 2rem;
}

#items-container.text-mode .item-image {
  display: none;
}

#items-container.text-mode .item-writing {
  display: block;
  font-size: 1.1rem;
  line-height: 1.8;
  margin-top: 1rem;
}

/* Images Only Mode */
#items-container.images-mode {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 1rem;
}

#items-container.images-mode .item-details {
  display: none;
}

#items-container.images-mode .browse-item {
  position: relative;
}

#items-container.images-mode .item-overlay {
  opacity: 1;
}

/* Common Item Styles */
.browse-item {
  transition: all 0.3s ease;
}

.browse-item.hidden {
  display: none;
}

.item-image {
  position: relative;
  overflow: hidden;
  background: #f4f4f4;
}

.item-image img {
  width: 100%;
  height: auto;
  display: block;
  transition: transform 0.3s ease;
}

.item-image:hover img {
  transform: scale(1.05);
}

.item-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(0,0,0,0.8);
  color: white;
  padding: 0.5rem;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.item-image:hover .item-overlay {
  opacity: 1;
}

.item-year {
  font-weight: bold;
  font-family: monospace;
}

.item-details h3 {
  margin: 0 0 0.5rem;
  font-size: 1.2rem;
}

.item-details h3 a {
  color: #333;
  text-decoration: none;
  border-bottom: 2px solid transparent;
  transition: border-color 0.3s ease;
}

.item-details h3 a:hover {
  border-bottom-color: #333;
}

.item-subject {
  font-style: italic;
  color: #666;
  margin: 0 0 1rem;
}

.item-writing {
  font-size: 0.95rem;
  line-height: 1.6;
  color: #444;
}

.read-more {
  display: inline-block;
  margin-top: 0.5rem;
  color: #667eea;
  text-decoration: none;
  font-weight: bold;
}

.read-more:hover {
  text-decoration: underline;
}

#stats-panel {
  display: flex;
  justify-content: center;
  gap: 3rem;
  padding: 2rem;
  background: #333;
  color: white;
  border-radius: 8px;
  margin-top: 2rem;
}

.stat {
  text-align: center;
}

.stat-number {
  display: block;
  font-size: 3rem;
  font-weight: bold;
  font-family: monospace;
}

.stat-label {
  display: block;
  font-size: 0.9rem;
  text-transform: uppercase;
  letter-spacing: 1px;
}

@media (max-width: 768px) {
  #items-container.list-mode .browse-item {
    grid-template-columns: 1fr;
  }

  #items-container.grid-mode {
    grid-template-columns: 1fr;
  }
}
</style>

<script>
document.addEventListener('DOMContentLoaded', function() {
  const modeButtons = document.querySelectorAll('.mode-btn');
  const filterButtons = document.querySelectorAll('.filter-btn');
  const container = document.getElementById('items-container');
  const items = document.querySelectorAll('.browse-item');
  const visibleCount = document.getElementById('visible-count');

  let currentFilters = {
    type: 'all',
    era: 'all',
    content: 'all'
  };

  // Mode switching
  modeButtons.forEach(button => {
    button.addEventListener('click', function() {
      const mode = this.dataset.mode;

      modeButtons.forEach(b => b.classList.remove('active'));
      this.classList.add('active');

      container.className = mode + '-mode';
    });
  });

  // Filter functionality
  function updateVisibility() {
    let visibleItems = 0;

    items.forEach(item => {
      let show = true;

      // Check each filter
      if (currentFilters.type !== 'all' && item.dataset.type !== currentFilters.type) {
        show = false;
      }
      if (currentFilters.era !== 'all' && item.dataset.era !== currentFilters.era) {
        show = false;
      }
      if (currentFilters.content !== 'all' && item.dataset.content !== currentFilters.content) {
        show = false;
      }

      if (show) {
        item.classList.remove('hidden');
        visibleItems++;
      } else {
        item.classList.add('hidden');
      }
    });

    visibleCount.textContent = visibleItems;
  }

  filterButtons.forEach(button => {
    button.addEventListener('click', function() {
      const filter = this.dataset.filter;
      const value = this.dataset.value;

      // Update filter state
      currentFilters[filter] = value;

      // Update active button in this group
      const group = this.closest('.filter-group');
      group.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
      this.classList.add('active');

      // Update visibility
      updateVisibility();
    });
  });

  // Initialize
  updateVisibility();
});
</script>

---
layout: page
title: Network of Ideas
permalink: /network/
---

<div id="network-container">
  <div id="network-intro">
    <h2>Exploring Connections</h2>
    <p>An interactive network visualizing the themes, subjects, and temporal relationships in Samuel R. Delany's curated posts. Click nodes to explore connections.</p>
  </div>

  <div id="network-controls">
    <button class="network-btn active" data-view="all">All Connections</button>
    <button class="network-btn" data-view="temporal">By Time</button>
    <button class="network-btn" data-view="thematic">By Theme</button>
  </div>

  <div id="network-legend">
    <div class="legend-item">
      <div class="legend-dot" style="background: #667eea;"></div>
      <span>Posts with Commentary</span>
    </div>
    <div class="legend-item">
      <div class="legend-dot" style="background: #f093fb;"></div>
      <span>Photos/Images</span>
    </div>
    <div class="legend-item">
      <div class="legend-dot" style="background: #4facfe;"></div>
      <span>Books/Works</span>
    </div>
    <div class="legend-item">
      <div class="legend-dot" style="background: #43e97b;"></div>
      <span>Personal/Family</span>
    </div>
  </div>

  <div id="network-viz"></div>

  <div id="network-info">
    <h3>Selected Item</h3>
    <div id="info-content">
      <p>Click on a node to see details</p>
    </div>
  </div>
</div>

<style>
#network-container {
  max-width: 1600px;
  margin: 0 auto;
  padding: 2rem;
}

#network-intro {
  text-align: center;
  margin-bottom: 2rem;
  padding: 2rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border-radius: 8px;
}

#network-intro h2 {
  margin: 0 0 1rem;
  font-size: 2.5rem;
}

#network-intro p {
  font-size: 1.1rem;
  max-width: 600px;
  margin: 0 auto;
}

#network-controls {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin-bottom: 2rem;
}

.network-btn {
  background: white;
  border: 2px solid #333;
  padding: 0.75rem 1.5rem;
  cursor: pointer;
  font-size: 1rem;
  font-weight: bold;
  transition: all 0.3s ease;
  border-radius: 4px;
}

.network-btn:hover {
  background: #f4f4f4;
}

.network-btn.active {
  background: #333;
  color: white;
}

#network-legend {
  display: flex;
  justify-content: center;
  gap: 2rem;
  margin-bottom: 2rem;
  flex-wrap: wrap;
}

.legend-item {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.legend-dot {
  width: 16px;
  height: 16px;
  border-radius: 50%;
  border: 2px solid #333;
}

#network-viz {
  width: 100%;
  height: 800px;
  background: #f9f9f9;
  border: 3px solid #333;
  border-radius: 8px;
  position: relative;
  overflow: hidden;
}

.network-node {
  cursor: pointer;
  transition: all 0.3s ease;
}

.network-node circle {
  stroke: #333;
  stroke-width: 2px;
  transition: all 0.3s ease;
}

.network-node:hover circle {
  stroke-width: 4px;
  filter: brightness(1.2);
}

.network-node text {
  font-size: 11px;
  font-weight: bold;
  pointer-events: none;
  text-shadow:
    -1px -1px 0 white,
    1px -1px 0 white,
    -1px 1px 0 white,
    1px 1px 0 white;
}

.network-link {
  stroke: #999;
  stroke-width: 1.5px;
  opacity: 0.6;
  transition: all 0.3s ease;
}

.network-link.highlighted {
  stroke: #333;
  stroke-width: 3px;
  opacity: 1;
}

.network-node.highlighted circle {
  stroke-width: 5px;
  filter: brightness(1.3) drop-shadow(0 0 8px rgba(0,0,0,0.3));
}

#network-info {
  margin-top: 2rem;
  padding: 2rem;
  background: white;
  border: 2px solid #333;
  border-radius: 8px;
  min-height: 200px;
}

#network-info h3 {
  margin: 0 0 1rem;
  font-size: 1.5rem;
  color: #333;
}

#info-content {
  line-height: 1.8;
}

#info-content h4 {
  margin: 0 0 0.5rem;
  font-size: 1.3rem;
}

#info-content .info-meta {
  color: #666;
  font-style: italic;
  margin-bottom: 1rem;
}

#info-content .info-text {
  margin-top: 1rem;
  padding-top: 1rem;
  border-top: 1px solid #ddd;
}

#info-content .info-link {
  display: inline-block;
  margin-top: 1rem;
  padding: 0.5rem 1rem;
  background: #667eea;
  color: white;
  text-decoration: none;
  border-radius: 4px;
  transition: background 0.3s ease;
}

#info-content .info-link:hover {
  background: #5568d3;
}
</style>

<script>
document.addEventListener('DOMContentLoaded', function() {
  // Data from Jekyll collection
  const items = [
    {% for item in site.sf %}
    {
      id: "{{ item.pid }}",
      label: "{{ item.label | escape }}",
      subject: "{{ item.subject | escape }}",
      date: "{{ item._date }}",
      {% if item.writing and item.writing != '' %}
      writing: {{ item.writing | jsonify }},
      hasWriting: true,
      {% else %}
      writing: null,
      hasWriting: false,
      {% endif %}
      url: "{{ item.url | relative_url }}",
      thumbnail: "{{ item.thumbnail | relative_url }}"
    }{% unless forloop.last %},{% endunless %}
    {% endfor %}
  ];

  // Determine node type/color
  function getNodeType(item) {
    if (item.hasWriting) return 'commentary';
    if (item.subject.includes('Book') || item.subject.includes('Cover')) return 'book';
    if (item.subject.includes('Photo') || item.subject.includes('Family')) return 'personal';
    return 'photo';
  }

  function getNodeColor(type) {
    const colors = {
      'commentary': '#667eea',
      'photo': '#f093fb',
      'book': '#4facfe',
      'personal': '#43e97b'
    };
    return colors[type] || '#999';
  }

  // Build network data
  const nodes = items.map(item => ({
    ...item,
    type: getNodeType(item),
    color: getNodeColor(getNodeType(item)),
    year: parseInt(item.date)
  }));

  // Create links based on temporal proximity and thematic similarity
  const links = [];

  // Temporal links (connect items within 5 years)
  for (let i = 0; i < nodes.length; i++) {
    for (let j = i + 1; j < nodes.length; j++) {
      const yearDiff = Math.abs(nodes[i].year - nodes[j].year);
      if (yearDiff <= 5) {
        links.push({
          source: nodes[i].id,
          target: nodes[j].id,
          type: 'temporal',
          strength: 1 / (yearDiff + 1)
        });
      }
    }
  }

  // Thematic links (connect items of same type)
  for (let i = 0; i < nodes.length; i++) {
    for (let j = i + 1; j < nodes.length; j++) {
      if (nodes[i].type === nodes[j].type) {
        links.push({
          source: nodes[i].id,
          target: nodes[j].id,
          type: 'thematic',
          strength: 0.8
        });
      }
    }
  }

  // Simple force-directed layout (no D3 dependency)
  const viz = document.getElementById('network-viz');
  const width = viz.clientWidth;
  const height = viz.clientHeight;

  // Create SVG
  const svg = document.createElementNS('http://www.w3.org/2000/svg', 'svg');
  svg.setAttribute('width', width);
  svg.setAttribute('height', height);
  viz.appendChild(svg);

  // Position nodes in a circle initially
  const centerX = width / 2;
  const centerY = height / 2;
  const radius = Math.min(width, height) / 3;

  nodes.forEach((node, i) => {
    const angle = (i / nodes.length) * 2 * Math.PI;
    node.x = centerX + radius * Math.cos(angle);
    node.y = centerY + radius * Math.sin(angle);
    node.vx = 0;
    node.vy = 0;
  });

  // Draw links
  const linkGroup = document.createElementNS('http://www.w3.org/2000/svg', 'g');
  svg.appendChild(linkGroup);

  links.forEach(link => {
    const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
    line.classList.add('network-link');
    line.setAttribute('data-type', link.type);
    line.setAttribute('data-source', link.source);
    line.setAttribute('data-target', link.target);
    linkGroup.appendChild(line);
    link.element = line;
  });

  // Draw nodes
  const nodeGroup = document.createElementNS('http://www.w3.org/2000/svg', 'g');
  svg.appendChild(nodeGroup);

  nodes.forEach(node => {
    const g = document.createElementNS('http://www.w3.org/2000/svg', 'g');
    g.classList.add('network-node');
    g.setAttribute('data-id', node.id);

    const circle = document.createElementNS('http://www.w3.org/2000/svg', 'circle');
    circle.setAttribute('r', node.hasWriting ? 12 : 8);
    circle.setAttribute('fill', node.color);

    const text = document.createElementNS('http://www.w3.org/2000/svg', 'text');
    text.setAttribute('dy', -15);
    text.setAttribute('text-anchor', 'middle');
    text.textContent = node.year;

    g.appendChild(circle);
    g.appendChild(text);
    nodeGroup.appendChild(g);
    node.element = g;

    // Click handler
    g.addEventListener('click', () => selectNode(node));
  });

  // Simple physics simulation
  function updatePositions() {
    // Apply forces
    const alpha = 0.1;

    // Repulsion between nodes
    for (let i = 0; i < nodes.length; i++) {
      for (let j = i + 1; j < nodes.length; j++) {
        const dx = nodes[j].x - nodes[i].x;
        const dy = nodes[j].y - nodes[i].y;
        const dist = Math.sqrt(dx * dx + dy * dy) || 1;
        const force = 100 / (dist * dist);

        nodes[i].vx -= (dx / dist) * force;
        nodes[i].vy -= (dy / dist) * force;
        nodes[j].vx += (dx / dist) * force;
        nodes[j].vy += (dy / dist) * force;
      }
    }

    // Link attraction
    links.forEach(link => {
      const source = nodes.find(n => n.id === link.source);
      const target = nodes.find(n => n.id === link.target);
      if (!source || !target) return;

      const dx = target.x - source.x;
      const dy = target.y - source.y;
      const dist = Math.sqrt(dx * dx + dy * dy) || 1;
      const force = (dist - 100) * 0.01 * link.strength;

      source.vx += (dx / dist) * force;
      source.vy += (dy / dist) * force;
      target.vx -= (dx / dist) * force;
      target.vy -= (dy / dist) * force;
    });

    // Center gravity
    nodes.forEach(node => {
      node.vx += (centerX - node.x) * 0.001;
      node.vy += (centerY - node.y) * 0.001;
    });

    // Update positions
    nodes.forEach(node => {
      node.x += node.vx * alpha;
      node.y += node.vy * alpha;
      node.vx *= 0.9;
      node.vy *= 0.9;

      // Keep in bounds
      node.x = Math.max(50, Math.min(width - 50, node.x));
      node.y = Math.max(50, Math.min(height - 50, node.y));

      node.element.setAttribute('transform', `translate(${node.x}, ${node.y})`);
    });

    // Update links
    links.forEach(link => {
      const source = nodes.find(n => n.id === link.source);
      const target = nodes.find(n => n.id === link.target);
      if (!source || !target) return;

      link.element.setAttribute('x1', source.x);
      link.element.setAttribute('y1', source.y);
      link.element.setAttribute('x2', target.x);
      link.element.setAttribute('y2', target.y);
    });
  }

  // Animate
  let iterations = 0;
  const maxIterations = 500;
  const interval = setInterval(() => {
    updatePositions();
    iterations++;
    if (iterations >= maxIterations) {
      clearInterval(interval);
    }
  }, 20);

  // Node selection
  function selectNode(node) {
    // Clear previous highlights
    document.querySelectorAll('.network-node').forEach(n => n.classList.remove('highlighted'));
    document.querySelectorAll('.network-link').forEach(l => l.classList.remove('highlighted'));

    // Highlight selected node
    node.element.classList.add('highlighted');

    // Highlight connected links
    links.forEach(link => {
      if (link.source === node.id || link.target === node.id) {
        link.element.classList.add('highlighted');
      }
    });

    // Update info panel
    const infoContent = document.getElementById('info-content');
    infoContent.innerHTML = `
      <h4>${node.label}</h4>
      <p class="info-meta">${node.subject} (${node.date})</p>
      ${node.writing ? `<p class="info-text">${node.writing.substring(0, 300)}...</p>` : ''}
      <a href="${node.url}" class="info-link">View Full Item →</a>
    `;
  }

  // View controls
  const viewButtons = document.querySelectorAll('.network-btn');
  viewButtons.forEach(button => {
    button.addEventListener('click', function() {
      const view = this.dataset.view;

      viewButtons.forEach(b => b.classList.remove('active'));
      this.classList.add('active');

      // Filter links based on view
      links.forEach(link => {
        if (view === 'all') {
          link.element.style.display = '';
        } else if (view === link.type) {
          link.element.style.display = '';
        } else {
          link.element.style.display = 'none';
        }
      });
    });
  });
});
</script>

---
layout: page
title: Thematic Analysis
permalink: /themes/
---

<div id="themes-container">
  <header id="themes-header">
    <h1>Thematic Constellations</h1>
    <p class="themes-intro">Exploring recurring ideas, concepts, and connections across Samuel R. Delany's posts</p>
  </header>

  <section id="key-themes">
    <h2>Key Themes Discovered</h2>
    <div class="themes-grid">
      <div class="theme-card" data-theme="spectacle">
        <div class="theme-icon">👁️</div>
        <h3>Spectacle & Society</h3>
        <p class="theme-description">Debord's theories on spectacle, misinformation, and media saturation</p>
        <div class="theme-stats">
          <span class="stat-item">1 post</span>
          <span class="stat-item">2016</span>
        </div>
        <div class="theme-connections">
          <strong>Connected to:</strong>
          <span class="connection-tag">Critical Theory</span>
          <span class="connection-tag">Media Studies</span>
        </div>
      </div>

      <div class="theme-card" data-theme="identity">
        <div class="theme-icon">🌈</div>
        <h3>LGBTQ+ Identity & Space</h3>
        <p class="theme-description">Queer spaces, Giovanni's Room, and LGBTQ+ history</p>
        <div class="theme-stats">
          <span class="stat-item">1 post</span>
          <span class="stat-item">2019</span>
        </div>
        <div class="theme-connections">
          <strong>Connected to:</strong>
          <span class="connection-tag">Personal History</span>
          <span class="connection-tag">Philadelphia</span>
        </div>
      </div>

      <div class="theme-card" data-theme="archive">
        <div class="theme-icon">📚</div>
        <h3>Literary Archive</h3>
        <p class="theme-description">Book covers, publication history, and the material culture of SF</p>
        <div class="theme-stats">
          <span class="stat-item">7 posts</span>
          <span class="stat-item">1962-1977</span>
        </div>
        <div class="theme-connections">
          <strong>Connected to:</strong>
          <span class="connection-tag">Science Fiction</span>
          <span class="connection-tag">Publishing</span>
        </div>
      </div>

      <div class="theme-card" data-theme="memory">
        <div class="theme-icon">👨‍👩‍👧</div>
        <h3>Family & Memory</h3>
        <p class="theme-description">Early photographs, family relationships, and personal history</p>
        <div class="theme-stats">
          <span class="stat-item">3 posts</span>
          <span class="stat-item">1948-1950</span>
        </div>
        <div class="theme-connections">
          <strong>Connected to:</strong>
          <span class="connection-tag">Childhood</span>
          <span class="connection-tag">Documentary</span>
        </div>
      </div>

      <div class="theme-card" data-theme="icons">
        <div class="theme-icon">⭐</div>
        <h3>Cultural Icons</h3>
        <p class="theme-description">Influential figures and moments in queer and cultural history</p>
        <div class="theme-stats">
          <span class="stat-item">1 post</span>
          <span class="stat-item">1966</span>
        </div>
        <div class="theme-connections">
          <strong>Connected to:</strong>
          <span class="connection-tag">Stonewall Era</span>
          <span class="connection-tag">Activism</span>
        </div>
      </div>

      <div class="theme-card" data-theme="contemporary">
        <div class="theme-icon">💭</div>
        <h3>Contemporary Thought</h3>
        <p class="theme-description">Modern reflections, selfies, and present-day observations</p>
        <div class="theme-stats">
          <span class="stat-item">1 post</span>
          <span class="stat-item">2016</span>
        </div>
        <div class="theme-connections">
          <strong>Connected to:</strong>
          <span class="connection-tag">Self-Representation</span>
          <span class="connection-tag">Digital Age</span>
        </div>
      </div>
    </div>
  </section>

  <section id="temporal-analysis">
    <h2>Temporal Patterns</h2>
    <div class="temporal-viz">
      <div class="decade-bar" style="--height: 30%; --color: #667eea;">
        <span class="decade-label">1940s</span>
        <span class="decade-count">2 items</span>
      </div>
      <div class="decade-bar" style="--height: 10%; --color: #764ba2;">
        <span class="decade-label">1950s</span>
        <span class="decade-count">1 item</span>
      </div>
      <div class="decade-bar" style="--height: 60%; --color: #f093fb;">
        <span class="decade-label">1960s</span>
        <span class="decade-count">4 items</span>
      </div>
      <div class="decade-bar" style="--height: 20%; --color: #4facfe;">
        <span class="decade-label">1970s</span>
        <span class="decade-count">2 items</span>
      </div>
      <div class="decade-bar" style="--height: 40%; --color: #43e97b;">
        <span class="decade-label">2010s</span>
        <span class="decade-count">3 items</span>
      </div>
    </div>
    <p class="temporal-insight">The collection spans seven decades, with concentrated activity in the 1960s (documenting Delany's early career) and 2010s (recent Facebook posts).</p>
  </section>

  <section id="word-cloud">
    <h2>Recurring Concepts</h2>
    <div class="word-cloud">
      {% for item in site.sf %}
        {% if item.writing and item.writing != '' %}
          {% assign words = item.writing | downcase | split: " " %}
          {% assign important_words = "spectacle,society,book,delany,debord,disinformation,ecological,power,cover,photo,family,facebook,giovanni,room,pride,edition,chip" | split: "," %}
          {% for word in words %}
            {% if important_words contains word %}
              <span class="cloud-word" data-word="{{ word }}">{{ word }}</span>
            {% endif %}
          {% endfor %}
        {% endif %}
      {% endfor %}
    </div>
  </section>

  <section id="content-breakdown">
    <h2>Content Analysis</h2>
    <div class="breakdown-grid">
      <div class="breakdown-card">
        <div class="breakdown-number">13</div>
        <div class="breakdown-label">Total Items</div>
      </div>
      <div class="breakdown-card">
        <div class="breakdown-number">3</div>
        <div class="breakdown-label">Posts with<br>Commentary</div>
      </div>
      <div class="breakdown-card">
        <div class="breakdown-number">7</div>
        <div class="breakdown-label">Book<br>Covers</div>
      </div>
      <div class="breakdown-card">
        <div class="breakdown-number">3</div>
        <div class="breakdown-label">Family<br>Photos</div>
      </div>
      <div class="breakdown-card">
        <div class="breakdown-number">70</div>
        <div class="breakdown-label">Years<br>Spanned</div>
      </div>
    </div>
  </section>

  <section id="deep-dive">
    <h2>Featured Analysis</h2>

    <article class="analysis-article">
      <h3>The Spectacle of Misinformation</h3>
      <div class="analysis-meta">
        <span class="analysis-tag">Critical Theory</span>
        <span class="analysis-tag">Contemporary Issues</span>
      </div>
      <div class="analysis-content">
        <p>Delany's 2016 post on Guy Debord's "Comments on the Society of the Spectacle" reveals a deep engagement with critical theory applied to contemporary media landscapes. The post connects Debord's concept of "unanswerable lies" and "disinformation" to modern phenomena like climate change denial.</p>

        <blockquote class="analysis-quote">
          "Where disinformation is named, it does not exist. Where it exists, it is not named."
        </blockquote>

        <p>This reflection demonstrates Delany's ongoing intellectual engagement with theoretical frameworks that explain power, media, and social control—themes that have permeated his speculative fiction throughout his career.</p>

        <div class="related-items">
          <strong>Related Items:</strong>
          <a href="{{ '/sf/sf12/' | relative_url }}" class="related-link">Facebook Post De Bord (2016)</a>
        </div>
      </div>
    </article>

    <article class="analysis-article">
      <h3>Archiving a Literary Life</h3>
      <div class="analysis-meta">
        <span class="analysis-tag">Publishing History</span>
        <span class="analysis-tag">Material Culture</span>
      </div>
      <div class="analysis-content">
        <p>The seven book covers spanning 1962-1977 create a visual archive of Delany's most productive period as a science fiction writer. From "The Fall of the Towers" to "Triton," these covers document the material culture of SF publishing in its golden age.</p>

        <p>Each cover reflects not just a literary work but a moment in design history, genre conventions, and market positioning. Together, they tell the story of how speculative fiction presented itself to readers during a transformative period.</p>

        <div class="related-items">
          <strong>Related Items:</strong>
          <a href="{{ '/timeline/' | relative_url }}" class="related-link">View on Timeline</a>
        </div>
      </div>
    </article>

    <article class="analysis-article">
      <h3>Personal & Political Space</h3>
      <div class="analysis-meta">
        <span class="analysis-tag">LGBTQ+ History</span>
        <span class="analysis-tag">Place</span>
      </div>
      <div class="analysis-content">
        <p>The 2019 post "Leaving Giovanni's Room on Gay Pride Day" marks a contemporary moment of queer visibility in Philadelphia. Giovanni's Room, the legendary LGBTQ+ bookstore (named after James Baldwin's novel), represents decades of queer literary culture.</p>

        <p>This brief post connects personal experience, literary heritage, political celebration, and urban space—compressing layers of meaning into a single documented moment.</p>

        <div class="related-items">
          <strong>Related Items:</strong>
          <a href="{{ '/sf/sf13/' | relative_url }}" class="related-link">Facebook Post Gay Pride (2019)</a>
        </div>
      </div>
    </article>
  </section>

  <section id="connections-map">
    <h2>Conceptual Connections</h2>
    <div class="connections-diagram">
      <svg viewBox="0 0 800 600" class="connections-svg">
        <!-- Central node -->
        <circle cx="400" cy="300" r="60" fill="#667eea" stroke="#fff" stroke-width="3"/>
        <text x="400" y="305" text-anchor="middle" fill="#fff" font-weight="bold">SRD</text>

        <!-- Surrounding nodes -->
        <circle cx="200" cy="150" r="40" fill="#764ba2" stroke="#fff" stroke-width="2"/>
        <text x="200" y="155" text-anchor="middle" fill="#fff" font-size="12">Theory</text>
        <line x1="400" y1="300" x2="200" y2="150" stroke="#999" stroke-width="2"/>

        <circle cx="600" cy="150" r="40" fill="#f093fb" stroke="#fff" stroke-width="2"/>
        <text x="600" y="155" text-anchor="middle" fill="#fff" font-size="12">SF Work</text>
        <line x1="400" y1="300" x2="600" y2="150" stroke="#999" stroke-width="2"/>

        <circle cx="150" cy="400" r="40" fill="#4facfe" stroke="#fff" stroke-width="2"/>
        <text x="150" y="405" text-anchor="middle" fill="#fff" font-size="12">Family</text>
        <line x1="400" y1="300" x2="150" y2="400" stroke="#999" stroke-width="2"/>

        <circle cx="650" cy="400" r="40" fill="#43e97b" stroke="#fff" stroke-width="2"/>
        <text x="650" y="405" text-anchor="middle" fill="#fff" font-size="12">Identity</text>
        <line x1="400" y1="300" x2="650" y2="400" stroke="#999" stroke-width="2"/>

        <circle cx="400" cy="500" r="40" fill="#ffeaa7" stroke="#fff" stroke-width="2"/>
        <text x="400" y="505" text-anchor="middle" fill="#333" font-size="12">Space</text>
        <line x1="400" y1="300" x2="400" y2="500" stroke="#999" stroke-width="2"/>
      </svg>
    </div>
    <p class="connections-note">All themes connect through Delany's multifaceted identity as writer, theorist, and chronicler of personal and cultural history.</p>
  </section>
</div>

<style>
#themes-container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 2rem;
  background: #0a0a0a;
  color: #fff;
}

#themes-header {
  text-align: center;
  padding: 4rem 2rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  margin: -2rem -2rem 3rem;
  border-radius: 0 0 20px 20px;
}

#themes-header h1 {
  font-size: 3.5rem;
  margin-bottom: 1rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
}

.themes-intro {
  font-size: 1.3rem;
  opacity: 0.9;
  max-width: 700px;
  margin: 0 auto;
}

section {
  margin-bottom: 5rem;
  padding: 3rem;
  background: #1a1a1a;
  border-radius: 12px;
  border: 2px solid #333;
}

section h2 {
  font-size: 2.5rem;
  margin-bottom: 2rem;
  color: #667eea;
  text-align: center;
}

.themes-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.theme-card {
  background: #2a2a2a;
  padding: 2rem;
  border-radius: 8px;
  border: 2px solid #444;
  transition: all 0.3s ease;
  cursor: pointer;
}

.theme-card:hover {
  transform: translateY(-5px);
  border-color: #667eea;
  box-shadow: 0 10px 30px rgba(102, 126, 234, 0.3);
}

.theme-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.theme-card h3 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: #fff;
}

.theme-description {
  font-size: 1rem;
  line-height: 1.6;
  color: #ccc;
  margin-bottom: 1.5rem;
}

.theme-stats {
  display: flex;
  gap: 1rem;
  margin-bottom: 1rem;
  padding: 0.75rem 0;
  border-top: 1px solid #444;
  border-bottom: 1px solid #444;
}

.stat-item {
  font-family: monospace;
  color: #667eea;
  font-weight: bold;
}

.theme-connections {
  font-size: 0.9rem;
  color: #999;
}

.connection-tag {
  display: inline-block;
  background: #333;
  padding: 0.25rem 0.75rem;
  border-radius: 12px;
  margin: 0.25rem;
  font-size: 0.85rem;
}

.temporal-viz {
  display: flex;
  justify-content: space-around;
  align-items: flex-end;
  height: 300px;
  margin-bottom: 2rem;
  padding: 2rem;
  background: #2a2a2a;
  border-radius: 8px;
}

.decade-bar {
  flex: 1;
  height: var(--height);
  background: var(--color);
  margin: 0 0.5rem;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  align-items: center;
  padding: 1rem 0.5rem;
  border-radius: 4px 4px 0 0;
  transition: all 0.3s ease;
  cursor: pointer;
  position: relative;
}

.decade-bar:hover {
  filter: brightness(1.3);
  transform: translateY(-10px);
}

.decade-label {
  font-weight: bold;
  margin-top: 1rem;
  font-size: 0.9rem;
}

.decade-count {
  font-size: 0.8rem;
  color: rgba(255, 255, 255, 0.7);
}

.temporal-insight {
  text-align: center;
  font-size: 1.1rem;
  line-height: 1.8;
  color: #ccc;
  padding: 0 2rem;
}

.word-cloud {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 1rem;
  padding: 3rem;
  background: #2a2a2a;
  border-radius: 8px;
  min-height: 300px;
  align-items: center;
}

.cloud-word {
  display: inline-block;
  font-size: calc(1rem + var(--size, 1) * 0.5rem);
  color: var(--color, #667eea);
  opacity: 0.8;
  transition: all 0.3s ease;
  cursor: pointer;
  padding: 0.25rem 0.5rem;
}

.cloud-word:hover {
  opacity: 1;
  transform: scale(1.3);
  color: #fff;
}

.breakdown-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 2rem;
}

.breakdown-card {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  padding: 2rem;
  border-radius: 8px;
  text-align: center;
  transition: transform 0.3s ease;
}

.breakdown-card:hover {
  transform: scale(1.05);
}

.breakdown-number {
  font-size: 4rem;
  font-weight: 900;
  margin-bottom: 0.5rem;
}

.breakdown-label {
  font-size: 1rem;
  opacity: 0.9;
  line-height: 1.4;
}

.analysis-article {
  background: #2a2a2a;
  padding: 2rem;
  border-radius: 8px;
  margin-bottom: 2rem;
  border-left: 4px solid #667eea;
}

.analysis-article h3 {
  font-size: 2rem;
  margin-bottom: 1rem;
  color: #fff;
}

.analysis-meta {
  margin-bottom: 1.5rem;
}

.analysis-tag {
  display: inline-block;
  background: #667eea;
  color: #fff;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  margin-right: 0.5rem;
  font-size: 0.85rem;
  font-weight: bold;
}

.analysis-content {
  font-size: 1.1rem;
  line-height: 1.8;
  color: #ddd;
}

.analysis-content p {
  margin-bottom: 1.5rem;
}

.analysis-quote {
  background: #1a1a1a;
  border-left: 4px solid #667eea;
  padding: 1.5rem;
  margin: 2rem 0;
  font-style: italic;
  font-size: 1.2rem;
  color: #fff;
}

.related-items {
  margin-top: 2rem;
  padding-top: 1.5rem;
  border-top: 1px solid #444;
}

.related-link {
  display: inline-block;
  margin-left: 1rem;
  color: #667eea;
  text-decoration: none;
  font-weight: bold;
}

.related-link:hover {
  text-decoration: underline;
}

.connections-diagram {
  background: #2a2a2a;
  padding: 2rem;
  border-radius: 8px;
}

.connections-svg {
  width: 100%;
  height: auto;
}

.connections-note {
  text-align: center;
  font-size: 1.1rem;
  color: #ccc;
  margin-top: 2rem;
  font-style: italic;
}

@media (max-width: 768px) {
  #themes-header h1 {
    font-size: 2rem;
  }

  .themes-grid {
    grid-template-columns: 1fr;
  }

  .temporal-viz {
    height: 200px;
  }

  section {
    padding: 1.5rem;
  }
}
</style>

<script>
document.addEventListener('DOMContentLoaded', function() {
  // Randomize word cloud appearance
  const cloudWords = document.querySelectorAll('.cloud-word');
  const colors = ['#667eea', '#764ba2', '#f093fb', '#4facfe', '#43e97b'];

  cloudWords.forEach((word, index) => {
    const size = Math.random() * 2 + 0.5;
    const color = colors[Math.floor(Math.random() * colors.length)];
    word.style.setProperty('--size', size);
    word.style.setProperty('--color', color);
    word.style.animation = `float ${3 + Math.random() * 2}s ease-in-out infinite`;
    word.style.animationDelay = `${Math.random() * 2}s`;
  });

  // Add float animation
  const style = document.createElement('style');
  style.textContent = `
    @keyframes float {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-10px); }
    }
  `;
  document.head.appendChild(style);

  // Theme card interactions
  const themeCards = document.querySelectorAll('.theme-card');
  themeCards.forEach(card => {
    card.addEventListener('click', function() {
      const theme = this.dataset.theme;
      console.log('Theme clicked:', theme);
      // Could navigate to filtered view
    });
  });
});
</script>

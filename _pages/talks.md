---
layout: page
permalink: /talks/
title: talks
description: Invited talks, seminars, and conference presentations.
nav: true
nav_order: 3
---

<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<style>
  #talk-map { height: 420px; border-radius: 8px; margin-bottom: 1.5rem; }
  .talks-widget { position: relative; }
  .talks-list { max-height: 480px; overflow-y: auto; padding-right: 4px; }
  .talk-card {
    padding: 0.9rem 1rem;
    margin-bottom: 0.6rem;
    border: 1px solid rgba(128,128,128,0.25);
    border-radius: 6px;
    cursor: pointer;
    transition: background 0.2s, border-color 0.2s;
    display: flex;
    gap: 0.8rem;
    align-items: flex-start;
  }
  .talk-photo {
    width: 72px;
    height: 72px;
    object-fit: cover;
    border-radius: 6px;
    flex-shrink: 0;
  }
  .talk-card-text { flex: 1; min-width: 0; }
  .talk-links { margin-top: 0.3rem; }
  .talk-card:hover { background: rgba(128,128,128,0.08); }
  .talk-card.active { border-color: #6c63ff; background: rgba(108,99,255,0.08); }
  .talk-card h4 { margin: 0 0 0.2rem; font-size: 1rem; }
  .talk-card p { margin: 0 0 0.2rem; font-size: 0.9rem; }
  .talk-card a { font-size: 0.85rem; }
  .talks-controls { margin-bottom: 0.8rem; display: flex; align-items: center; gap: 0.6rem; }
  #talks-toggle {
    padding: 0.35rem 0.9rem;
    border-radius: 999px;
    border: 1px solid rgba(128,128,128,0.4);
    background: transparent;
    cursor: pointer;
    font-size: 0.85rem;
  }
</style>

<div class="talks-widget">
  <div id="talk-map"></div>

  <div class="talks-controls">
    <button id="talks-toggle">⏸ Pause auto-tour</button>
  </div>

  <div class="talks-list" id="talks-list">
    {% assign talks = site.data.talks | sort: "date" | reverse %}
    {% for talk in talks %}
    <div class="talk-card" data-index="{{ forloop.index0 }}">
      {% if talk.photo %}
        <img src="{{ talk.photo | relative_url }}" alt="{{ talk.title }}" class="talk-photo">
      {% endif %}
      <div class="talk-card-text">
        <h4>{{ talk.title }}</h4>
        <p><em>{{ talk.event }}</em></p>
        <p>{{ talk.venue }}, {{ talk.location }} &mdash; {{ talk.date | date: "%B %Y" }}</p>
        <p class="talk-links">
          {% if talk.slides %}<a href="{{ talk.slides | relative_url }}">slides</a>{% endif %}
          {% if talk.links %}
            {% for link in talk.links %}
              {% if talk.slides or forloop.first == false %} &middot; {% endif %}
              <a href="{{ link.url }}" target="_blank" rel="external nofollow noopener">{{ link.label }}</a>
            {% endfor %}
          {% endif %}
        </p>
      </div>
      <!-- <div class="talk-card-text">
        <h4>{{ talk.title }}</h4>
        <p><em>{{ talk.event }}</em></p>
        <p>{{ talk.venue }}, {{ talk.location }} &mdash; {{ talk.date | date: "%B %Y" }}</p>
        {% if talk.slides %}<a href="{{ talk.slides | relative_url }}">slides</a>{% endif %}
      </div> -->
    </div>
    {% endfor %}
  </div>
</div>

<script>
(function () {
  // Leaflet's default marker icons need explicit URLs when loaded via plain <script> tag
  delete L.Icon.Default.prototype._getIconUrl;
  L.Icon.Default.mergeOptions({
    iconRetinaUrl: 'https://unpkg.com/leaflet@1.9.4/dist/images/marker-icon-2x.png',
    iconUrl: 'https://unpkg.com/leaflet@1.9.4/dist/images/marker-icon.png',
    shadowUrl: 'https://unpkg.com/leaflet@1.9.4/dist/images/marker-shadow.png',
  });

  const talksData = [
    {% for talk in talks %}
    {
      title: {{ talk.title | jsonify }},
      event: {{ talk.event | jsonify }},
      venue: {{ talk.venue | jsonify }},
      location: {{ talk.location | jsonify }},
      date: {{ talk.date | date: "%Y-%m-%d" | jsonify }},
      lat: {{ talk.lat }},
      lng: {{ talk.lng }},
      slides: {% if talk.slides %}{{ talk.slides | relative_url | jsonify }}{% else %}null{% endif %},
      photo: {% if talk.photo %}{{ talk.photo | relative_url | jsonify }}{% else %}null{% endif %}
    }{% unless forloop.last %},{% endunless %}
    {% endfor %}
  ];

  const map = L.map('talk-map').setView([20, 10], 2);
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    attribution: '&copy; OpenStreetMap contributors',
    maxZoom: 18,
  }).addTo(map);

  const markers = talksData.map((t) => {
    const m = L.marker([t.lat, t.lng]).addTo(map);
    const popupPhoto = t.photo ? `<img src="${t.photo}" style="width:100%;max-height:160px;object-fit:cover;border-radius:4px;margin-top:6px;display:block;">` : '';
    m.bindPopup(`<strong>${t.title}</strong><br>${t.venue}, ${t.location}${popupPhoto}`, { maxWidth: 220 });
    return m;
  });

  if (talksData.length) {
    const bounds = L.latLngBounds(talksData.map((t) => [t.lat, t.lng]));
    map.fitBounds(bounds.pad(0.3));
  }

  const cards = Array.from(document.querySelectorAll('.talk-card'));
  const listEl = document.getElementById('talks-list');
  const widgetEl = document.querySelector('.talks-widget');
  const toggleBtn = document.getElementById('talks-toggle');

  let currentIndex = 0;
  let playing = true;
  let timer = null;

  function focusTalk(index) {
    currentIndex = index;
    cards.forEach((c) => c.classList.remove('active'));
    const card = cards[index];
    if (card) {
      card.classList.add('active');
      card.scrollIntoView({ block: 'nearest', behavior: 'smooth' });
    }
    const t = talksData[index];
    const targetZoom = 6;
    // Shift the map's center north of the marker in pixel space, so the marker
    // (and its popup, which opens above it) lands in the lower half of the
    // viewport instead of dead center — leaving room for tall popups.
    const markerPoint = map.project([t.lat, t.lng], targetZoom);
    const shiftedPoint = markerPoint.subtract([0, 130]);
    const targetLatLng = map.unproject(shiftedPoint, targetZoom);
    map.flyTo(targetLatLng, targetZoom, { duration: 1.2 });
    markers[index].openPopup();
  }

  function tick() {
    focusTalk((currentIndex + 1) % talksData.length);
  }

  function startAutoplay() {
    stopAutoplay();
    timer = setInterval(tick, 3500);
  }
  function stopAutoplay() {
    if (timer) clearInterval(timer);
    timer = null;
  }

  cards.forEach((card, i) => {
    card.addEventListener('click', () => focusTalk(i));
  });

  toggleBtn.addEventListener('click', () => {
    playing = !playing;
    toggleBtn.textContent = playing ? '⏸ Pause auto-tour' : '▶ Resume auto-tour';
    if (playing) startAutoplay();
    else stopAutoplay();
  });

  widgetEl.addEventListener('mouseenter', stopAutoplay);
  widgetEl.addEventListener('mouseleave', () => { if (playing) startAutoplay(); });

  if (talksData.length) {
    focusTalk(0);
    startAutoplay();
  }
})();
</script>
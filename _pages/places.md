---
layout: page
title: Places
permalink: /places/
---

<!--
  ╔══════════════════════════════════════════════════════════════════════╗
  ║  places.md  —  Places I recommend                                   ║
  ║                                                                      ║
  ║  TO ADD A PLACE — add a new object to the PLACES array below:       ║
  ║    name       → place name                                           ║
  ║    city       → city / region                                        ║
  ║    country    → country                                              ║
  ║    category   → 'cafe' | 'city' | 'trail' | 'restaurant' |          ║
  ║                 'hidden-gem' | 'coworking' | 'nature' | 'stay'       ║
  ║                 (any new string auto-appears as a filter)            ║
  ║    status     → 'been' | 'want-to-go'                                ║
  ║    oneliner   → one-sentence personal take                           ║
  ║    mapsUrl    → Google Maps share link, or "" to skip                ║
  ╚══════════════════════════════════════════════════════════════════════╝
-->

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,300;0,400;0,500;0,700&family=DM+Mono:wght@400;500&family=Playfair+Display:ital,wght@0,700;1,600&display=swap" rel="stylesheet">

<style>
  .pl-wrap * { box-sizing: border-box; margin: 0; padding: 0; }

  /* Design tokens */
  :root {
    --rc-gold:        #f0a500;
    --rc-gold-dim:    rgba(240,165,0,0.06);
    --rc-gold-border: rgba(240,165,0,0.25);
    --rc-text-bright: #f5f2eb;
    --rc-text-muted:  #6b6965;
    --rc-text-dim:    #4a4845;
    --rc-surface:     rgba(255,255,255,0.03);
    --rc-border:      rgba(255,255,255,0.06);
    --rc-border-h:    rgba(240,165,0,0.3);
    --rc-divider:     rgba(255,255,255,0.07);
  }
  html[data-mode="light"] {
    --rc-gold:        #b86e00;
    --rc-gold-dim:    rgba(184,110,0,0.05);
    --rc-gold-border: rgba(184,110,0,0.25);
    --rc-text-bright: #1a1916;
    --rc-text-muted:  #7a7875;
    --rc-text-dim:    #c0bebb;
    --rc-surface:     #f8f7f5;
    --rc-border:      rgba(0,0,0,0.08);
    --rc-border-h:    rgba(184,110,0,0.35);
    --rc-divider:     rgba(0,0,0,0.08);
  }

  .pl-wrap {
    font-family: 'DM Sans', sans-serif;
    max-width: 900px; margin: 0 auto; padding: 0 0 80px;
  }

  /* Header */
  .pl-header {
    padding: 48px 0 52px;
    border-bottom: 1px solid var(--rc-divider);
    margin-bottom: 48px;
    opacity: 0; animation: plUp 0.7s ease forwards 0.1s;
  }
  .pl-back {
    display: inline-flex; align-items: center; gap: 6px;
    font-family: 'DM Mono', monospace; font-size: 10px;
    letter-spacing: 0.15em; text-transform: uppercase;
    color: var(--rc-text-muted) !important; text-decoration: none !important;
    margin-bottom: 28px; transition: color 0.2s, gap 0.2s;
  }
  .pl-back:hover { color: var(--rc-gold) !important; gap: 10px; }
  .pl-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(36px, 6vw, 60px); font-weight: 700;
    line-height: 1.05; letter-spacing: -0.02em;
    color: var(--rc-text-bright); margin-bottom: 16px;
  }
  .pl-title em { font-style: italic; color: var(--rc-gold); }
  .pl-subtitle { font-size: 15px; line-height: 1.7; color: var(--rc-text-muted); font-weight: 300; max-width: 520px; }

  /* Stats */
  .pl-stats {
    display: flex; gap: 32px; flex-wrap: wrap;
    margin-bottom: 44px; opacity: 0;
    animation: plUp 0.6s ease forwards 0.25s;
  }
  .pl-stat-n { font-family: 'Playfair Display', serif; font-size: 30px; font-weight: 700; color: var(--rc-text-bright); line-height: 1; margin-bottom: 3px; }
  .pl-stat-n span { font-size: 15px; color: var(--rc-gold); }
  .pl-stat-l { font-family: 'DM Mono', monospace; font-size: 9px; letter-spacing: 0.15em; text-transform: uppercase; color: var(--rc-text-dim); }

  /* Filters */
  .pl-filters {
    display: flex; gap: 8px; flex-wrap: wrap;
    margin-bottom: 40px; opacity: 0;
    animation: plUp 0.6s ease forwards 0.35s;
  }
  .pl-filter {
    font-family: 'DM Mono', monospace; font-size: 10px;
    letter-spacing: 0.1em; text-transform: uppercase;
    padding: 7px 14px; border: 1px solid var(--rc-border);
    background: transparent; color: var(--rc-text-muted); cursor: pointer;
    transition: all 0.2s ease;
  }
  .pl-filter:hover, .pl-filter.active {
    border-color: var(--rc-border-h); color: var(--rc-gold);
    background: var(--rc-gold-dim);
  }

  /* Grid */
  .pl-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(260px, 1fr)); gap: 20px; }
  @media (max-width: 480px) { .pl-grid { grid-template-columns: 1fr; } }

  /* Card */
  .pl-card {
    background: var(--rc-surface); border: 1px solid var(--rc-border);
    padding: 22px 24px; display: flex; flex-direction: column; gap: 14px;
    transition: all 0.25s ease; opacity: 0; animation: plUp 0.5s ease forwards;
  }
  .pl-card:hover {
    background: rgba(255,255,255,0.06); border-color: var(--rc-border-h);
    transform: translateY(-4px); box-shadow: 0 20px 48px rgba(0,0,0,0.3);
  }
  .pl-card.hidden { display: none; }
  html[data-mode="light"] .pl-card { background: #f8f7f5; border-color: rgba(0,0,0,0.08); }
  html[data-mode="light"] .pl-card:hover { background: #f0ede8; border-color: rgba(184,110,0,0.35); box-shadow: 0 16px 40px rgba(0,0,0,0.1); }

  .pl-card-top { display: flex; align-items: flex-start; gap: 14px; }
  .pl-icon {
    font-size: 22px; width: 44px; height: 44px; flex-shrink: 0;
    display: flex; align-items: center; justify-content: center;
    background: var(--rc-gold-dim); border: 1px solid var(--rc-gold-border);
  }
  .pl-card-identity { flex: 1; min-width: 0; }
  .pl-name { font-size: 15px; font-weight: 500; color: var(--rc-text-bright); margin-bottom: 4px; line-height: 1.3; }
  html[data-mode="light"] .pl-name { color: #1a1916; }
  .pl-location { font-family: 'DM Mono', monospace; font-size: 10px; letter-spacing: 0.05em; color: var(--rc-text-dim); }
  html[data-mode="light"] .pl-location { color: #9a9895; }

  /* Badge */
  .pl-badge {
    display: inline-flex; align-items: center; gap: 4px;
    font-family: 'DM Mono', monospace; font-size: 9px;
    letter-spacing: 0.1em; text-transform: uppercase;
    padding: 3px 8px; width: fit-content;
  }
  .pl-badge-been    { background: rgba(34,197,94,0.1);   color: #4ade80; border: 1px solid rgba(34,197,94,0.2); }
  .pl-badge-want    { background: rgba(148,163,184,0.1); color: #94a3b8; border: 1px solid rgba(148,163,184,0.2); }
  html[data-mode="light"] .pl-badge-been { background: rgba(22,163,74,0.08); color: #16a34a; border-color: rgba(22,163,74,0.2); }
  html[data-mode="light"] .pl-badge-want { background: rgba(100,116,139,0.08); color: #64748b; border-color: rgba(100,116,139,0.2); }

  .pl-oneliner {
    font-size: 13px; line-height: 1.65; color: var(--rc-text-muted); font-weight: 300;
    border-left: 2px solid var(--rc-gold-border); padding-left: 12px;
  }
  html[data-mode="light"] .pl-oneliner { color: #6b6865; }

  .pl-maps-link {
    display: inline-flex; align-items: center; gap: 6px;
    font-family: 'DM Mono', monospace; font-size: 9px;
    letter-spacing: 0.12em; text-transform: uppercase;
    color: var(--rc-gold) !important; text-decoration: none !important;
    border-bottom: 1px solid var(--rc-gold-border); padding-bottom: 1px;
    width: fit-content; transition: all 0.2s ease;
  }
  .pl-maps-link:hover { border-color: var(--rc-gold); gap: 9px; }

  /* Empty state */
  .pl-empty {
    display: none; grid-column: 1/-1; text-align: center; padding: 48px 0;
    font-family: 'DM Mono', monospace; font-size: 12px; letter-spacing: 0.1em;
    color: var(--rc-text-dim); text-transform: uppercase;
  }

  @keyframes plUp { from { opacity: 0; transform: translateY(14px); } to { opacity: 1; transform: translateY(0); } }
</style>

<div class="pl-wrap">

  <div class="pl-header">
    <a href="/recommendations/" class="pl-back"><i class="fas fa-arrow-left"></i> Back to Recommendations</a>
    <h1 class="pl-title">Places Worth <em>Going.</em></h1>
    <p class="pl-subtitle">Cafes, cities, trails and hidden corners — spots I've been to or genuinely want to visit.</p>
  </div>

  <div class="pl-stats" id="pl-stats"></div>
  <div class="pl-filters" id="pl-filters"></div>

  <div class="pl-grid" id="pl-grid">
    <div class="pl-empty" id="pl-empty">No places in this category yet.</div>
  </div>

</div>

<script>
/*
  ══════════════════════════════════════════════════════════════════════
  PLACES DATA — edit this list to add / update places
  ══════════════════════════════════════════════════════════════════════
*/
var PLACES = [

  {
    name:     "Cubbon Park",
    city:     "Bengaluru",
    country:  "India",
    category: "nature",
    status:   "been",
    oneliner: "Best place in Bengaluru to run, breathe, and reset when the city gets too loud.",
    mapsUrl:  ""
  }

  /*
  ── Add more places below ─────────────────────────────────────────────
  ,{
    name:     "Third Wave Coffee",
    city:     "Bengaluru",
    country:  "India",
    category: "cafe",
    status:   "been",
    oneliner: "My default work cafe — great filter coffee, calm vibe, fast wifi.",
    mapsUrl:  ""
  }
  ,{
    name:     "Hampi",
    city:     "Karnataka",
    country:  "India",
    category: "hidden-gem",
    status:   "been",
    oneliner: "Ruins, boulders and a river. Feels like stepping into another era.",
    mapsUrl:  ""
  }
  ,{
    name:     "Kyoto",
    city:     "Kyoto",
    country:  "Japan",
    category: "city",
    status:   "want-to-go",
    oneliner: "Everything I've read and seen tells me this is a place I need to experience once.",
    mapsUrl:  ""
  }
  ──────────────────────────────────────────────────────────────────── */
];

/* ── Renderer — no need to edit below ── */
(function () {
  var CAT_LABELS = {
    'cafe': 'Cafe', 'city': 'City', 'trail': 'Trail', 'restaurant': 'Restaurant',
    'hidden-gem': 'Hidden Gem', 'coworking': 'Cowork', 'nature': 'Nature', 'stay': 'Stay'
  };
  var CAT_ICONS = {
    'cafe': '☕', 'city': '🌆', 'trail': '🥾', 'restaurant': '🍽️',
    'hidden-gem': '💎', 'coworking': '💻', 'nature': '🌿', 'stay': '🏡'
  };
  function catLabel(c) { return CAT_LABELS[c] || (c.charAt(0).toUpperCase() + c.slice(1)); }
  function catIcon(c)  { return CAT_ICONS[c]  || '📍'; }

  /* Stats */
  var been = PLACES.filter(function(p){ return p.status === 'been'; }).length;
  var want = PLACES.filter(function(p){ return p.status === 'want-to-go'; }).length;
  var sh = '<div><p class="pl-stat-n">' + PLACES.length + '</p><p class="pl-stat-l">Total</p></div>';
  if (been > 0) sh += '<div><p class="pl-stat-n">' + been + '</p><p class="pl-stat-l">Been</p></div>';
  if (want > 0) sh += '<div><p class="pl-stat-n">' + want + '</p><p class="pl-stat-l">Want to go</p></div>';
  document.getElementById('pl-stats').innerHTML = sh;

  /* Filters */
  var cats = {};
  PLACES.forEach(function(p){ cats[p.category] = (cats[p.category] || 0) + 1; });
  var catKeys = ['all'].concat(Object.keys(cats));
  var filtersEl = document.getElementById('pl-filters');
  filtersEl.innerHTML = catKeys.map(function(c){
    return '<button class="pl-filter' + (c==='all'?' active':'') + '" data-cat="' + c + '">' + (c==='all'?'All':catLabel(c)) + '</button>';
  }).join('');

  var activeFilter = 'all';
  filtersEl.addEventListener('click', function(e){
    var btn = e.target.closest('.pl-filter');
    if (!btn) return;
    activeFilter = btn.getAttribute('data-cat');
    filtersEl.querySelectorAll('.pl-filter').forEach(function(b){ b.classList.remove('active'); });
    btn.classList.add('active');
    applyFilter();
  });

  /* Cards */
  var grid = document.getElementById('pl-grid');
  var emptyEl = document.getElementById('pl-empty');

  PLACES.forEach(function(p, i){
    var badgeCls = p.status === 'been' ? 'pl-badge-been' : 'pl-badge-want';
    var badgeTxt = p.status === 'been' ? '✓ Been' : '○ Want to go';
    var mapsHtml = p.mapsUrl
      ? '<a href="' + p.mapsUrl + '" class="pl-maps-link" target="_blank" rel="noopener"><i class="fas fa-map-marker-alt"></i> Open in Maps</a>'
      : '';
    var card = document.createElement('div');
    card.className = 'pl-card';
    card.setAttribute('data-cat', p.category);
    card.style.animationDelay = (0.05 * i) + 's';
    card.innerHTML =
      '<div class="pl-card-top">'
      + '<div class="pl-icon">' + catIcon(p.category) + '</div>'
      + '<div class="pl-card-identity"><p class="pl-name">' + p.name + '</p><p class="pl-location">' + p.city + ', ' + p.country + '</p></div>'
      + '</div>'
      + '<span class="pl-badge ' + badgeCls + '">' + badgeTxt + '</span>'
      + '<p class="pl-oneliner">' + p.oneliner + '</p>'
      + mapsHtml;
    grid.insertBefore(card, emptyEl);
  });

  function applyFilter(){
    var cards = grid.querySelectorAll('.pl-card');
    var visible = 0;
    cards.forEach(function(c){
      var match = activeFilter === 'all' || c.getAttribute('data-cat') === activeFilter;
      c.classList.toggle('hidden', !match);
      if (match) visible++;
    });
    emptyEl.style.display = visible === 0 ? 'block' : 'none';
  }
})();
</script>

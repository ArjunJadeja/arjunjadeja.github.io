---
layout: page
title: Things
permalink: /things/
---

<!--
  ╔══════════════════════════════════════════════════════════════════════╗
  ║  things.md  —  Objects, tools and gear I genuinely recommend        ║
  ║                                                                      ║
  ║  TO ADD A THING — add a new object to the THINGS array below:       ║
  ║    name       → product / item name                                  ║
  ║    brand      → brand name, or "" if not applicable                  ║
  ║    category   → 'tech' | 'fitness' | 'desk' | 'kitchen' |           ║
  ║                 'reading' | 'carry' | 'skincare' | 'audio'           ║
  ║                 (any new string auto-appears as a filter)            ║
  ║    owned      → true = own it, false = wishlist                      ║
  ║    rating     → 1–5 stars shown in gold. 0 = no rating yet          ║
  ║    oneliner   → one honest sentence                                  ║
  ║    url        → product link, or "" to skip                          ║
  ╚══════════════════════════════════════════════════════════════════════╝
-->

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,300;0,400;0,500;0,700&family=DM+Mono:wght@400;500&family=Playfair+Display:ital,wght@0,700;1,600&display=swap" rel="stylesheet">

<style>
  .th-wrap * { box-sizing: border-box; margin: 0; padding: 0; }

  /* Design tokens */
  :root {
    --rc-gold:        #f0a500;
    --rc-gold-dim:    rgba(240,165,0,0.06);
    --rc-gold-border: rgba(240,165,0,0.25);
    --rc-text-bright: #f5f2eb;
    --rc-text-muted:  #6b6965;
    --rc-text-dim:    #4a4845;
    --rc-text-ghost:  #3a3835;
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
    --rc-text-ghost:  #c0bebb;
    --rc-surface:     #f8f7f5;
    --rc-border:      rgba(0,0,0,0.08);
    --rc-border-h:    rgba(184,110,0,0.35);
    --rc-divider:     rgba(0,0,0,0.08);
  }

  .th-wrap {
    font-family: 'DM Sans', sans-serif;
    max-width: 900px; margin: 0 auto; padding: 0 0 80px;
  }

  /* Header */
  .th-header {
    padding: 48px 0 52px; border-bottom: 1px solid var(--rc-divider);
    margin-bottom: 48px; opacity: 0; animation: thUp 0.7s ease forwards 0.1s;
  }
  .th-back {
    display: inline-flex; align-items: center; gap: 6px;
    font-family: 'DM Mono', monospace; font-size: 10px;
    letter-spacing: 0.15em; text-transform: uppercase;
    color: var(--rc-text-muted) !important; text-decoration: none !important;
    margin-bottom: 28px; transition: color 0.2s, gap 0.2s;
  }
  .th-back:hover { color: var(--rc-gold) !important; gap: 10px; }
  .th-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(36px, 6vw, 60px); font-weight: 700;
    line-height: 1.05; letter-spacing: -0.02em;
    color: var(--rc-text-bright); margin-bottom: 16px;
  }
  .th-title em { font-style: italic; color: var(--rc-gold); }
  .th-subtitle { font-size: 15px; line-height: 1.7; color: var(--rc-text-muted); font-weight: 300; max-width: 520px; }

  /* Stats */
  .th-stats {
    display: flex; gap: 32px; flex-wrap: wrap;
    margin-bottom: 44px; opacity: 0; animation: thUp 0.6s ease forwards 0.25s;
  }
  .th-stat-n { font-family: 'Playfair Display', serif; font-size: 30px; font-weight: 700; color: var(--rc-text-bright); line-height: 1; margin-bottom: 3px; }
  .th-stat-n span { font-size: 15px; color: var(--rc-gold); }
  .th-stat-l { font-family: 'DM Mono', monospace; font-size: 9px; letter-spacing: 0.15em; text-transform: uppercase; color: var(--rc-text-dim); }

  /* Filters */
  .th-filters {
    display: flex; gap: 8px; flex-wrap: wrap;
    margin-bottom: 40px; opacity: 0; animation: thUp 0.6s ease forwards 0.35s;
  }
  .th-filter {
    font-family: 'DM Mono', monospace; font-size: 10px;
    letter-spacing: 0.1em; text-transform: uppercase;
    padding: 7px 14px; border: 1px solid var(--rc-border);
    background: transparent; color: var(--rc-text-muted); cursor: pointer;
    transition: all 0.2s ease;
  }
  .th-filter:hover, .th-filter.active {
    border-color: var(--rc-border-h); color: var(--rc-gold); background: var(--rc-gold-dim);
  }

  /* Grid */
  .th-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(240px, 1fr)); gap: 20px; }
  @media (max-width: 480px) { .th-grid { grid-template-columns: 1fr; } }

  /* Card */
  .th-card {
    background: var(--rc-surface); border: 1px solid var(--rc-border);
    padding: 22px 24px; display: flex; flex-direction: column; gap: 14px;
    transition: all 0.25s ease; opacity: 0; animation: thUp 0.5s ease forwards;
  }
  .th-card:hover {
    background: rgba(255,255,255,0.06); border-color: var(--rc-border-h);
    transform: translateY(-4px); box-shadow: 0 20px 48px rgba(0,0,0,0.3);
  }
  .th-card.hidden { display: none; }
  html[data-mode="light"] .th-card { background: #f8f7f5; border-color: rgba(0,0,0,0.08); }
  html[data-mode="light"] .th-card:hover { background: #f0ede8; border-color: rgba(184,110,0,0.35); box-shadow: 0 16px 40px rgba(0,0,0,0.1); }

  .th-card-top { display: flex; align-items: flex-start; gap: 14px; }
  .th-icon {
    font-size: 22px; width: 44px; height: 44px; flex-shrink: 0;
    display: flex; align-items: center; justify-content: center;
    background: var(--rc-gold-dim); border: 1px solid var(--rc-gold-border);
  }
  .th-card-identity { flex: 1; min-width: 0; }
  .th-name { font-size: 15px; font-weight: 500; color: var(--rc-text-bright); margin-bottom: 3px; line-height: 1.3; }
  html[data-mode="light"] .th-name { color: #1a1916; }
  .th-brand { font-family: 'DM Mono', monospace; font-size: 10px; letter-spacing: 0.05em; color: var(--rc-text-dim); }
  html[data-mode="light"] .th-brand { color: #9a9895; }

  /* Badge */
  .th-badge {
    display: inline-flex; align-items: center; gap: 4px;
    font-family: 'DM Mono', monospace; font-size: 9px;
    letter-spacing: 0.1em; text-transform: uppercase;
    padding: 3px 8px; width: fit-content;
  }
  .th-badge-own  { background: rgba(34,197,94,0.1);   color: #4ade80; border: 1px solid rgba(34,197,94,0.2); }
  .th-badge-want { background: rgba(148,163,184,0.1); color: #94a3b8; border: 1px solid rgba(148,163,184,0.2); }
  html[data-mode="light"] .th-badge-own  { background: rgba(22,163,74,0.08);  color: #16a34a; border-color: rgba(22,163,74,0.2); }
  html[data-mode="light"] .th-badge-want { background: rgba(100,116,139,0.08); color: #64748b; border-color: rgba(100,116,139,0.2); }

  /* Stars */
  .th-stars { display: flex; gap: 2px; }
  .th-star { font-size: 11px; color: var(--rc-text-ghost); }
  .th-star.on { color: var(--rc-gold); }
  html[data-mode="light"] .th-star { color: #d0ccc8; }
  html[data-mode="light"] .th-star.on { color: #b86e00; }

  .th-oneliner {
    font-size: 13px; line-height: 1.65; color: var(--rc-text-muted); font-weight: 300;
    border-left: 2px solid var(--rc-gold-border); padding-left: 12px;
  }
  html[data-mode="light"] .th-oneliner { color: #6b6865; }

  .th-link {
    display: inline-flex; align-items: center; gap: 6px;
    font-family: 'DM Mono', monospace; font-size: 9px;
    letter-spacing: 0.12em; text-transform: uppercase;
    color: var(--rc-gold) !important; text-decoration: none !important;
    border-bottom: 1px solid var(--rc-gold-border); padding-bottom: 1px;
    width: fit-content; transition: all 0.2s ease;
  }
  .th-link:hover { border-color: var(--rc-gold); gap: 9px; }

  /* Empty */
  .th-empty {
    display: none; grid-column: 1/-1; text-align: center; padding: 48px 0;
    font-family: 'DM Mono', monospace; font-size: 12px; letter-spacing: 0.1em;
    color: var(--rc-text-dim); text-transform: uppercase;
  }

  @keyframes thUp { from { opacity: 0; transform: translateY(14px); } to { opacity: 1; transform: translateY(0); } }
</style>

<div class="th-wrap">

  <div class="th-header">
    <a href="/recommendations/" class="th-back"><i class="fas fa-arrow-left"></i> Back to Recommendations</a>
    <h1 class="th-title">Things I <em>Recommend.</em></h1>
    <p class="th-subtitle">Objects, tools and gear I actually use — no sponsorships, no affiliate deals. Just honest picks.</p>
  </div>

  <div class="th-stats" id="th-stats"></div>
  <div class="th-filters" id="th-filters"></div>

  <div class="th-grid" id="th-grid">
    <div class="th-empty" id="th-empty">No things in this category yet.</div>
  </div>

</div>

<script>
/*
  ══════════════════════════════════════════════════════════════════════
  THINGS DATA — edit this list to add / update items
  ══════════════════════════════════════════════════════════════════════
*/
var THINGS = [

  {
    name:     "Kindle Paperwhite",
    brand:    "Amazon",
    category: "reading",
    owned:    true,
    rating:   5,
    oneliner: "Best thing I ever bought for reading. Lightweight, no distractions, weeks of battery life.",
    url:      ""
  },
  {
    name:     "Foam Roller",
    brand:    "",
    category: "fitness",
    owned:    true,
    rating:   4,
    oneliner: "Non-negotiable for recovery after long runs. Legs thank me every time.",
    url:      ""
  }

  /*
  ── Add more things below ─────────────────────────────────────────────
  ,{
    name:     "Keychron K2",
    brand:    "Keychron",
    category: "desk",
    owned:    true,
    rating:   5,
    oneliner: "Compact mechanical keyboard that made typing feel like a joy again.",
    url:      "https://keychron.com"
  }
  ,{
    name:     "Sony WH-1000XM5",
    brand:    "Sony",
    category: "audio",
    owned:    false,
    rating:   0,
    oneliner: "On the wishlist — best-in-class noise cancellation for deep work sessions.",
    url:      ""
  }
  ──────────────────────────────────────────────────────────────────── */
];

/* ── Renderer — no need to edit below ── */
(function () {
  var CAT_LABELS = {
    'tech': 'Tech', 'fitness': 'Fitness', 'desk': 'Desk', 'kitchen': 'Kitchen',
    'reading': 'Reading', 'carry': 'Carry', 'skincare': 'Skincare', 'audio': 'Audio'
  };
  var CAT_ICONS = {
    'tech': '💻', 'fitness': '🏃', 'desk': '🖥️', 'kitchen': '🍳',
    'reading': '📖', 'carry': '🎒', 'skincare': '🧴', 'audio': '🎧'
  };
  function catLabel(c) { return CAT_LABELS[c] || (c.charAt(0).toUpperCase() + c.slice(1)); }
  function catIcon(c)  { return CAT_ICONS[c]  || '📦'; }

  function starsHtml(r) {
    if (!r) return '';
    var h = '<div class="th-stars">';
    for (var i = 1; i <= 5; i++) h += '<span class="th-star' + (i <= r ? ' on' : '') + '">★</span>';
    return h + '</div>';
  }

  /* Stats */
  var owned = THINGS.filter(function(t){ return t.owned; }).length;
  var want  = THINGS.filter(function(t){ return !t.owned; }).length;
  var sh = '<div><p class="th-stat-n">' + THINGS.length + '</p><p class="th-stat-l">Total</p></div>';
  if (owned > 0) sh += '<div><p class="th-stat-n">' + owned + '</p><p class="th-stat-l">Own it</p></div>';
  if (want  > 0) sh += '<div><p class="th-stat-n">' + want  + '</p><p class="th-stat-l">Wishlist</p></div>';
  document.getElementById('th-stats').innerHTML = sh;

  /* Filters */
  var cats = {};
  THINGS.forEach(function(t){ cats[t.category] = (cats[t.category] || 0) + 1; });
  var catKeys = ['all'].concat(Object.keys(cats));
  var filtersEl = document.getElementById('th-filters');
  filtersEl.innerHTML = catKeys.map(function(c){
    return '<button class="th-filter' + (c==='all'?' active':'') + '" data-cat="' + c + '">' + (c==='all'?'All':catLabel(c)) + '</button>';
  }).join('');

  var activeFilter = 'all';
  filtersEl.addEventListener('click', function(e){
    var btn = e.target.closest('.th-filter');
    if (!btn) return;
    activeFilter = btn.getAttribute('data-cat');
    filtersEl.querySelectorAll('.th-filter').forEach(function(b){ b.classList.remove('active'); });
    btn.classList.add('active');
    applyFilter();
  });

  /* Cards */
  var grid = document.getElementById('th-grid');
  var emptyEl = document.getElementById('th-empty');

  THINGS.forEach(function(t, i){
    var badgeCls = t.owned ? 'th-badge-own' : 'th-badge-want';
    var badgeTxt = t.owned ? '✓ Own it' : '○ Wishlist';
    var linkHtml = t.url
      ? '<a href="' + t.url + '" class="th-link" target="_blank" rel="noopener"><i class="fas fa-external-link-alt"></i> View product</a>'
      : '';
    var card = document.createElement('div');
    card.className = 'th-card';
    card.setAttribute('data-cat', t.category);
    card.style.animationDelay = (0.05 * i) + 's';
    card.innerHTML =
      '<div class="th-card-top">'
      + '<div class="th-icon">' + catIcon(t.category) + '</div>'
      + '<div class="th-card-identity"><p class="th-name">' + t.name + '</p>' + (t.brand ? '<p class="th-brand">' + t.brand + '</p>' : '') + '</div>'
      + '</div>'
      + '<span class="th-badge ' + badgeCls + '">' + badgeTxt + '</span>'
      + starsHtml(t.rating)
      + '<p class="th-oneliner">' + t.oneliner + '</p>'
      + linkHtml;
    grid.insertBefore(card, emptyEl);
  });

  function applyFilter(){
    var cards = grid.querySelectorAll('.th-card');
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

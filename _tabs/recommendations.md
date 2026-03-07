---
layout: page
title: Recommendations
icon: fas fa-star
order: 4
---

<!--
  ╔══════════════════════════════════════════════════════════════════════╗
  ║  recommendations.md  —  Hub page for all recommendation sub-pages   ║
  ║                                                                      ║
  ║  TO ADD A NEW CATEGORY:                                              ║
  ║    Add a new object to the CATEGORIES array in the <script> below.  ║
  ╚══════════════════════════════════════════════════════════════════════╝
-->

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,300;0,400;0,500;0,700&family=DM+Mono:wght@400;500&family=Playfair+Display:ital,wght@0,700;1,600&display=swap" rel="stylesheet">

<style>
  .rc-wrap * { box-sizing: border-box; margin: 0; padding: 0; }

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

  .rc-wrap {
    font-family: 'DM Sans', sans-serif;
    max-width: 900px;
    margin: 0 auto;
    padding: 0 0 80px;
  }

  /* Hero */
  .rh-hero {
    padding: 56px 0 52px;
    border-bottom: 1px solid var(--rc-divider);
    margin-bottom: 64px;
  }
  .rh-eyebrow {
    font-family: 'DM Mono', monospace;
    font-size: 11px; letter-spacing: 0.2em; text-transform: uppercase;
    color: var(--rc-gold); margin-bottom: 18px;
    opacity: 0; animation: rcUp 0.6s ease forwards 0.1s;
  }
  .rh-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(44px, 7vw, 72px);
    font-weight: 700; line-height: 1.04; letter-spacing: -0.02em;
    color: var(--rc-text-bright); margin-bottom: 20px;
    opacity: 0; animation: rcUp 0.7s ease forwards 0.2s;
  }
  .rh-title em { font-style: italic; color: var(--rc-gold); }
  .rh-intro {
    font-size: 16px; line-height: 1.8; color: var(--rc-text-muted);
    max-width: 540px; font-weight: 300;
    opacity: 0; animation: rcUp 0.7s ease forwards 0.35s;
  }

  /* Grid */
  .rh-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
    gap: 20px;
    opacity: 0; animation: rcUp 0.7s ease forwards 0.5s;
  }
  @media (max-width: 560px) { .rh-grid { grid-template-columns: 1fr; } }

  /* Card */
  .rh-card {
    background: var(--rc-surface);
    border: 1px solid var(--rc-border);
    padding: 32px 28px;
    text-decoration: none !important;
    display: flex; flex-direction: column; gap: 20px;
    transition: all 0.25s ease;
    position: relative; overflow: hidden;
  }
  .rh-card::after {
    content: ''; position: absolute; bottom: 0; left: 0;
    width: 0; height: 2px; background: var(--rc-gold);
    transition: width 0.3s ease;
  }
  .rh-card:hover {
    background: rgba(255,255,255,0.055);
    border-color: var(--rc-border-h);
    transform: translateY(-5px);
    box-shadow: 0 20px 48px rgba(0,0,0,0.3);
    text-decoration: none !important;
  }
  .rh-card:hover::after { width: 100%; }
  html[data-mode="light"] .rh-card { background: #f8f7f5; border-color: rgba(0,0,0,0.08); }
  html[data-mode="light"] .rh-card:hover { background: #f0ede8; border-color: rgba(184,110,0,0.35); box-shadow: 0 16px 40px rgba(0,0,0,0.1); }

  .rh-card-icon {
    font-size: 28px; width: 52px; height: 52px;
    display: flex; align-items: center; justify-content: center;
    background: var(--rc-gold-dim); border: 1px solid var(--rc-gold-border);
    transition: background 0.2s;
  }
  .rh-card:hover .rh-card-icon { background: rgba(240,165,0,0.1); }

  .rh-card-title {
    font-family: 'Playfair Display', serif;
    font-size: 22px; font-weight: 700;
    color: var(--rc-text-bright); margin-bottom: 8px; line-height: 1.2;
  }
  .rh-card-desc { font-size: 13px; line-height: 1.65; color: var(--rc-text-muted); font-weight: 300; }

  .rh-card-stats {
    display: flex; gap: 16px; flex-wrap: wrap;
    border-top: 1px solid var(--rc-divider);
    padding-top: 16px; margin-top: auto;
  }
  .rh-card-stat-n {
    font-family: 'Playfair Display', serif;
    font-size: 20px; font-weight: 700;
    color: var(--rc-text-bright); line-height: 1; margin-bottom: 2px;
  }
  .rh-card-stat-n span { font-size: 12px; color: var(--rc-gold); }
  .rh-card-stat-l {
    font-family: 'DM Mono', monospace; font-size: 8px;
    letter-spacing: 0.12em; text-transform: uppercase; color: var(--rc-text-dim);
  }

  .rh-card-arrow {
    position: absolute; top: 28px; right: 28px;
    font-family: 'DM Mono', monospace; font-size: 10px;
    color: var(--rc-gold); opacity: 0; transform: translateX(-6px);
    transition: all 0.25s ease;
  }
  .rh-card:hover .rh-card-arrow { opacity: 1; transform: translateX(0); }

  @keyframes rcUp {
    from { opacity: 0; transform: translateY(14px); }
    to   { opacity: 1; transform: translateY(0); }
  }
</style>

<div class="rc-wrap">
  <div class="rh-hero">
    <p class="rh-eyebrow">// things worth your time</p>
    <h1 class="rh-title">My <em>Recommendations.</em></h1>
    <p class="rh-intro">
      Not curated to impress — just things that genuinely made a difference.
      Books that rewired how I think, people who raised the bar, places and objects I keep coming back to.
    </p>
  </div>
  <div class="rh-grid" id="rh-grid"></div>
</div>

<script>
/*
  ══════════════════════════════════════════════════════════════════════
  CATEGORIES CONFIG — edit to add / update category cards
  ══════════════════════════════════════════════════════════════════════
  Fields:
    icon   → emoji in the icon box
    title  → card heading
    desc   → one-line description
    href   → URL of the sub-page
    stats  → array of { n, label } — update n manually when you add items
  ══════════════════════════════════════════════════════════════════════
*/
var CATEGORIES = [
  {
    icon:  "📚",
    title: "Reading",
    desc:  "Books I've read, am reading, or plan to — with honest one-liners on each.",
    href:  "/reading/",
    stats: [{ n: "4", label: "Read" }, { n: "2", label: "Reading" }]
  },
  {
    icon:  "🎬",
    title: "Watching",
    desc:  "Movies and shows that left a mark — or at least kept me up past midnight.",
    href:  "/watching/",
    stats: [{ n: "30+", label: "Watched" }, { n: "2", label: "Watching" }]
  },
  {
    icon:  "🙌",
    title: "People",
    desc:  "People who've shaped how I think, work, run, and live. A genuine list.",
    href:  "/people/",
    stats: [{ n: "3", label: "People" }]
  },
  {
    icon:  "📍",
    title: "Places",
    desc:  "Spots worth visiting — cafes, cities, trails and hidden corners I keep returning to.",
    href:  "/places/",
    stats: [{ n: "—", label: "Coming soon" }]
  },
  {
    icon:  "🎒",
    title: "Things",
    desc:  "Objects, tools and gear I actually use and would genuinely recommend.",
    href:  "/things/",
    stats: [{ n: "—", label: "Coming soon" }]
  }
];

(function () {
  var grid = document.getElementById('rh-grid');
  CATEGORIES.forEach(function (cat, i) {
    var statsHtml = cat.stats.map(function (s) {
      return '<div><p class="rh-card-stat-n">' + s.n + '</p><p class="rh-card-stat-l">' + s.label + '</p></div>';
    }).join('');
    var card = document.createElement('a');
    card.className = 'rh-card';
    card.href = cat.href;
    card.style.animationDelay = (0.08 * i) + 's';
    card.innerHTML =
      '<span class="rh-card-arrow">↗</span>'
      + '<div class="rh-card-icon">' + cat.icon + '</div>'
      + '<div><p class="rh-card-title">' + cat.title + '</p><p class="rh-card-desc">' + cat.desc + '</p></div>'
      + '<div class="rh-card-stats">' + statsHtml + '</div>';
    grid.appendChild(card);
  });
})();
</script>

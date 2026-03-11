---
layout: page
title: Watching
permalink: /watching/
---

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,300;0,400;0,500;0,700&family=DM+Mono:wght@400;500&family=Playfair+Display:ital,wght@0,700;1,600&display=swap" rel="stylesheet">

<style>
  .wt-wrap * { box-sizing: border-box; margin: 0; padding: 0; }
  .wt-wrap {
    font-family: 'DM Sans', sans-serif;
    max-width: 900px;
    margin: 0 auto;
    padding: 0 0 80px;
  }

  /* ── Header ── */
  .wt-header {
    padding: 48px 0 52px;
    border-bottom: 1px solid rgba(255,255,255,0.07);
    margin-bottom: 48px;
    opacity: 0;
    animation: wtUp 0.7s ease forwards 0.1s;
  }
  .wt-back {
    display: inline-flex; align-items: center; gap: 6px;
    font-family: 'DM Mono', monospace; font-size: 10px;
    letter-spacing: 0.15em; text-transform: uppercase;
    color: #6b6965 !important; text-decoration: none !important;
    margin-bottom: 28px; transition: color 0.2s, gap 0.2s;
  }
  .wt-back:hover { color: #f0a500 !important; gap: 10px; }
  .wt-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(36px, 6vw, 60px);
    font-weight: 700; line-height: 1.05;
    letter-spacing: -0.02em; color: #f5f2eb;
    margin-bottom: 16px;
  }
  .wt-title em { font-style: italic; color: #f0a500; }
  .wt-subtitle { font-size: 15px; line-height: 1.7; color: #6b6965; font-weight: 300; max-width: 520px; }

  /* ── Stats ── */
  .wt-stats {
    display: flex; gap: 32px; flex-wrap: wrap;
    margin-bottom: 44px; opacity: 0;
    animation: wtUp 0.6s ease forwards 0.25s;
  }
  .wt-stat-n { font-family: 'Playfair Display', serif; font-size: 30px; font-weight: 700; color: #f5f2eb; line-height: 1; margin-bottom: 3px; }
  .wt-stat-n span { font-size: 15px; color: #f0a500; }
  .wt-stat-l { font-family: 'DM Mono', monospace; font-size: 9px; letter-spacing: 0.15em; text-transform: uppercase; color: #3a3835; }

  /* ── Filters ── */
  .wt-filters {
    display: flex; gap: 8px; flex-wrap: wrap;
    margin-bottom: 40px; opacity: 0;
    animation: wtUp 0.6s ease forwards 0.35s;
  }
  .wt-filter {
    font-family: 'DM Mono', monospace; font-size: 10px;
    letter-spacing: 0.1em; text-transform: uppercase;
    padding: 7px 14px; border: 1px solid rgba(255,255,255,0.08);
    background: transparent; color: #6b6965; cursor: pointer;
    transition: all 0.2s ease;
  }
  .wt-filter:hover, .wt-filter.active {
    border-color: rgba(240,165,0,0.35); color: #f0a500;
    background: rgba(240,165,0,0.06);
  }

  /* ── Grid ── */
  .wt-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
    gap: 20px;
  }
  @media (max-width: 480px) { .wt-grid { grid-template-columns: repeat(2, 1fr); gap: 14px; } }

  .wt-card {
    background: rgba(255,255,255,0.03);
    border: 1px solid rgba(255,255,255,0.06);
    padding: 14px; display: flex; flex-direction: column;
    gap: 10px; transition: all 0.25s ease; cursor: pointer;
    opacity: 0; animation: wtUp 0.5s ease forwards;
    position: relative;
  }
  .wt-card:hover {
    background: rgba(255,255,255,0.06);
    border-color: rgba(240,165,0,0.3);
    transform: translateY(-5px);
    box-shadow: 0 20px 48px rgba(0,0,0,0.35);
  }
  .wt-card.hidden { display: none; }

  /* Poster */
  .wt-poster-wrap {
    width: 100%; aspect-ratio: 2/3; position: relative;
    background: rgba(255,255,255,0.04); overflow: hidden;
  }
  .wt-poster {
    width: 100%; height: 100%; object-fit: cover;
    display: block; transition: opacity 0.3s ease;
  }
  .wt-poster-ph {
    width: 100%; height: 100%;
    background: linear-gradient(135deg, rgba(240,165,0,0.15), rgba(240,165,0,0.04));
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    gap: 8px; position: absolute; top: 0; left: 0;
  }
  .wt-poster-ph-letter {
    font-family: 'Playfair Display', serif;
    font-size: 36px; font-weight: 700; color: #f0a500; opacity: 0.6;
  }
  .wt-poster-loading {
    position: absolute; top: 0; left: 0; width: 100%; height: 100%;
    display: flex; align-items: center; justify-content: center;
    background: rgba(255,255,255,0.02);
  }
  .wt-spinner {
    width: 20px; height: 20px;
    border: 2px solid rgba(240,165,0,0.2);
    border-top-color: #f0a500; border-radius: 50%;
    animation: spin 0.8s linear infinite;
  }

  /* Type badge overlay */
  .wt-type-badge {
    position: absolute; top: 8px; left: 8px;
    font-family: 'DM Mono', monospace; font-size: 8px;
    letter-spacing: 0.1em; text-transform: uppercase;
    padding: 3px 6px; background: rgba(0,0,0,0.7);
    color: #f0a500; backdrop-filter: blur(4px);
  }

  /* Status badge */
  .wt-badge {
    display: inline-flex; align-items: center; gap: 4px;
    font-family: 'DM Mono', monospace; font-size: 9px;
    letter-spacing: 0.1em; text-transform: uppercase;
    padding: 3px 8px; width: fit-content;
  }
  .wt-badge-watched  { background: rgba(34,197,94,0.1);  color: #4ade80; border: 1px solid rgba(34,197,94,0.2); }
  .wt-badge-watching { background: rgba(240,165,0,0.1);  color: #f0a500; border: 1px solid rgba(240,165,0,0.2); }
  .wt-badge-want     { background: rgba(148,163,184,0.1); color: #94a3b8; border: 1px solid rgba(148,163,184,0.2); }

  .wt-card-title  { font-size: 13px; font-weight: 500; color: #f5f2eb; line-height: 1.3; }
  .wt-card-meta   { font-family: 'DM Mono', monospace; font-size: 10px; color: #4a4845; letter-spacing: 0.04em; }
  .wt-card-note   { font-size: 11px; line-height: 1.6; color: #5a5855; font-weight: 300; }

  /* ── Rating stars ── */
  .wt-rating { display: flex; gap: 2px; align-items: center; }
  .wt-star { font-size: 10px; color: #3a3835; }
  .wt-star.filled { color: #f0a500; }

  /* ── Empty state ── */
  .wt-empty {
    display: none; grid-column: 1 / -1; text-align: center;
    padding: 48px 0; font-family: 'DM Mono', monospace;
    font-size: 12px; letter-spacing: 0.1em;
    color: #3a3835; text-transform: uppercase;
  }

  /* ── API key notice ── */
  .wt-api-notice {
    background: rgba(240,165,0,0.06); border: 1px solid rgba(240,165,0,0.2);
    padding: 14px 18px; margin-bottom: 32px;
    display: flex; align-items: flex-start; gap: 10px;
  }
  .wt-api-notice p { font-size: 12px; line-height: 1.7; color: #a09e98; }
  .wt-api-notice strong { color: #f0a500; }
  .wt-api-notice code { font-family: 'DM Mono', monospace; font-size: 11px; background: rgba(255,255,255,0.06); padding: 1px 5px; }

  /* ── Light mode ── */
  html[data-mode="light"] .wt-header { border-bottom-color: rgba(0,0,0,0.08); }
  html[data-mode="light"] .wt-back { color: #9a9895 !important; }
  html[data-mode="light"] .wt-back:hover { color: #b86e00 !important; }
  html[data-mode="light"] .wt-title { color: #1a1916; }
  html[data-mode="light"] .wt-title em { color: #b86e00; }
  html[data-mode="light"] .wt-subtitle { color: #7a7875; }
  html[data-mode="light"] .wt-stat-n { color: #1a1916; }
  html[data-mode="light"] .wt-stat-n span { color: #b86e00; }
  html[data-mode="light"] .wt-stat-l { color: #c0bebb; }
  html[data-mode="light"] .wt-filter { border-color: rgba(0,0,0,0.1); color: #9a9895; }
  html[data-mode="light"] .wt-filter.active,
  html[data-mode="light"] .wt-filter:hover { border-color: rgba(184,110,0,0.35); color: #b86e00; background: rgba(184,110,0,0.06); }
  html[data-mode="light"] .wt-card { background: #f8f7f5; border-color: rgba(0,0,0,0.08); }
  html[data-mode="light"] .wt-card:hover { background: #f0ede8; border-color: rgba(184,110,0,0.35); box-shadow: 0 16px 40px rgba(0,0,0,0.1); }
  html[data-mode="light"] .wt-card-title { color: #1a1916; }
  html[data-mode="light"] .wt-card-meta { color: #9a9895; }
  html[data-mode="light"] .wt-card-note { color: #7a7875; }
  html[data-mode="light"] .wt-star { color: #d0ccc8; }
  html[data-mode="light"] .wt-star.filled { color: #b86e00; }
  html[data-mode="light"] .wt-badge-watched  { background: rgba(22,163,74,0.08);  color: #16a34a; border-color: rgba(22,163,74,0.2); }
  html[data-mode="light"] .wt-badge-watching { background: rgba(184,110,0,0.08);  color: #b86e00; border-color: rgba(184,110,0,0.2); }
  html[data-mode="light"] .wt-badge-want     { background: rgba(100,116,139,0.08); color: #64748b; border-color: rgba(100,116,139,0.2); }
  html[data-mode="light"] .wt-api-notice { background: rgba(184,110,0,0.05); border-color: rgba(184,110,0,0.2); }
  html[data-mode="light"] .wt-empty { color: #c0bebb; }
  html[data-mode="light"] .wt-poster-ph { background: linear-gradient(135deg, rgba(184,110,0,0.12), rgba(184,110,0,0.03)); }

  @keyframes wtUp { from { opacity: 0; transform: translateY(14px); } to { opacity: 1; transform: translateY(0); } }
  @keyframes spin  { to { transform: rotate(360deg); } }
</style>

<div class="wt-wrap">

  <!-- Header -->
  <div class="wt-header">
    <a href="/recommendations/" class="rc-back"><i class="fas fa-arrow-left"></i> Back to About</a>
    <h1 class="wt-title">Movies & <em>Shows.</em></h1>
    <p class="wt-subtitle">Everything I've watched, or  watching, or want to watch. Posters and ratings pulled automatically from TMDB.</p>
  </div>

  <!-- API key notice (hidden once key is set) -->
  <div class="wt-api-notice" id="wt-api-notice" style="display:none">
    <span style="font-size:16px;flex-shrink:0">🔑</span>
    <p><strong>TMDB API key missing.</strong> Posters won't load. Open <code>watching.md</code>, find <code>TMDB_API_KEY</code> at the top of the script and paste your key. Get a free key at <strong>themoviedb.org/settings/api</strong>.</p>
  </div>

  <!-- Stats -->
  <div class="wt-stats" id="wt-stats"></div>

  <!-- Filters -->
  <div class="wt-filters" id="wt-filters"></div>

  <!-- Grid -->
  <div class="wt-grid" id="wt-grid">
    <div class="wt-empty" id="wt-empty">Nothing in this category yet.</div>
  </div>

</div>

<script>
/* ═══════════════════════════════════════════════════════════════════════
   🔑 STEP 1: PASTE YOUR TMDB API KEY HERE
   Get a free key at: themoviedb.org/settings/api
   ═══════════════════════════════════════════════════════════════════════ */
 const TMDB_API_KEY = '{{ site.tmdb_api_key }}';

/* ═══════════════════════════════════════════════════════════════════════
   ✏️  STEP 2: EDIT THIS LIST TO ADD / UPDATE MOVIES & SHOWS

   HOW TO ADD AN ENTRY:
   1. Go to themoviedb.org and search for the movie or show.
   2. Click it — the URL will be like:
        themoviedb.org/movie/155-the-dark-knight   → tmdbId: 155,  type: 'movie'
        themoviedb.org/tv/1396-breaking-bad        → tmdbId: 1396, type: 'tv'
   3. Copy the number and add an object below.

   Fields:
     tmdbId  → number from TMDB URL (required for auto poster + year)
     type    → 'movie' or 'tv'
     status  → 'watched' | 'watching' | 'want-to-watch'
     rating  → your personal rating 1–5 (0 = not rated yet)
     note    → one-line personal take (optional, leave "" to hide)

   The poster, title, and year are fetched automatically from TMDB.
   ═══════════════════════════════════════════════════════════════════════ */
   const WATCHLIST = [
      /* ── Movies ── */
      { tmdbId: 489,    type: 'movie', status: 'watched', rating: 5, note: "Good Will Hunting — raw and human." },
      { tmdbId: 207,    type: 'movie', status: 'watched', rating: 5, note: "Dead Poets Society — carpe diem." },
      { tmdbId: 155,    type: 'movie', status: 'watched', rating: 5, note: "The Dark Knight — still unmatched." },
      { tmdbId: 11324,  type: 'movie', status: 'watched', rating: 5, note: "Shutter Island — paranoia done beautifully." },
      { tmdbId: 680,    type: 'movie', status: 'watched', rating: 5, note: "Pulp Fiction — nothing quite like it." },
      { tmdbId: 45317,  type: 'movie', status: 'watched', rating: 4, note: "Bumm Bumm Bole — simple and heartfelt." },
    
      /* ── TV ── */
      { tmdbId: 1434,   type: 'tv',    status: 'watched', rating: 5, note: "Succession — family, power, and the illusion of control." },
      { tmdbId: 1668,   type: 'tv',    status: 'watched', rating: 5, note: "Friends — comfort TV." },
      { tmdbId: 2316,   type: 'tv',    status: 'watched', rating: 5, note: "The Office — awkward brilliance." },
    ];

/* ═══════════════════════════════════════════════════════════════════════
   RENDERER — no need to edit below this line
═══════════════════════════════════════════════════════════════════════ */
(function () {
  var BASE_IMG = 'https://image.tmdb.org/t/p/w342';
  var activeFilter = 'all';

  /* Show API notice if key missing */
  if (!TMDB_API_KEY) {
    document.getElementById('wt-api-notice').style.display = 'flex';
  }

  /* ── Stats ── */
  var watched  = WATCHLIST.filter(function (w) { return w.status === 'watched'; }).length;
  var watching = WATCHLIST.filter(function (w) { return w.status === 'watching'; }).length;
  var want     = WATCHLIST.filter(function (w) { return w.status === 'want-to-watch'; }).length;
  var movies   = WATCHLIST.filter(function (w) { return w.type === 'movie'; }).length;
  var shows    = WATCHLIST.filter(function (w) { return w.type === 'tv'; }).length;

  var sh = '<div><p class="wt-stat-n">' + watched + '</p><p class="wt-stat-l">Watched</p></div>';
  if (watching > 0) sh += '<div><p class="wt-stat-n">' + watching + '</p><p class="wt-stat-l">Watching</p></div>';
  if (want > 0)     sh += '<div><p class="wt-stat-n">' + want + '</p><p class="wt-stat-l">Want to watch</p></div>';
  sh += '<div><p class="wt-stat-n">' + movies + '</p><p class="wt-stat-l">Movies</p></div>';
  if (shows > 0) sh += '<div><p class="wt-stat-n">' + shows + '</p><p class="wt-stat-l">TV Shows</p></div>';
  document.getElementById('wt-stats').innerHTML = sh;

  /* ── Filters ── */
  var filterDefs = [{ key: 'all', label: 'All' }];
  if (movies > 0)   filterDefs.push({ key: 'movie',         label: 'Movies' });
  if (shows > 0)    filterDefs.push({ key: 'tv',            label: 'TV Shows' });
  if (watched > 0)  filterDefs.push({ key: 'watched',       label: 'Watched' });
  if (watching > 0) filterDefs.push({ key: 'watching',      label: 'Watching' });
  if (want > 0)     filterDefs.push({ key: 'want-to-watch', label: 'Want to Watch' });

  var filtersEl = document.getElementById('wt-filters');
  filtersEl.innerHTML = filterDefs.map(function (f) {
    return '<button class="wt-filter' + (f.key === 'all' ? ' active' : '') + '" data-key="' + f.key + '">' + f.label + '</button>';
  }).join('');

  filtersEl.addEventListener('click', function (e) {
    var btn = e.target.closest('.wt-filter');
    if (!btn) return;
    activeFilter = btn.getAttribute('data-key');
    filtersEl.querySelectorAll('.wt-filter').forEach(function (b) { b.classList.remove('active'); });
    btn.classList.add('active');
    applyFilter();
  });

  /* ── Badge HTML ── */
  function badgeHtml(status) {
    if (status === 'watching')      return '<span class="wt-badge wt-badge-watching">● Watching</span>';
    if (status === 'want-to-watch') return '<span class="wt-badge wt-badge-want">○ Want to watch</span>';
    return '<span class="wt-badge wt-badge-watched">✓ Watched</span>';
  }

  /* ── Stars HTML ── */
  function starsHtml(rating) {
    if (!rating) return '';
    var html = '<div class="wt-rating">';
    for (var i = 1; i <= 5; i++) {
      html += '<span class="wt-star' + (i <= rating ? ' filled' : '') + '">★</span>';
    }
    return html + '</div>';
  }

  /* ── Build cards ── */
  var grid = document.getElementById('wt-grid');
  var emptyEl = document.getElementById('wt-empty');
  var cards = [];

  WATCHLIST.forEach(function (item, i) {
    var card = document.createElement('div');
    card.className = 'wt-card';
    card.setAttribute('data-type', item.type);
    card.setAttribute('data-status', item.status);
    card.style.animationDelay = (0.04 * i) + 's';

    /* Placeholder while loading */
    card.innerHTML =
      '<div class="wt-poster-wrap">' +
        '<div class="wt-poster-ph"><div class="wt-poster-loading"><div class="wt-spinner"></div></div></div>' +
        '<span class="wt-type-badge">' + (item.type === 'tv' ? 'TV' : 'Film') + '</span>' +
      '</div>' +
      badgeHtml(item.status) +
      '<p class="wt-card-title">Loading…</p>' +
      '<p class="wt-card-meta"></p>' +
      (item.note ? '<p class="wt-card-note">' + item.note + '</p>' : '') +
      starsHtml(item.rating);

    grid.insertBefore(card, emptyEl);
    cards.push({ card: card, item: item });

    /* Fetch from TMDB */
    if (TMDB_API_KEY) {
      var endpoint = item.type === 'tv'
        ? 'https://api.themoviedb.org/3/tv/' + item.tmdbId + '?api_key=' + TMDB_API_KEY
        : 'https://api.themoviedb.org/3/movie/' + item.tmdbId + '?api_key=' + TMDB_API_KEY;

      fetch(endpoint)
        .then(function (r) { return r.json(); })
        .then(function (data) {
          var title  = data.title || data.name || 'Unknown';
          var year   = (data.release_date || data.first_air_date || '').slice(0, 4);
          var poster = data.poster_path;
          var tmdbUrl = 'https://www.themoviedb.org/' + item.type + '/' + item.tmdbId;

          card.onclick = function () { window.open(tmdbUrl, '_blank'); };
          card.title = 'View on TMDB';

          var posterWrap = card.querySelector('.wt-poster-wrap');
          if (poster) {
            posterWrap.innerHTML =
              '<img class="wt-poster" src="' + BASE_IMG + poster + '" alt="' + title + '" ' +
                   'onerror="this.style.display=\'none\';this.nextSibling.style.display=\'flex\'">' +
              '<div class="wt-poster-ph" style="display:none"><span class="wt-poster-ph-letter">' + title[0] + '</span></div>' +
              '<span class="wt-type-badge">' + (item.type === 'tv' ? 'TV' : 'Film') + '</span>';
          } else {
            posterWrap.innerHTML =
              '<div class="wt-poster-ph"><span class="wt-poster-ph-letter">' + title[0] + '</span></div>' +
              '<span class="wt-type-badge">' + (item.type === 'tv' ? 'TV' : 'Film') + '</span>';
          }

          card.querySelector('.wt-card-title').textContent = title;
          card.querySelector('.wt-card-meta').textContent  = year || '';
        })
        .catch(function () {
          var posterWrap = card.querySelector('.wt-poster-wrap');
          posterWrap.querySelector('.wt-poster-loading').style.display = 'none';
          card.querySelector('.wt-card-title').textContent = 'TMDB #' + item.tmdbId;
        });
    } else {
      /* No API key — show placeholder with ID */
      var posterWrap = card.querySelector('.wt-poster-wrap');
      posterWrap.innerHTML =
        '<div class="wt-poster-ph"><span class="wt-poster-ph-letter">?</span></div>' +
        '<span class="wt-type-badge">' + (item.type === 'tv' ? 'TV' : 'Film') + '</span>';
      card.querySelector('.wt-card-title').textContent = 'ID ' + item.tmdbId + ' (add API key)';
    }
  });

  /* ── Filter function ── */
  function applyFilter() {
    var visible = 0;
    cards.forEach(function (c) {
      var type   = c.card.getAttribute('data-type');
      var status = c.card.getAttribute('data-status');
      var match  = activeFilter === 'all'
        || activeFilter === type
        || activeFilter === status;
      c.card.classList.toggle('hidden', !match);
      if (match) visible++;
    });
    emptyEl.style.display = visible === 0 ? 'block' : 'none';
  }

})();
</script>

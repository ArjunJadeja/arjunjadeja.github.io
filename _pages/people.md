---
layout: page
title: People
permalink: /people/
---

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,300;0,400;0,500;0,700&family=DM+Mono:wght@400;500&family=Playfair+Display:ital,wght@0,700;1,600&display=swap" rel="stylesheet">

<style>
  .pp-wrap * { box-sizing: border-box; margin: 0; padding: 0; }
  .pp-wrap {
    font-family: 'DM Sans', sans-serif;
    max-width: 900px;
    margin: 0 auto;
    padding: 0 0 80px;
  }

  /* ── Header ── */
  .pp-header {
    padding: 48px 0 52px;
    border-bottom: 1px solid rgba(255,255,255,0.07);
    margin-bottom: 48px;
    opacity: 0;
    animation: ppUp 0.7s ease forwards 0.1s;
  }
  .pp-back {
    display: inline-flex; align-items: center; gap: 6px;
    font-family: 'DM Mono', monospace; font-size: 10px;
    letter-spacing: 0.15em; text-transform: uppercase;
    color: #6b6965 !important; text-decoration: none !important;
    margin-bottom: 28px; transition: color 0.2s, gap 0.2s;
  }
  .pp-back:hover { color: #f0a500 !important; gap: 10px; }
  .pp-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(36px, 6vw, 60px);
    font-weight: 700; line-height: 1.05;
    letter-spacing: -0.02em; color: #f5f2eb; margin-bottom: 16px;
  }
  .pp-title em { font-style: italic; color: #f0a500; }
  .pp-subtitle {
    font-size: 15px; line-height: 1.7;
    color: #6b6965; font-weight: 300; max-width: 520px;
  }

  /* ── Stats ── */
  .pp-stats {
    display: flex; gap: 32px; flex-wrap: wrap;
    margin-bottom: 44px; opacity: 0;
    animation: ppUp 0.6s ease forwards 0.25s;
  }
  .pp-stat-n {
    font-family: 'Playfair Display', serif; font-size: 30px;
    font-weight: 700; color: #f5f2eb; line-height: 1; margin-bottom: 3px;
  }
  .pp-stat-n span { font-size: 15px; color: #f0a500; }
  .pp-stat-l {
    font-family: 'DM Mono', monospace; font-size: 9px;
    letter-spacing: 0.15em; text-transform: uppercase; color: #3a3835;
  }

  /* ── Filters ── */
  .pp-filters {
    display: flex; gap: 8px; flex-wrap: wrap;
    margin-bottom: 40px; opacity: 0;
    animation: ppUp 0.6s ease forwards 0.35s;
  }
  .pp-filter {
    font-family: 'DM Mono', monospace; font-size: 10px;
    letter-spacing: 0.1em; text-transform: uppercase;
    padding: 7px 14px; border: 1px solid rgba(255,255,255,0.08);
    background: transparent; color: #6b6965; cursor: pointer;
    transition: all 0.2s ease;
  }
  .pp-filter:hover, .pp-filter.active {
    border-color: rgba(240,165,0,0.35); color: #f0a500;
    background: rgba(240,165,0,0.06);
  }

  /* ── Grid ── */
  .pp-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
    gap: 20px;
  }
  @media (max-width: 560px) {
    .pp-grid { grid-template-columns: 1fr; }
  }

  /* ── Card ── */
  .pp-card {
    background: rgba(255,255,255,0.03);
    border: 1px solid rgba(255,255,255,0.06);
    padding: 24px;
    display: flex;
    flex-direction: column;
    gap: 16px;
    transition: all 0.25s ease;
    opacity: 0;
    animation: ppUp 0.5s ease forwards;
  }
  .pp-card:hover {
    background: rgba(255,255,255,0.06);
    border-color: rgba(240,165,0,0.3);
    transform: translateY(-4px);
    box-shadow: 0 20px 48px rgba(0,0,0,0.3);
  }
  .pp-card.hidden { display: none; }

  /* ── Card Top Row ── */
  .pp-card-top {
    display: flex;
    align-items: center;
    gap: 16px;
  }

  /* ── Avatar ── */
  .pp-avatar-wrap {
    position: relative;
    flex-shrink: 0;
  }
  .pp-avatar {
    width: 56px;
    height: 56px;
    border-radius: 50%;
    object-fit: cover;
    display: block;
    border: 2px solid rgba(240,165,0,0.25);
  }
  .pp-avatar-initials {
    width: 56px;
    height: 56px;
    border-radius: 50%;
    background: linear-gradient(135deg, #f0a500, #c47d00);
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'Playfair Display', serif;
    font-size: 20px;
    font-weight: 700;
    color: #111;
    flex-shrink: 0;
    border: 2px solid rgba(240,165,0,0.3);
    letter-spacing: 0;
  }

  /* ── Name & Tag ── */
  .pp-card-identity { flex: 1; min-width: 0; }
  .pp-name {
    font-size: 16px; font-weight: 500; color: #f5f2eb;
    margin-bottom: 5px; line-height: 1.2;
  }
  .pp-tag {
    font-family: 'DM Mono', monospace;
    font-size: 9px; letter-spacing: 0.12em; text-transform: uppercase;
    padding: 3px 8px; border: 1px solid rgba(240,165,0,0.25);
    color: #f0a500; width: fit-content;
  }

  /* ── One-liner ── */
  .pp-oneliner {
    font-size: 13px; line-height: 1.65; color: #7a7875; font-weight: 300;
    border-left: 2px solid rgba(240,165,0,0.2);
    padding-left: 12px;
  }

  /* ── Social links ── */
  .pp-socials {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-top: 2px;
  }
  .pp-social-link {
    display: inline-flex; align-items: center; gap: 5px;
    font-family: 'DM Mono', monospace; font-size: 9px;
    letter-spacing: 0.1em; text-transform: uppercase;
    color: #5a5855 !important; text-decoration: none !important;
    padding: 5px 10px;
    border: 1px solid rgba(255,255,255,0.07);
    transition: all 0.2s ease;
  }
  .pp-social-link:hover {
    color: #f0a500 !important;
    border-color: rgba(240,165,0,0.3);
    background: rgba(240,165,0,0.05);
  }
  .pp-social-link i { font-size: 10px; }

  /* ── Empty ── */
  .pp-empty {
    display: none; grid-column: 1/-1; text-align: center;
    padding: 48px 0; font-family: 'DM Mono', monospace;
    font-size: 12px; letter-spacing: 0.1em; color: #3a3835;
    text-transform: uppercase;
  }

  /* ── Note ── */
  .pp-note {
    background: rgba(240,165,0,0.05);
    border: 1px solid rgba(240,165,0,0.15);
    padding: 14px 18px;
    margin-top: 48px;
    display: flex; align-items: flex-start; gap: 10px;
  }
  .pp-note p { font-size: 12px; line-height: 1.7; color: #6b6965; }
  .pp-note p em { color: #a09e98; font-style: normal; }

  /* ── Light mode ── */
  html[data-mode="light"] .pp-header { border-bottom-color: rgba(0,0,0,0.08); }
  html[data-mode="light"] .pp-back { color: #9a9895 !important; }
  html[data-mode="light"] .pp-back:hover { color: #b86e00 !important; }
  html[data-mode="light"] .pp-title { color: #1a1916; }
  html[data-mode="light"] .pp-title em { color: #b86e00; }
  html[data-mode="light"] .pp-subtitle { color: #7a7875; }
  html[data-mode="light"] .pp-stat-n { color: #1a1916; }
  html[data-mode="light"] .pp-stat-n span { color: #b86e00; }
  html[data-mode="light"] .pp-stat-l { color: #c0bebb; }
  html[data-mode="light"] .pp-filter { border-color: rgba(0,0,0,0.1); color: #9a9895; }
  html[data-mode="light"] .pp-filter.active,
  html[data-mode="light"] .pp-filter:hover { border-color: rgba(184,110,0,0.35); color: #b86e00; background: rgba(184,110,0,0.06); }
  html[data-mode="light"] .pp-card { background: #f8f7f5; border-color: rgba(0,0,0,0.08); }
  html[data-mode="light"] .pp-card:hover { background: #f0ede8; border-color: rgba(184,110,0,0.35); box-shadow: 0 16px 40px rgba(0,0,0,0.1); }
  html[data-mode="light"] .pp-name { color: #1a1916; }
  html[data-mode="light"] .pp-tag { border-color: rgba(184,110,0,0.3); color: #b86e00; }
  html[data-mode="light"] .pp-oneliner { color: #6b6865; border-left-color: rgba(184,110,0,0.25); }
  html[data-mode="light"] .pp-social-link { color: #9a9895 !important; border-color: rgba(0,0,0,0.1); }
  html[data-mode="light"] .pp-social-link:hover { color: #b86e00 !important; border-color: rgba(184,110,0,0.3); background: rgba(184,110,0,0.05); }
  html[data-mode="light"] .pp-avatar-initials { background: linear-gradient(135deg, #b86e00, #8a5200); }
  html[data-mode="light"] .pp-empty { color: #c0bebb; }
  html[data-mode="light"] .pp-note { background: rgba(184,110,0,0.05); border-color: rgba(184,110,0,0.15); }
  html[data-mode="light"] .pp-note p { color: #7a7875; }
  html[data-mode="light"] .pp-note p em { color: #9a9895; }

  @keyframes ppUp { from { opacity: 0; transform: translateY(14px); } to { opacity: 1; transform: translateY(0); } }
</style>

<div class="pp-wrap">

  <!-- Header -->
  <div class="pp-header">
    <a href="/about/" class="pp-back"><i class="fas fa-arrow-left"></i> Back to About</a>
    <h1 class="pp-title">People I <em>Look Up To.</em></h1>
    <p class="pp-subtitle">People who've shaped how I think, work, run, and live. Not a network — a genuine list of people I admire.</p>
  </div>

  <!-- Stats -->
  <div class="pp-stats" id="pp-stats"></div>

  <!-- Filters -->
  <div class="pp-filters" id="pp-filters"></div>

  <!-- Grid -->
  <div class="pp-grid" id="pp-grid">
    <div class="pp-empty" id="pp-empty">No one in this category yet.</div>
  </div>

  <!-- Note -->
  <div class="pp-note">
    <span style="font-size:15px;flex-shrink:0">💛</span>
    <p>These are people I genuinely look up to — not sponsorships, not networking. <em>If you know them, tell them they made the list.</em></p>
  </div>

</div>

<script>
/* ═══════════════════════════════════════════════════════════════════════
   ✏️  EDIT THIS LIST TO ADD / UPDATE PEOPLE

   Fields:
     name      → full name
     initials  → 1–2 letters shown when no image (e.g. "KN")
     image     → URL to photo, or "" to use initials avatar
     category  → 'tech' | 'fitness' | 'life' | 'creator' | 'friend' | 'mentor'
     oneliner  → one sentence — why they matter to you
     socials   → array of { platform, url }
                 platform options: 'twitter' | 'linkedin' | 'github' | 'website' | 'instagram' | 'youtube'

   HOW TO ADD A NEW CATEGORY:
   Just use any new string in the `category` field — it auto-appears in filters.
   ═══════════════════════════════════════════════════════════════════════ */
var PEOPLE = [
  {
    name: "Dr. Kailash Nadh",
    initials: "KN",
    image: "",
    category: "tech",
    oneliner: "A rare kind of technologist — deeply principled, builds things that matter, thinks long-term. Shapes how I approach software.",
    socials: [
      { platform: "twitter",  url: "https://twitter.com/kailashnadh" },
      { platform: "website",  url: "https://nadh.in" }
    ]
  },
  {
    name: "Anil Mahobia",
    initials: "AM",
    image: "",
    category: "fitness",
    oneliner: "My running coach and mentor. The person who pushed me across my first half marathon finish line.",
    socials: []
  },
  {
    name: "Rahul Bhobhate",
    initials: "RB",
    image: "",
    category: "fitness",
    oneliner: "My gym brother. Having the right person beside you when you want to quit changes everything.",
    socials: []
  }

  /*
  ── Add more people below ───────────────────────────────────────────
  ,{
    name: "Paul Graham",
    initials: "PG",
    image: "",
    category: "tech",
    oneliner: "Essays that rewired how I think about startups, writing, and what it means to make something.",
    socials: [
      { platform: "twitter", url: "https://twitter.com/paulg" },
      { platform: "website", url: "https://paulgraham.com" }
    ]
  }
  ,{
    name: "David Goggins",
    initials: "DG",
    image: "",
    category: "fitness",
    oneliner: "Proof that the limits you believe in are mostly made up.",
    socials: [
      { platform: "instagram", url: "https://instagram.com/davidgoggins" }
    ]
  }
  ─────────────────────────────────────────────────────────────────── */
];

/* ═══════════════════════════════════════════════════════════════════════
   RENDERER — no need to edit below this line
═══════════════════════════════════════════════════════════════════════ */
(function () {

  var PLATFORM_ICONS = {
    twitter:   { icon: 'fab fa-twitter',   label: 'Twitter'   },
    linkedin:  { icon: 'fab fa-linkedin',  label: 'LinkedIn'  },
    github:    { icon: 'fab fa-github',    label: 'GitHub'    },
    website:   { icon: 'fas fa-globe',     label: 'Website'   },
    instagram: { icon: 'fab fa-instagram', label: 'Instagram' },
    youtube:   { icon: 'fab fa-youtube',   label: 'YouTube'   }
  };

  /* ── Stats ── */
  var cats = {};
  PEOPLE.forEach(function (p) {
    cats[p.category] = (cats[p.category] || 0) + 1;
  });

  var statsHtml = '<div><p class="pp-stat-n">' + PEOPLE.length + '</p><p class="pp-stat-l">People</p></div>';
  Object.keys(cats).forEach(function (c) {
    statsHtml += '<div><p class="pp-stat-n">' + cats[c] + '</p><p class="pp-stat-l">' + catLabel(c) + '</p></div>';
  });
  document.getElementById('pp-stats').innerHTML = statsHtml;

  /* ── Filters ── */
  var catKeys = ['all'].concat(Object.keys(cats));
  var filtersEl = document.getElementById('pp-filters');
  filtersEl.innerHTML = catKeys.map(function (c) {
    return '<button class="pp-filter' + (c === 'all' ? ' active' : '') + '" data-cat="' + c + '">'
      + (c === 'all' ? 'All' : catLabel(c)) + '</button>';
  }).join('');

  var activeFilter = 'all';
  filtersEl.addEventListener('click', function (e) {
    var btn = e.target.closest('.pp-filter');
    if (!btn) return;
    activeFilter = btn.getAttribute('data-cat');
    filtersEl.querySelectorAll('.pp-filter').forEach(function (b) { b.classList.remove('active'); });
    btn.classList.add('active');
    applyFilter();
  });

  /* ── Build cards ── */
  var grid = document.getElementById('pp-grid');
  var emptyEl = document.getElementById('pp-empty');

  PEOPLE.forEach(function (p, i) {
    var card = document.createElement('div');
    card.className = 'pp-card';
    card.setAttribute('data-cat', p.category);
    card.style.animationDelay = (0.06 * i) + 's';

    /* Avatar */
    var avatarHtml = p.image
      ? '<img class="pp-avatar" src="' + p.image + '" alt="' + p.name + '" onerror="this.style.display=\'none\';this.nextSibling.style.display=\'flex\'">'
        + '<div class="pp-avatar-initials" style="display:none">' + p.initials + '</div>'
      : '<div class="pp-avatar-initials">' + p.initials + '</div>';

    /* Socials */
    var socialsHtml = '';
    if (p.socials && p.socials.length) {
      socialsHtml = '<div class="pp-socials">'
        + p.socials.map(function (s) {
            var meta = PLATFORM_ICONS[s.platform] || { icon: 'fas fa-link', label: s.platform };
            return '<a href="' + s.url + '" class="pp-social-link" target="_blank" rel="noopener">'
              + '<i class="' + meta.icon + '"></i>' + meta.label + '</a>';
          }).join('')
        + '</div>';
    }

    card.innerHTML =
      '<div class="pp-card-top">'
      +  '<div class="pp-avatar-wrap">' + avatarHtml + '</div>'
      +  '<div class="pp-card-identity">'
      +    '<p class="pp-name">' + p.name + '</p>'
      +    '<span class="pp-tag">' + catLabel(p.category) + '</span>'
      +  '</div>'
      + '</div>'
      + '<p class="pp-oneliner">' + p.oneliner + '</p>'
      + socialsHtml;

    grid.insertBefore(card, emptyEl);
  });

  /* ── Filter ── */
  function applyFilter() {
    var cards = grid.querySelectorAll('.pp-card');
    var visible = 0;
    cards.forEach(function (c) {
      var match = activeFilter === 'all' || c.getAttribute('data-cat') === activeFilter;
      c.classList.toggle('hidden', !match);
      if (match) visible++;
    });
    emptyEl.style.display = visible === 0 ? 'block' : 'none';
  }

  /* ── Category label helper ── */
  function catLabel(c) {
    var map = {
      'tech': 'Tech', 'fitness': 'Fitness', 'life': 'Life',
      'creator': 'Creator', 'friend': 'Friend', 'mentor': 'Mentor'
    };
    return map[c] || (c.charAt(0).toUpperCase() + c.slice(1));
  }

  window.catLabel = catLabel; // expose for stats render above
})();

function catLabel(c) {
  var map = {
    'tech': 'Tech', 'fitness': 'Fitness', 'life': 'Life',
    'creator': 'Creator', 'friend': 'Friend', 'mentor': 'Mentor'
  };
  return map[c] || (c.charAt(0).toUpperCase() + c.slice(1));
}
</script>

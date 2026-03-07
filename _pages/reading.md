---
layout: page
title: Reading
permalink: /reading/
---

<style>
  .reading-wrap * { box-sizing: border-box; margin: 0; padding: 0; }

  .reading-wrap {
    font-family: 'DM Sans', sans-serif;
    max-width: 900px;
    margin: 0 auto;
    padding: 0 0 80px;
  }

  /* ── Header ── */
  .rd-header {
    padding: 48px 0 52px;
    border-bottom: 1px solid rgba(255,255,255,0.07);
    margin-bottom: 48px;
    opacity: 0;
    animation: rdUp 0.7s ease forwards 0.1s;
  }

  .rd-back {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: #6b6965 !important;
    text-decoration: none !important;
    margin-bottom: 28px;
    transition: color 0.2s, gap 0.2s;
  }

  .rd-back:hover { color: #f0a500 !important; gap: 10px; }

  .rd-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(36px, 6vw, 60px);
    font-weight: 700;
    line-height: 1.05;
    letter-spacing: -0.02em;
    color: #f5f2eb;
    margin-bottom: 16px;
  }

  .rd-title em { font-style: italic; color: #f0a500; }

  .rd-subtitle {
    font-size: 15px;
    line-height: 1.7;
    color: #6b6965;
    font-weight: 300;
    max-width: 520px;
  }

  /* ── Stats ── */
  .rd-stats {
    display: flex;
    gap: 32px;
    flex-wrap: wrap;
    margin-bottom: 44px;
    opacity: 0;
    animation: rdUp 0.6s ease forwards 0.25s;
  }

  .rd-stat-n {
    font-family: 'Playfair Display', serif;
    font-size: 30px;
    font-weight: 700;
    color: #f5f2eb;
    line-height: 1;
    margin-bottom: 3px;
  }

  .rd-stat-n span { font-size: 15px; color: #f0a500; }

  .rd-stat-l {
    font-family: 'DM Mono', monospace;
    font-size: 9px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: #3a3835;
  }

  /* ── Filter bar ── */
  .rd-filters {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
    margin-bottom: 40px;
    opacity: 0;
    animation: rdUp 0.6s ease forwards 0.35s;
  }

  .rd-filter {
    font-family: 'DM Mono', monospace;
    font-size: 10px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 7px 14px;
    border: 1px solid rgba(255,255,255,0.08);
    background: transparent;
    color: #6b6965;
    cursor: pointer;
    transition: all 0.2s ease;
  }

  .rd-filter:hover,
  .rd-filter.active {
    border-color: rgba(240,165,0,0.35);
    color: #f0a500;
    background: rgba(240,165,0,0.06);
  }

  /* ── Book grid ── */
  .rd-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
    gap: 24px;
  }

  @media (max-width: 480px) {
    .rd-grid { grid-template-columns: repeat(2, 1fr); gap: 16px; }
  }

  .rd-card {
    background: rgba(255,255,255,0.03);
    border: 1px solid rgba(255,255,255,0.06);
    padding: 16px;
    display: flex;
    flex-direction: column;
    gap: 10px;
    transition: all 0.25s ease;
    text-decoration: none !important;
    opacity: 0;
    animation: rdUp 0.5s ease forwards;
  }

  .rd-card:hover {
    background: rgba(255,255,255,0.06);
    border-color: rgba(240,165,0,0.3);
    transform: translateY(-5px);
    box-shadow: 0 20px 48px rgba(0,0,0,0.35);
  }

  .rd-card.hidden { display: none; }

  .rd-cover {
    width: 100%;
    aspect-ratio: 2/3;
    object-fit: cover;
    display: block;
    background: rgba(255,255,255,0.04);
  }

  .rd-cover-ph {
    width: 100%;
    aspect-ratio: 2/3;
    background: linear-gradient(135deg, rgba(240,165,0,0.12), rgba(240,165,0,0.04));
    display: none;
    align-items: center;
    justify-content: center;
    font-size: 36px;
  }

  /* Badges */
  .rd-badge {
    display: inline-flex;
    align-items: center;
    gap: 4px;
    font-family: 'DM Mono', monospace;
    font-size: 9px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 3px 8px;
    width: fit-content;
  }

  .rd-badge-read    { background: rgba(34,197,94,0.1);  color: #4ade80; border: 1px solid rgba(34,197,94,0.2); }
  .rd-badge-reading { background: rgba(240,165,0,0.1);  color: #f0a500; border: 1px solid rgba(240,165,0,0.2); }
  .rd-badge-want    { background: rgba(148,163,184,0.1); color: #94a3b8; border: 1px solid rgba(148,163,184,0.2); }

  .rd-book-title  { font-size: 13px; font-weight: 500; color: #f5f2eb; line-height: 1.3; }
  .rd-book-author { font-family: 'DM Mono', monospace; font-size: 10px; color: #4a4845; letter-spacing: 0.04em; }
  .rd-book-cat    { font-family: 'DM Mono', monospace; font-size: 9px; letter-spacing: 0.08em; text-transform: uppercase; color: #3a3835; }
  .rd-book-summary { font-size: 11px; line-height: 1.6; color: #5a5855; font-weight: 300; }

  /* ── Empty state ── */
  .rd-empty {
    display: none;
    grid-column: 1 / -1;
    text-align: center;
    padding: 48px 0;
    font-family: 'DM Mono', monospace;
    font-size: 12px;
    letter-spacing: 0.1em;
    color: #3a3835;
    text-transform: uppercase;
  }

  /* ── Light mode overrides ── */
  @media (prefers-color-scheme: light) {
    .rd-header { border-bottom-color: rgba(0,0,0,0.08); }
    .rd-title { color: #1a1916; }
    .rd-subtitle { color: #7a7875; }
    .rd-stat-n { color: #1a1916; }
    .rd-stat-l { color: #c0bebb; }
    .rd-filter { border-color: rgba(0,0,0,0.1); color: #9a9895; }
    .rd-card { background: #f8f7f5; border-color: rgba(0,0,0,0.08); }
    .rd-card:hover { background: #f0ede8; box-shadow: 0 16px 40px rgba(0,0,0,0.1); }
    .rd-book-title  { color: #1a1916; }
    .rd-book-author { color: #9a9895; }
    .rd-book-cat    { color: #c0bebb; }
    .rd-book-summary { color: #7a7875; }
    .rd-back { color: #9a9895 !important; }
    .rd-empty { color: #c0bebb; }
    .rd-badge-read    { background: rgba(22,163,74,0.08);  color: #16a34a; border-color: rgba(22,163,74,0.2); }
    .rd-badge-reading { background: rgba(184,110,0,0.08);  color: #b86e00; border-color: rgba(184,110,0,0.2); }
    .rd-badge-want    { background: rgba(100,116,139,0.08); color: #64748b; border-color: rgba(100,116,139,0.2); }
  }

  /* Chirpy light mode class */
  html[data-mode="light"] .rd-header { border-bottom-color: rgba(0,0,0,0.08); }
  html[data-mode="light"] .rd-title  { color: #1a1916; }
  html[data-mode="light"] .rd-subtitle { color: #7a7875; }
  html[data-mode="light"] .rd-stat-n { color: #1a1916; }
  html[data-mode="light"] .rd-stat-l { color: #c0bebb; }
  html[data-mode="light"] .rd-filter { border-color: rgba(0,0,0,0.1); color: #9a9895; }
  html[data-mode="light"] .rd-filter.active,
  html[data-mode="light"] .rd-filter:hover { border-color: rgba(184,110,0,0.35); color: #b86e00; background: rgba(184,110,0,0.06); }
  html[data-mode="light"] .rd-card { background: #f8f7f5; border-color: rgba(0,0,0,0.08); }
  html[data-mode="light"] .rd-card:hover { background: #f0ede8; border-color: rgba(184,110,0,0.35); box-shadow: 0 16px 40px rgba(0,0,0,0.1); }
  html[data-mode="light"] .rd-book-title  { color: #1a1916; }
  html[data-mode="light"] .rd-book-author { color: #9a9895; }
  html[data-mode="light"] .rd-book-cat    { color: #c0bebb; }
  html[data-mode="light"] .rd-book-summary { color: #7a7875; }
  html[data-mode="light"] .rd-back { color: #9a9895 !important; }
  html[data-mode="light"] .rd-empty { color: #c0bebb; }
  html[data-mode="light"] .rd-badge-read    { background: rgba(22,163,74,0.08);  color: #16a34a; border-color: rgba(22,163,74,0.2); }
  html[data-mode="light"] .rd-badge-reading { background: rgba(184,110,0,0.08);  color: #b86e00; border-color: rgba(184,110,0,0.2); }
  html[data-mode="light"] .rd-badge-want    { background: rgba(100,116,139,0.08); color: #64748b; border-color: rgba(100,116,139,0.2); }

  @keyframes rdUp {
    from { opacity: 0; transform: translateY(14px); }
    to   { opacity: 1; transform: translateY(0); }
  }
</style>

<div class="reading-wrap">

  <!-- Header -->
  <div class="rd-header">
    <a href="/recommendations/" class="rc-back"><i class="fas fa-arrow-left"></i> Back to About</a>
    <h1 class="rd-title">Books I'm <em>Reading.</em></h1>
    <p class="rd-subtitle">A personal shortlist of books I’ve read, am currently reading, or plan to read and found worth recommending.</p>
  </div>

  <!-- Stats -->
  <div class="rd-stats" id="rd-stats"></div>

  <!-- Filters -->
  <div class="rd-filters" id="rd-filters"></div>

  <!-- Grid -->
  <div class="rd-grid" id="rd-grid">
    <div class="rd-empty" id="rd-empty">No books in this category yet.</div>
  </div>

</div>

<script>
(function () {
  /*
  ═══════════════════════════════════════════════════════════════════
  BOOK DATA
  This is the single source of truth. The about page also references
  window.ARJUN_BOOKS if it loads first — but this page is self-contained.

  To add a book:
    1. Copy one of the existing objects
    2. Fill in title, author, isbn, category, status, summary
    3. Save — done.

  isbn: find at openlibrary.org → used for cover thumbnail
  category: 'self-help' | 'fiction' | 'non-fiction' | 'philosophy' |
            'science' | 'biography' | 'tech' | 'classic'
  status:   'read' | 'reading' | 'want-to-read'
  ═══════════════════════════════════════════════════════════════════
  */
  var BOOKS = [
    {
      title: "Dopamine Nation",
      author: "Anna Lembke",
      isbn: "9781524746728",
      category: "non-fiction",
      status: "read",
      summary: "Why pleasure and pain are more intertwined than we think — and what that means for modern life."
    },
    {
      title: "Animal Farm",
      author: "George Orwell",
      isbn: "9780451526342",
      category: "fiction",
      status: "read",
      summary: "A deceptively simple fable about power, corruption, and how revolutions eat their own."
    },
    {
      title: "The Politics",
      author: "Aristotle",
      isbn: "9780140444216",
      category: "philosophy",
      status: "reading",
      summary: "The foundational text on governance — surprisingly relevant two millennia later."
    },
    {
      title: "Think and Grow Rich",
      author: "Napoleon Hill",
      isbn: "9781585424337",
      category: "self-help",
      status: "read",
      summary: "A classic on wealth-building mindset, persistence, and the psychology of achievement."
    }
    ,{
      title: "Zero to One",
      author: "Peter Thiel",
      isbn: "9780804139298",
      category: "non-fiction",
      status: "read",
      summary: "Building companies that create new things instead of competing in crowded markets."
    }
    ,{
      title: "Dark Matter",
      author: "Blake Crouch",
      isbn: "9781101904220",
      category: "fiction",
      status: "reading",
      summary: "A fast-paced sci-fi thriller exploring parallel universes, identity, and the roads not taken."
    }

    /*
    ── Add more books below ────────────────────────────────────────── 
    ,{
      title: "The Power of Habit",
      author: "Charles Duhigg",
      isbn: "9780812981605",
      category: "self-help",
      status: "read",
      summary: "How habits form, how they work, and how understanding them can reshape our lives."
    }
    ,{
      title: "Atomic Habits",
      author: "James Clear",
      isbn: "9780735211292",
      category: "self-help",
      status: "want-to-read",
      summary: "Tiny changes, remarkable results — the compounding effect of small daily improvements."
    }
    ,{
      title: "How to Win Friends and Influence People",
      author: "Dale Carnegie",
      isbn: "9780671027032",
      category: "self-help",
      status: "want-to-read",
      summary: "Timeless principles on communication, persuasion, and building meaningful relationships."
    }
    ,{
      title: "The Pragmatic Programmer",
      author: "David Thomas & Andrew Hunt",
      isbn: "9780135957059",
      category: "tech",
      status: "reading",
      summary: "Timeless advice on thinking about software the right way."
    }
    ,{
      title: "Sapiens",
      author: "Yuval Noah Harari",
      isbn: "9780062316097",
      category: "non-fiction",
      status: "want-to-read",
      summary: "A sweeping history of humankind and why we ended up here."
    }
    ,{
      title: "Meditations",
      author: "Marcus Aurelius",
      isbn: "9780140449334",
      category: "philosophy",
      status: "want-to-read",
      summary: "Personal journal of a Roman emperor — still the best stoic primer."
    }
    ,{
      title: "Clean Code",
      author: "Robert C. Martin",
      isbn: "9780132350884",
      category: "tech",
      status: "read",
      summary: "How to write code that other humans can actually understand."
    }
    ,{
      title: "The Alchemist",
      author: "Paulo Coelho",
      isbn: "9780062315007",
      category: "fiction",
      status: "read",
      summary: "Follow your personal legend — even when the universe seems to be testing you."
    }
    ,{
      title: "Thinking, Fast and Slow",
      author: "Daniel Kahneman",
      isbn: "9780374533557",
      category: "science",
      status: "want-to-read",
      summary: "Two systems that drive the way we think — and how to use that knowledge."
    }
    ──────────────────────────────────────────────────────────────── */
  ];

  /* ── Helpers ── */
  function googleUrl(title, author) {
    return 'https://www.google.com/search?q=' + encodeURIComponent(title + ' ' + author + ' book');
  }

  function badgeHtml(status) {
    if (status === 'reading')      return '<span class="rd-badge rd-badge-reading">● Reading</span>';
    if (status === 'want-to-read') return '<span class="rd-badge rd-badge-want">○ Want to read</span>';
    return '<span class="rd-badge rd-badge-read">✓ Read</span>';
  }

  function catLabel(c) {
    var map = {
      'self-help': 'Self Help', 'fiction': 'Fiction', 'non-fiction': 'Non-Fiction',
      'philosophy': 'Philosophy', 'science': 'Science', 'biography': 'Biography',
      'tech': 'Tech', 'classic': 'Classic'
    };
    return map[c] || c;
  }

  /* ── Compute stats ── */
  var read = BOOKS.filter(function (b) { return b.status === 'read'; }).length;
  var reading = BOOKS.filter(function (b) { return b.status === 'reading'; }).length;
  var want = BOOKS.filter(function (b) { return b.status === 'want-to-read'; }).length;

  var statsEl = document.getElementById('rd-stats');
  statsEl.innerHTML =
    '<div><p class="rd-stat-n">' + read + '</p><p class="rd-stat-l">Read</p></div>' +
    (reading > 0 ? '<div><p class="rd-stat-n">' + reading + '</p><p class="rd-stat-l">Reading</p></div>' : '') +
    (want > 0    ? '<div><p class="rd-stat-n">' + want + '</p><p class="rd-stat-l">Want to read</p></div>' : '') +
    '<div><p class="rd-stat-n">' + BOOKS.length + '</p><p class="rd-stat-l">Total</p></div>';

  /* ── Build filters ── */
  var cats = ['all'];
  BOOKS.forEach(function (b) {
    if (cats.indexOf(b.category) === -1) cats.push(b.category);
  });

  var filtersEl = document.getElementById('rd-filters');
  filtersEl.innerHTML = cats.map(function (c) {
    return '<button class="rd-filter' + (c === 'all' ? ' active' : '') + '" data-cat="' + c + '">' +
      (c === 'all' ? 'All' : catLabel(c)) +
      '</button>';
  }).join('');

  var activeFilter = 'all';

  filtersEl.addEventListener('click', function (e) {
    var btn = e.target.closest('.rd-filter');
    if (!btn) return;
    activeFilter = btn.getAttribute('data-cat');
    filtersEl.querySelectorAll('.rd-filter').forEach(function (b) { b.classList.remove('active'); });
    btn.classList.add('active');
    filterCards();
  });

  /* ── Render all cards ── */
  var grid = document.getElementById('rd-grid');
  var emptyEl = document.getElementById('rd-empty');

  BOOKS.forEach(function (b, i) {
    var card = document.createElement('a');
    card.className = 'rd-card';
    card.href = googleUrl(b.title, b.author);
    card.target = '_blank';
    card.rel = 'noopener';
    card.setAttribute('data-cat', b.category);
    card.style.animationDelay = (0.05 * i) + 's';
    card.innerHTML =
      '<img class="rd-cover" src="https://covers.openlibrary.org/b/isbn/' + b.isbn + '-M.jpg" ' +
           'alt="' + b.title + '" onerror="this.style.display=\'none\';this.nextElementSibling.style.display=\'flex\'">' +
      '<div class="rd-cover-ph" style="display:none">📖</div>' +
      badgeHtml(b.status) +
      '<p class="rd-book-title">' + b.title + '</p>' +
      '<p class="rd-book-author">' + b.author + '</p>' +
      '<p class="rd-book-cat">' + catLabel(b.category) + '</p>' +
      '<p class="rd-book-summary">' + b.summary + '</p>';
    grid.insertBefore(card, emptyEl);
  });

  /* ── Filter function ── */
  function filterCards() {
    var cards = grid.querySelectorAll('.rd-card');
    var visible = 0;
    cards.forEach(function (card) {
      var match = activeFilter === 'all' || card.getAttribute('data-cat') === activeFilter;
      card.classList.toggle('hidden', !match);
      if (match) visible++;
    });
    emptyEl.style.display = visible === 0 ? 'block' : 'none';
  }

})();
</script>

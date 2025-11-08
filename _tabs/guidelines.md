---
layout: page
title: Guidelines
icon: fas fa-compass
order: 3
---

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,300;0,400;0,500;0,700&family=DM+Mono:wght@400;500&family=Playfair+Display:ital,wght@0,700;1,600&display=swap" rel="stylesheet">

<style>
  .gl * { box-sizing: border-box; margin: 0; padding: 0; }
  .gl { font-family: 'DM Sans', sans-serif; max-width: 860px; margin: 0 auto; padding: 0 0 80px; }

  .gl-header { padding: 44px 0 48px; border-bottom: 1px solid rgba(255,255,255,0.07); margin-bottom: 56px; }
  .gl-eyebrow { font-family: 'DM Mono', monospace; font-size: 11px; letter-spacing: 0.2em; text-transform: uppercase; color: #f0a500; margin-bottom: 16px; opacity: 0; animation: glUp 0.6s ease forwards 0.1s; }
  .gl-title { font-family: 'Playfair Display', serif; font-size: clamp(36px, 6vw, 60px); font-weight: 700; line-height: 1.08; letter-spacing: -0.02em; color: #f5f2eb; margin-bottom: 20px; opacity: 0; animation: glUp 0.7s ease forwards 0.2s; }
  .gl-title em { font-style: italic; color: #f0a500; }
  .gl-intro { font-size: 15px; line-height: 1.85; color: #c8c6c0; max-width: 600px; font-weight: 300; opacity: 0; animation: glUp 0.7s ease forwards 0.35s; }
  .gl-intro strong { color: #f5f2eb; font-weight: 500; }

  .gl-stats { display: flex; gap: 32px; flex-wrap: wrap; padding: 28px 0; border-bottom: 1px solid rgba(255,255,255,0.07); margin-bottom: 52px; opacity: 0; animation: glUp 0.7s ease forwards 0.5s; }
  .gl-stat-n { font-family: 'Playfair Display', serif; font-size: 28px; font-weight: 700; color: #f5f2eb; line-height: 1; margin-bottom: 3px; }
  .gl-stat-n span { font-size: 14px; color: #f0a500; }
  .gl-stat-l { font-family: 'DM Mono', monospace; font-size: 9px; letter-spacing: 0.15em; text-transform: uppercase; color: #6b6965; }

  .gl-cat-header { display: flex; align-items: center; gap: 14px; margin-bottom: 28px; margin-top: 52px; opacity: 0; transform: translateY(10px); transition: opacity 0.6s ease, transform 0.6s ease; }
  .gl-cat-header.visible { opacity: 1; transform: translateY(0); }
  .gl-cat-icon { font-size: 20px; }
  .gl-cat-name { font-family: 'Playfair Display', serif; font-size: 18px; font-weight: 700; color: #f5f2eb; }
  .gl-cat-line { flex: 1; height: 1px; background: rgba(255,255,255,0.06); }
  .gl-cat-count { font-family: 'DM Mono', monospace; font-size: 9px; letter-spacing: 0.15em; text-transform: uppercase; color: #4a4845; }

  .gl-timeline { position: relative; padding-left: 28px; }
  .gl-timeline::before { content: ''; position: absolute; left: 7px; top: 8px; bottom: 8px; width: 1px; background: rgba(255,255,255,0.06); }

  .gl-entry { position: relative; margin-bottom: 32px; opacity: 0; transform: translateY(12px); transition: opacity 0.6s ease, transform 0.6s ease; }
  .gl-entry.visible { opacity: 1; transform: translateY(0); }
  .gl-entry::before { content: ''; position: absolute; left: -24px; top: 18px; width: 8px; height: 8px; border-radius: 50%; border: 2px solid #f0a500; background: #0f0f0e; transition: background 0.2s; }
  .gl-entry:hover::before { background: #f0a500; }

  .gl-card { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.07); padding: 22px 24px; transition: all 0.25s ease; }
  .gl-card:hover { background: rgba(255,255,255,0.055); border-color: rgba(240,165,0,0.3); transform: translateX(4px); box-shadow: 0 14px 36px rgba(0,0,0,0.3); }

  .gl-card-top { display: flex; align-items: flex-start; justify-content: space-between; gap: 12px; margin-bottom: 12px; flex-wrap: wrap; }
  .gl-card-left { display: flex; align-items: center; gap: 12px; }
  .gl-card-icon { font-size: 18px; flex-shrink: 0; width: 34px; height: 34px; display: flex; align-items: center; justify-content: center; background: rgba(240,165,0,0.08); border: 1px solid rgba(240,165,0,0.18); }
  .gl-card-title { font-family: 'Playfair Display', serif; font-size: 17px; font-weight: 700; color: #f5f2eb; line-height: 1.2; }
  .gl-card-meta { display: flex; align-items: center; gap: 8px; flex-shrink: 0; flex-wrap: wrap; justify-content: flex-end; }
  .gl-since { font-family: 'DM Mono', monospace; font-size: 9px; letter-spacing: 0.12em; text-transform: uppercase; color: #4a4845; white-space: nowrap; }
  .gl-cat-tag { font-family: 'DM Mono', monospace; font-size: 9px; letter-spacing: 0.1em; text-transform: uppercase; padding: 3px 8px; background: rgba(255,255,255,0.04); border: 1px solid rgba(255,255,255,0.08); color: #7a7875; white-space: nowrap; }

  .gl-card-body { font-size: 13.5px; line-height: 1.75; color: #b0ada6; margin-bottom: 14px; }
  .gl-card-points { list-style: none; display: flex; flex-direction: column; gap: 8px; margin-bottom: 14px; }
  .gl-card-points li { font-size: 13px; line-height: 1.65; color: #a09e98; padding-left: 18px; position: relative; }
  .gl-card-points li::before { content: '→'; position: absolute; left: 0; color: #f0a500; font-size: 11px; top: 1px; }

  .gl-read-more { display: inline-flex; align-items: center; gap: 5px; font-family: 'DM Mono', monospace; font-size: 9px; letter-spacing: 0.12em; text-transform: uppercase; color: #f0a500 !important; text-decoration: none !important; border-bottom: 1px solid rgba(240,165,0,0.25); padding-bottom: 1px; transition: all 0.2s; }
  .gl-read-more:hover { border-color: #f0a500; gap: 8px; }

  .gl-flexible-note { background: rgba(240,165,0,0.05); border: 1px solid rgba(240,165,0,0.18); padding: 16px 20px; margin-top: 52px; display: flex; align-items: flex-start; gap: 12px; }
  .gl-flexible-note p { font-size: 13px; line-height: 1.7; color: #a09e98; }
  .gl-flexible-note p strong { color: #f0a500; font-weight: 500; }
  .gl-flexible-note a { color: #f0a500 !important; text-decoration: none !important; }

  /* ── Light mode ── */
  html[data-mode="light"] .gl-header { border-bottom-color: rgba(0,0,0,0.08); }
  html[data-mode="light"] .gl-eyebrow { color: #b86e00; }
  html[data-mode="light"] .gl-title { color: #1a1916; }
  html[data-mode="light"] .gl-title em { color: #b86e00; }
  html[data-mode="light"] .gl-intro { color: #4a4845; }
  html[data-mode="light"] .gl-intro strong { color: #1a1916; }
  html[data-mode="light"] .gl-stats { border-bottom-color: rgba(0,0,0,0.08); }
  html[data-mode="light"] .gl-stat-n { color: #1a1916; }
  html[data-mode="light"] .gl-stat-n span { color: #b86e00; }
  html[data-mode="light"] .gl-stat-l { color: #9a9895; }
  html[data-mode="light"] .gl-cat-name { color: #1a1916; }
  html[data-mode="light"] .gl-cat-line { background: rgba(0,0,0,0.08); }
  html[data-mode="light"] .gl-cat-count { color: #b0ada6; }
  html[data-mode="light"] .gl-timeline::before { background: rgba(0,0,0,0.08); }
  html[data-mode="light"] .gl-entry::before { border-color: #b86e00; background: #ffffff; }
  html[data-mode="light"] .gl-entry:hover::before { background: #b86e00; }
  html[data-mode="light"] .gl-card { background: #f8f7f5; border-color: rgba(0,0,0,0.08); }
  html[data-mode="light"] .gl-card:hover { background: #f0ede8; border-color: rgba(184,110,0,0.35); box-shadow: 0 10px 28px rgba(0,0,0,0.08); }
  html[data-mode="light"] .gl-card-icon { background: rgba(184,110,0,0.07); border-color: rgba(184,110,0,0.2); }
  html[data-mode="light"] .gl-card-title { color: #1a1916; }
  html[data-mode="light"] .gl-since { color: #b0ada6; }
  html[data-mode="light"] .gl-cat-tag { background: rgba(0,0,0,0.03); border-color: rgba(0,0,0,0.09); color: #7a7875; }
  html[data-mode="light"] .gl-card-body { color: #4a4845; }
  html[data-mode="light"] .gl-card-points li { color: #5a5855; }
  html[data-mode="light"] .gl-card-points li::before { color: #b86e00; }
  html[data-mode="light"] .gl-read-more { color: #b86e00 !important; border-bottom-color: rgba(184,110,0,0.25); }
  html[data-mode="light"] .gl-read-more:hover { border-color: #b86e00; }
  html[data-mode="light"] .gl-flexible-note { background: rgba(184,110,0,0.05); border-color: rgba(184,110,0,0.2); }
  html[data-mode="light"] .gl-flexible-note p { color: #5a5855; }
  html[data-mode="light"] .gl-flexible-note p strong { color: #b86e00; }
  html[data-mode="light"] .gl-flexible-note a { color: #b86e00 !important; }

  @keyframes glUp {
    from { opacity: 0; transform: translateY(12px); }
    to   { opacity: 1; transform: translateY(0); }
  }
</style>

<div class="gl">
  <div class="gl-header">
    <p class="gl-eyebrow">// how I operate</p>
    <h1 class="gl-title">My <em>Guidelines.</em></h1>
    <p class="gl-intro">
      These aren't rules I follow perfectly — they're principles I keep coming back to.
      Some I've held for years, others are newer experiments.
      <strong>Flexible by design, honest by default.</strong> This page is a living document.
    </p>
  </div>
  <div class="gl-stats" id="gl-stats"></div>
  <div id="gl-body"></div>
  <div class="gl-flexible-note">
    <span style="font-size:16px;flex-shrink:0">💡</span>
    <p><strong>These are flexible, not rigid.</strong> I've broken every single one at some point — and will again. The point isn't perfection, it's having a compass to come back to. If something resonates or you do it differently, <a href="https://twitter.com/thearjunjadeja">I'd love to hear it.</a></p>
  </div>
</div>

<script>
/* ═══════════════════════════════════════════════════════════════════════
   ✏️  EDIT ONLY THIS SECTION TO ADD / UPDATE GUIDELINES
   ═══════════════════════════════════════════════════════════════════════

   HOW TO ADD A NEW GUIDELINE:
   1. Find the right category in CATEGORIES below (or add a new one).
   2. Add a new object to its `items` array — copy any existing one as template.
   3. Fields:
        icon      → any emoji
        title     → card heading
        since     → e.g. "Since Jan 2025"
        tag       → short label e.g. "Mind"
        body      → one sentence describing the why
        points    → array of bullet strings
        postSlug  → URL slug of a linked post (leave "" if none)
                    How to find the slug: look at the post URL in your browser
                    e.g. /posts/daily-routine-for-calmness/
                    slug = "daily-routine-for-calmness"

   HOW TO ADD A NEW CATEGORY:
   Add to CATEGORIES: { icon: "🎯", name: "New Category", items: [...] }

   The guideline count in the stats bar is calculated automatically.
   ═══════════════════════════════════════════════════════════════════════ */

var STATS = [
  { label: "Categories",       value: "5",    suffix: ""  },
  { label: "Started tracking", value: "2024", suffix: ""  },
  { label: "Work in progress", value: "∞",    suffix: ""  }
];

var CATEGORIES = [
  {
    icon: "🧠",
    name: "Mind & Calm",
    items: [
      {
        icon: "🌊",
        title: "Daily Calmness Routine",
        since: "Since Sep 2025",
        tag: "Mind",
        body: "To reduce overthinking and avoid anxiety spirals. The brain needs training just like the body does — and these are my reps.",
        points: [
          "5–7 min morning calm: sunlight, 5 deep breaths, 1 gratitude + 1 intention",
          "Scheduled worry time at 5:30 PM daily — 15 minutes only, thoughts go on paper",
          "7–10 min night routine: journal dump, 4-7-8 breathing, positive closure",
          "If panic hits mid-day: 3 deep breaths or 5-4-3-2-1 grounding"
        ],
        postSlug: "daily-routine-for-calmness"
      },
      {
        icon: "😴",
        title: "Sleep Guidelines",
        since: "Since Aug 2025",
        tag: "Mind",
        body: "Good sleep is the foundation everything else is built on. I stopped treating it as optional.",
        points: [
          "Phone off or on DND 30 minutes before bed — non-negotiable",
          "Read physical book before sleeping, even if just 10 pages",
          "Shift sleep 10–15 min earlier every few days — small steps compound",
          "Same wake-up time regardless of when you slept — anchors the rhythm",
          "Sleeping early is the keystone — everything else depends on it"
        ],
        postSlug: ""
      }
    ]
  },
  {
    icon: "💪",
    name: "Body",
    items: [
      {
        icon: "🏋️",
        title: "Hypertrophy Training Approach",
        since: "Since Jun 2025",
        tag: "Body",
        body: "Started underweight, now intermediate. The approach that worked: keep it simple, stay consistent, trust the process.",
        points: [
          "Follow provided chart for hypertrophy - intermediate level",
          "Progressive overload — add weight or reps every session, even if tiny",
          "Protein target: ~1.6–2g per kg bodyweight daily",
          "Rest days are part of the program, not failure",
          "Target by Jun 2026: 72–75 kg lean and muscular, decreasing fat while building muscle"
        ],
        postSlug: ""
      }
    ]
  },
  {
    icon: "📚",
    name: "Learning",
    items: [
      {
        icon: "🔍",
        title: "How to Approach Any New Topic",
        since: "Since 2023",
        tag: "Learning",
        body: "Most learning fails at the starting point — going straight to how without understanding why.",
        points: [
          "Start with the why — why does this exist, what problem does it solve?",
          "Get the big picture before any detail — read the intro, not the manual",
          "Build something small immediately — theory without practice evaporates",
          "Teach it back in your own words — if you can't, you don't understand it yet",
          "Keep a learning log: what confused me, what clicked, what's still open"
        ],
        postSlug: ""
      }
    ]
  },
  {
    icon: "✍️",
    name: "Writing & Blogging",
    items: [
      {
        icon: "📝",
        title: "How I Structure a Blog Post",
        since: "Since 2024",
        tag: "Writing",
        body: "Writing is thinking out loud. My posts are personal references I've open-sourced. The goal is clarity, not cleverness.",
        points: [
          "Write the messy draft first — editing before writing is the biggest blocker",
          "Never publish the same day you finish — sleep on it",
          "Start with the problem, not the solution — context earns attention",
          "Simplify until a curious 16-year-old could follow it",
          "Story first, code second — people remember narrative, not syntax"
        ],
        postSlug: ""
      }
    ]
  },
  {
    icon: "⚡",
    name: "Code & Work",
    items: [
      {
        icon: "🤖",
        title: "Android Development Principles",
        since: "Since 2022",
        tag: "Code",
        body: "These aren't rules from a book — they're things I got wrong first and learned the hard way.",
        points: [
          "Read the existing code before touching it — assumptions are expensive",
          "If it's hard to test, it's hard to maintain — that's the smell",
          "Name things clearly even if the name is long — code is read 10x more than written",
          "Solve the problem, not the imagined future problem",
          "When stuck: rubber duck first, Stack Overflow second, ask third"
        ],
        postSlug: ""
      }
    ]
  }
];

/* ═══════════════════════════════════════════════════════════════════════
   RENDERER — no need to edit below this line
═══════════════════════════════════════════════════════════════════════ */
(function () {
  var total = CATEGORIES.reduce(function (s, c) { return s + c.items.length; }, 0);

  /* Stats */
  var sh = '<div><p class="gl-stat-n">' + total + '<span>+</span></p><p class="gl-stat-l">Guidelines</p></div>';
  STATS.forEach(function (s) {
    sh += '<div><p class="gl-stat-n">' + s.value + (s.suffix ? '<span>' + s.suffix + '</span>' : '') + '</p><p class="gl-stat-l">' + s.label + '</p></div>';
  });
  document.getElementById('gl-stats').innerHTML = sh;

  /* Categories + entries */
  var html = '';
  CATEGORIES.forEach(function (cat) {
    html += '<div class="gl-cat-header">'
      + '<span class="gl-cat-icon">' + cat.icon + '</span>'
      + '<h2 class="gl-cat-name">' + cat.name + '</h2>'
      + '<div class="gl-cat-line"></div>'
      + '<span class="gl-cat-count">' + cat.items.length + ' guideline' + (cat.items.length !== 1 ? 's' : '') + '</span>'
      + '</div><div class="gl-timeline">';

    cat.items.forEach(function (item) {
      var link = item.postSlug
        ? '<a href="/posts/' + item.postSlug + '/" class="gl-read-more">Full post <i class="fas fa-arrow-right"></i></a>'
        : '';
      var pts = item.points.map(function (p) { return '<li>' + p + '</li>'; }).join('');
      html += '<div class="gl-entry"><div class="gl-card">'
        + '<div class="gl-card-top">'
        +   '<div class="gl-card-left">'
        +     '<div class="gl-card-icon">' + item.icon + '</div>'
        +     '<p class="gl-card-title">' + item.title + '</p>'
        +   '</div>'
        +   '<div class="gl-card-meta">'
        +     '<span class="gl-since">' + item.since + '</span>'
        +     '<span class="gl-cat-tag">' + item.tag + '</span>'
        +   '</div>'
        + '</div>'
        + '<p class="gl-card-body">' + item.body + '</p>'
        + '<ul class="gl-card-points">' + pts + '</ul>'
        + link
        + '</div></div>';
    });

    html += '</div>'; /* close gl-timeline */
  });

  document.getElementById('gl-body').innerHTML = html;

  /* Scroll reveal */
  var obs = new IntersectionObserver(function (entries) {
    entries.forEach(function (e) {
      if (e.isIntersecting) { e.target.classList.add('visible'); obs.unobserve(e.target); }
    });
  }, { threshold: 0.06 });
  document.querySelectorAll('.gl-entry, .gl-cat-header').forEach(function (el) { obs.observe(el); });
})();
</script>

---
layout: page
title: About
icon: fas fa-info-circle
order: 5
---

<style>
  .about-wrap * { box-sizing: border-box; margin: 0; padding: 0; }

  .about-wrap {
    font-family: 'DM Sans', sans-serif;
    color: var(--text-color, #e8e6e0);
    max-width: 860px;
    margin: 0 auto;
    padding: 0 0 80px;
  }

  @import url('https://fonts.googleapis.com/css2?family=DM+Sans:ital,wght@0,300;0,400;0,500;0,700;1,300&family=DM+Mono:wght@400;500&family=Playfair+Display:ital,wght@0,700;1,600&display=swap');

  /* ── Hero ── */
  .hero { position: relative; padding: 64px 0 56px; border-bottom: 1px solid rgba(255,255,255,0.07); margin-bottom: 72px; }
  .hero-eyebrow { font-family: 'DM Mono', monospace; font-size: 11px; letter-spacing: 0.2em; text-transform: uppercase; color: #f0a500; margin-bottom: 20px; opacity: 0; animation: fadeUp 0.6s ease forwards 0.1s; }
  .hero-name { font-family: 'Playfair Display', serif; font-size: clamp(48px, 7vw, 80px); font-weight: 700; line-height: 1.05; letter-spacing: -0.02em; color: #f5f2eb; margin-bottom: 20px; opacity: 0; animation: fadeUp 0.7s ease forwards 0.2s; }
  .hero-name span { font-style: italic; font-weight: 600; color: #f0a500; }
  .hero-bio { font-size: 17px; line-height: 1.75; color: #a09e98; max-width: 560px; font-weight: 300; margin-bottom: 32px; opacity: 0; animation: fadeUp 0.7s ease forwards 0.35s; }
  .hero-actions { display: flex; gap: 14px; flex-wrap: wrap; opacity: 0; animation: fadeUp 0.7s ease forwards 0.5s; }
  .btn-primary { display: inline-flex; align-items: center; gap: 8px; background: #f0a500; color: #111; font-family: 'DM Mono', monospace; font-size: 12px; letter-spacing: 0.1em; text-transform: uppercase; padding: 13px 24px; text-decoration: none !important; font-weight: 500; transition: all 0.2s ease; border: none; }
  .btn-primary:hover { background: #ffb820; transform: translateY(-2px); box-shadow: 0 8px 24px rgba(240,165,0,0.25); color: #111; text-decoration: none !important; }
  .btn-secondary { display: inline-flex; align-items: center; gap: 8px; background: transparent; color: #a09e98; font-family: 'DM Mono', monospace; font-size: 12px; letter-spacing: 0.1em; text-transform: uppercase; padding: 13px 24px; text-decoration: none !important; border: 1px solid rgba(255,255,255,0.12); transition: all 0.2s ease; }
  .btn-secondary:hover { border-color: rgba(255,255,255,0.3); color: #f5f2eb; text-decoration: none !important; }

  /* ── Quote ── */
  .quote-block { margin: 0 0 72px; padding: 36px 0 36px 32px; border-left: 3px solid #f0a500; opacity: 0; animation: fadeUp 0.7s ease forwards 0.6s; }
  .quote-text { font-family: 'Playfair Display', serif; font-style: italic; font-size: clamp(20px, 2.8vw, 26px); line-height: 1.5; color: #d4d0c8; margin-bottom: 12px; }
  .quote-attr { font-family: 'DM Mono', monospace; font-size: 11px; letter-spacing: 0.15em; color: #f0a500; text-transform: uppercase; }

  /* ── Section ── */
  .section { margin-bottom: 80px; opacity: 0; animation: fadeUp 0.7s ease forwards; }
  .section-header { display: flex; align-items: baseline; gap: 16px; margin-bottom: 36px; }
  .section-label { font-family: 'DM Mono', monospace; font-size: 10px; letter-spacing: 0.25em; text-transform: uppercase; color: #f0a500; white-space: nowrap; }
  .section-title { font-family: 'Playfair Display', serif; font-size: clamp(24px, 3vw, 32px); font-weight: 700; color: #f5f2eb; letter-spacing: -0.01em; }
  .section-line { flex: 1; height: 1px; background: rgba(255,255,255,0.07); margin-left: 8px; }

  /* ── Book Grid ── */
  .book-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 24px; margin-bottom: 20px; }
  .book-card { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.06); padding: 20px; display: flex; flex-direction: column; gap: 12px; transition: all 0.25s ease; cursor: pointer; text-decoration: none !important; }
  .book-card:hover { background: rgba(255,255,255,0.06); border-color: rgba(240,165,0,0.3); transform: translateY(-4px); box-shadow: 0 16px 40px rgba(0,0,0,0.3); }
  .book-card:focus { outline: 2px solid #f0a500; outline-offset: 2px; }
  .book-cover { width: 100%; aspect-ratio: 2/3; object-fit: cover; background: rgba(255,255,255,0.05); display: block; }
  .book-cover-placeholder { width: 100%; aspect-ratio: 2/3; background: linear-gradient(135deg, rgba(240,165,0,0.15), rgba(240,165,0,0.05)); display: flex; align-items: center; justify-content: center; font-size: 32px; }
  .book-title { font-size: 14px; font-weight: 500; color: #f5f2eb; line-height: 1.3; }
  .book-author { font-family: 'DM Mono', monospace; font-size: 11px; color: #6b6965; letter-spacing: 0.05em; }
  .badge { display: inline-flex; align-items: center; gap: 5px; font-family: 'DM Mono', monospace; font-size: 10px; letter-spacing: 0.1em; text-transform: uppercase; padding: 4px 9px; width: fit-content; }
  .badge-done { background: rgba(34,197,94,0.1); color: #4ade80; border: 1px solid rgba(34,197,94,0.2); }
  .view-all-link { display: inline-flex; align-items: center; gap: 8px; font-family: 'DM Mono', monospace; font-size: 11px; letter-spacing: 0.15em; text-transform: uppercase; color: #f0a500 !important; text-decoration: none !important; border-bottom: 1px solid rgba(240,165,0,0.25); padding-bottom: 2px; transition: all 0.2s ease; }
  .view-all-link:hover { border-color: #f0a500; gap: 12px; }

  /* ── Movie Grid ── */
  .movie-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(160px, 1fr)); gap: 20px; margin-bottom: 20px; }
  .movie-card { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.06); padding: 14px; display: flex; flex-direction: column; gap: 10px; transition: all 0.25s ease; cursor: pointer; position: relative; }
  .movie-card:hover { background: rgba(255,255,255,0.06); border-color: rgba(240,165,0,0.3); transform: translateY(-4px); box-shadow: 0 16px 40px rgba(0,0,0,0.3); }
  .movie-poster-wrap { width: 100%; aspect-ratio: 2/3; position: relative; background: rgba(255,255,255,0.04); overflow: hidden; }
  .movie-poster { width: 100%; height: 100%; object-fit: cover; display: block; }
  .movie-poster-ph { width: 100%; height: 100%; background: linear-gradient(135deg, rgba(240,165,0,0.15), rgba(240,165,0,0.04)); display: flex; align-items: center; justify-content: center; position: absolute; top: 0; left: 0; }
  .movie-poster-ph-letter { font-family: 'Playfair Display', serif; font-size: 36px; font-weight: 700; color: #f0a500; opacity: 0.6; }
  .movie-type-badge { position: absolute; top: 8px; left: 8px; font-family: 'DM Mono', monospace; font-size: 8px; letter-spacing: 0.1em; text-transform: uppercase; padding: 3px 6px; background: rgba(0,0,0,0.7); color: #f0a500; }
  .movie-spinner { width: 20px; height: 20px; border: 2px solid rgba(240,165,0,0.2); border-top-color: #f0a500; border-radius: 50%; animation: spin 0.8s linear infinite; position: absolute; top: 50%; left: 50%; margin: -10px 0 0 -10px; }
  .movie-title { font-size: 13px; font-weight: 500; color: #f5f2eb; line-height: 1.3; }
  .movie-year { font-family: 'DM Mono', monospace; font-size: 10px; color: #4a4845; }
  .movie-note { font-size: 11px; line-height: 1.6; color: #5a5855; font-weight: 300; }
  .movie-stars { display: flex; gap: 2px; }
  .movie-star { font-size: 10px; color: #3a3835; }
  .movie-star.on { color: #f0a500; }

  /* ── People ── */
  .people-grid { display: grid; gap: 16px; }
  .person-card { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.06); padding: 24px 28px; display: grid; grid-template-columns: auto 1fr auto; align-items: center; gap: 20px; transition: all 0.25s ease; }
  .person-card:hover { background: rgba(255,255,255,0.05); border-color: rgba(240,165,0,0.25); }
  .person-avatar { width: 48px; height: 48px; border-radius: 50%; background: linear-gradient(135deg, #f0a500, #c47d00); display: flex; align-items: center; justify-content: center; font-family: 'Playfair Display', serif; font-size: 18px; font-weight: 700; color: #111; flex-shrink: 0; }
  .person-name { font-size: 16px; font-weight: 500; color: #f5f2eb; margin-bottom: 4px; }
  .person-why { font-size: 13px; color: #6b6965; line-height: 1.5; }
  .person-tag { font-family: 'DM Mono', monospace; font-size: 10px; letter-spacing: 0.1em; text-transform: uppercase; padding: 5px 10px; border: 1px solid rgba(240,165,0,0.25); color: #f0a500; white-space: nowrap; }

  /* ── Running ── */
  .race-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(180px, 1fr)); gap: 16px; margin-bottom: 32px; }
  .race-card { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.06); padding: 24px 20px; text-align: center; transition: all 0.25s ease; position: relative; overflow: hidden; }
  .race-card.completed { border-color: rgba(240,165,0,0.3); background: rgba(240,165,0,0.04); }
  .race-card:hover { transform: translateY(-3px); box-shadow: 0 12px 32px rgba(0,0,0,0.25); }
  .race-distance { font-family: 'Playfair Display', serif; font-size: 28px; font-weight: 700; color: #f5f2eb; margin-bottom: 4px; }
  .race-label { font-family: 'DM Mono', monospace; font-size: 10px; letter-spacing: 0.15em; text-transform: uppercase; color: #4a4845; margin-bottom: 16px; }
  .race-time { font-family: 'DM Mono', monospace; font-size: 15px; color: #f0a500; font-weight: 500; }
  .race-pending { font-family: 'DM Mono', monospace; font-size: 12px; color: #3a3835; letter-spacing: 0.1em; }
  .race-meta { font-size: 11px; color: #5a5855; margin-top: 6px; line-height: 1.4; }
  .goal-banner { background: rgba(240,165,0,0.06); border: 1px solid rgba(240,165,0,0.2); padding: 20px 24px; display: flex; align-items: center; gap: 16px; }
  .goal-icon { font-size: 22px; }
  .goal-text { font-size: 14px; color: #a09e98; line-height: 1.5; }
  .goal-text strong { color: #f0a500; font-weight: 500; }

  /* ── Workout ── */
  .workout-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; margin-bottom: 24px; }
  .stat-card { background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.06); padding: 24px; }
  .stat-value { font-family: 'Playfair Display', serif; font-size: 36px; font-weight: 700; color: #f5f2eb; line-height: 1; margin-bottom: 6px; }
  .stat-value span { font-size: 18px; color: #f0a500; }
  .stat-label { font-family: 'DM Mono', monospace; font-size: 10px; letter-spacing: 0.15em; text-transform: uppercase; color: #4a4845; margin-bottom: 12px; }
  .stat-desc { font-size: 13px; color: #6b6965; line-height: 1.55; }
  .progress-wrap { margin-top: 14px; }
  .progress-label { display: flex; justify-content: space-between; font-family: 'DM Mono', monospace; font-size: 10px; letter-spacing: 0.1em; color: #5a5855; margin-bottom: 6px; text-transform: uppercase; }
  .progress-bar { height: 4px; background: rgba(255,255,255,0.06); border-radius: 2px; overflow: hidden; }
  .progress-fill { height: 100%; background: linear-gradient(90deg, #f0a500, #ffb820); border-radius: 2px; transition: width 1.2s ease; }

  /* ── Recovery ── */
  .recovery-notice { background: rgba(239,68,68,0.05); border: 1px solid rgba(239,68,68,0.15); padding: 16px 20px; display: flex; align-items: flex-start; gap: 12px; margin-top: 24px; }
  .recovery-icon { font-size: 16px; flex-shrink: 0; margin-top: 1px; }
  .recovery-text { font-size: 13px; color: #7a7875; line-height: 1.6; }
  .recovery-text strong { color: #f87171; font-weight: 500; }

  /* ── Connect ── */
  .connect-block { border-top: 1px solid rgba(255,255,255,0.07); padding-top: 48px; text-align: center; }
  .connect-title { font-family: 'Playfair Display', serif; font-size: clamp(22px, 3vw, 30px); color: #f5f2eb; margin-bottom: 12px; }
  .connect-sub { font-size: 15px; color: #6b6965; margin-bottom: 32px; font-weight: 300; }
  .connect-tags { display: flex; flex-wrap: wrap; justify-content: center; gap: 10px; }
  .connect-tag { font-family: 'DM Mono', monospace; font-size: 11px; letter-spacing: 0.1em; text-transform: uppercase; padding: 8px 16px; border: 1px solid rgba(255,255,255,0.08); color: #6b6965; transition: all 0.2s ease; }
  .connect-tag:hover { border-color: rgba(240,165,0,0.3); color: #f0a500; background: rgba(240,165,0,0.04); }

  /* ── Light Mode ── */
  html[data-mode="light"] .hero { border-bottom-color: rgba(0,0,0,0.08); }
  html[data-mode="light"] .hero-eyebrow { color: #b86e00; }
  html[data-mode="light"] .hero-name { color: #1a1916; }
  html[data-mode="light"] .hero-name span { color: #b86e00; }
  html[data-mode="light"] .hero-bio { color: #6b6865; }
  html[data-mode="light"] .btn-primary { background: #b86e00; color: #fff; }
  html[data-mode="light"] .btn-primary:hover { background: #c97c00; color: #fff; }
  html[data-mode="light"] .btn-secondary { color: #7a7875 !important; border-color: rgba(0,0,0,0.12); }
  html[data-mode="light"] .btn-secondary:hover { color: #1a1916 !important; border-color: rgba(0,0,0,0.3); }
  html[data-mode="light"] .quote-block { border-left-color: #b86e00; }
  html[data-mode="light"] .quote-text { color: #3a3836; }
  html[data-mode="light"] .quote-attr { color: #b86e00; }
  html[data-mode="light"] .section-label { color: #b86e00; }
  html[data-mode="light"] .section-title { color: #1a1916; }
  html[data-mode="light"] .section-line { background: rgba(0,0,0,0.08); }
  html[data-mode="light"] .book-card { background: #f8f7f5; border-color: rgba(0,0,0,0.08); }
  html[data-mode="light"] .book-card:hover { background: #f0ede8; border-color: rgba(184,110,0,0.35); box-shadow: 0 16px 40px rgba(0,0,0,0.1); }
  html[data-mode="light"] .book-title { color: #1a1916; }
  html[data-mode="light"] .book-author { color: #9a9895; }
  html[data-mode="light"] .badge-done { background: rgba(22,163,74,0.08); color: #16a34a; border-color: rgba(22,163,74,0.2); }
  html[data-mode="light"] .view-all-link { color: #b86e00 !important; }
  html[data-mode="light"] .movie-card { background: #f8f7f5; border-color: rgba(0,0,0,0.08); }
  html[data-mode="light"] .movie-card:hover { background: #f0ede8; border-color: rgba(184,110,0,0.35); box-shadow: 0 16px 40px rgba(0,0,0,0.1); }
  html[data-mode="light"] .movie-title { color: #1a1916; }
  html[data-mode="light"] .movie-year { color: #9a9895; }
  html[data-mode="light"] .movie-note { color: #7a7875; }
  html[data-mode="light"] .movie-star { color: #d0ccc8; }
  html[data-mode="light"] .movie-star.on { color: #b86e00; }
  html[data-mode="light"] .person-card { background: #f8f7f5; border-color: rgba(0,0,0,0.08); }
  html[data-mode="light"] .person-card:hover { background: #f0ede8; border-color: rgba(184,110,0,0.25); }
  html[data-mode="light"] .person-name { color: #1a1916; }
  html[data-mode="light"] .person-why { color: #7a7875; }
  html[data-mode="light"] .person-tag { border-color: rgba(184,110,0,0.3); color: #b86e00; }
  html[data-mode="light"] .person-avatar { background: linear-gradient(135deg, #b86e00, #8a5200); }
  html[data-mode="light"] .race-card { background: #f8f7f5; border-color: rgba(0,0,0,0.08); }
  html[data-mode="light"] .race-card.completed { background: rgba(184,110,0,0.05); border-color: rgba(184,110,0,0.3); }
  html[data-mode="light"] .race-distance { color: #1a1916; }
  html[data-mode="light"] .race-label { color: #c0bebb; }
  html[data-mode="light"] .race-time { color: #b86e00; }
  html[data-mode="light"] .race-pending { color: #d0cecc; }
  html[data-mode="light"] .race-meta { color: #9a9895; }
  html[data-mode="light"] .goal-banner { background: rgba(184,110,0,0.05); border-color: rgba(184,110,0,0.2); }
  html[data-mode="light"] .goal-text { color: #6b6865; }
  html[data-mode="light"] .goal-text strong { color: #b86e00; }
  html[data-mode="light"] .recovery-notice { background: rgba(200,30,30,0.04); border-color: rgba(200,30,30,0.14); }
  html[data-mode="light"] .recovery-text { color: #7a7875; }
  html[data-mode="light"] .recovery-text strong { color: #c01e1e; }
  html[data-mode="light"] .stat-card { background: #f8f7f5; border-color: rgba(0,0,0,0.08); }
  html[data-mode="light"] .stat-value { color: #1a1916; }
  html[data-mode="light"] .stat-value span { color: #b86e00; }
  html[data-mode="light"] .stat-label { color: #c0bebb; }
  html[data-mode="light"] .stat-desc { color: #7a7875; }
  html[data-mode="light"] .progress-label { color: #c0bebb; }
  html[data-mode="light"] .progress-bar { background: rgba(0,0,0,0.07); }
  html[data-mode="light"] .progress-fill { background: linear-gradient(90deg, #b86e00, #d48800); }
  html[data-mode="light"] .connect-block { border-top-color: rgba(0,0,0,0.08); }
  html[data-mode="light"] .connect-title { color: #1a1916; }
  html[data-mode="light"] .connect-sub { color: #7a7875; }
  html[data-mode="light"] .connect-tag { border-color: rgba(0,0,0,0.09); color: #9a9895; }
  html[data-mode="light"] .connect-tag:hover { border-color: rgba(184,110,0,0.3); color: #b86e00; background: rgba(184,110,0,0.05); }

  @media (max-width: 560px) {
    .workout-grid { grid-template-columns: 1fr; }
    .person-card { grid-template-columns: auto 1fr; }
    .person-tag { display: none; }
  }

  @keyframes fadeUp { from { opacity: 0; transform: translateY(18px); } to { opacity: 1; transform: translateY(0); } }
  @keyframes spin   { to { transform: rotate(360deg); } }

  .s1 { animation-delay: 0.7s; }
  .s2 { animation-delay: 0.85s; }
  .s3 { animation-delay: 1.0s; }
  .s4 { animation-delay: 1.1s; }
  .s5 { animation-delay: 1.2s; }
  .s6 { animation-delay: 1.3s; }
</style>

<div class="about-wrap">

  <!-- ── Hero ── -->
  <div class="hero">
    <p class="hero-eyebrow">// android engineer · kotlin · curious by default</p>
    <h1 class="hero-name">Arjun<br><span>Jadeja.</span></h1>
    <p class="hero-bio">
      Senior Android Engineer at ClearQuote. I build things for Android, obsess over clean code, and believe the best software solves real problems in the simplest possible way. This is my corner of the internet — no fluff, just things I care about.
    </p>
    <div class="hero-actions">
      <a href="https://drive.google.com/file/d/1PzgnYPKlnMB2W2ETLMIqv3OMoXwxeNTt/view?usp=share_link" class="btn-primary" target="_blank">
        <i class="fas fa-file-alt"></i> Resume
      </a>
      <a href="https://github.com/ArjunJadeja" class="btn-secondary" target="_blank">
        <i class="fab fa-github"></i> GitHub
      </a>
      <a href="https://twitter.com/thearjunjadeja" class="btn-secondary" target="_blank">
        <i class="fab fa-twitter"></i> Twitter
      </a>
    </div>
  </div>

  <!-- ── Quote ── -->
  <div class="quote-block">
    <p class="quote-text">"You miss 100% of the shots you don't take."</p>
    <p class="quote-attr">— Wayne Gretzky</p>
  </div>

  <!-- ── Recommendations teaser ── -->
  <div class="section s1">
    <div class="section-header">
      <span class="section-label">01</span>
      <h2 class="section-title">Recommendations</h2>
      <div class="section-line"></div>
    </div>
    <p style="color:#a09e98; font-size:14px; line-height:1.7; margin-bottom:20px;">
      Books, movies, people, places and things that genuinely made a difference.
    </p>
    <a href="/recommendations/" class="view-all-link">
      Browse recommendations <i class="fas fa-arrow-right"></i>
    </a>
  </div>

  <!-- ── Running ── -->
  <div class="section s4">
    <div class="section-header">
      <span class="section-label">04</span>
      <h2 class="section-title">Running</h2>
      <div class="section-line"></div>
    </div>

    <div class="race-grid">
      <div class="race-card">
        <p class="race-distance">5<span style="font-size:16px;color:#f0a500">k</span></p>
        <p class="race-label">Races</p>
        <p class="race-pending">— —</p>
      </div>
      <div class="race-card">
        <p class="race-distance">10<span style="font-size:16px;color:#f0a500">k</span></p>
        <p class="race-label">Races</p>
        <p class="race-pending">— —</p>
      </div>
      <div class="race-card completed">
        <p class="race-distance">21<span style="font-size:16px;color:#f0a500">k</span></p>
        <p class="race-label">Half Marathon</p>
        <p class="race-time">2:36:19</p>
        <p class="race-meta">1 Feb 2025<br>Huffman, Bengaluru</p>
      </div>
    </div>

    <div class="goal-banner">
      <span class="goal-icon">🎯</span>
      <p class="goal-text"><strong>2025 Goal:</strong> Complete all four races of the <strong>Pro-CAM Slam</strong> — Bengaluru, Mumbai, Delhi, Kolkata.</p>
    </div>

    <div class="recovery-notice">
      <span class="recovery-icon">⚠️</span>
      <p class="recovery-text"><strong>Currently recovering</strong> from a tibial stress fracture (left shin). On a mandatory rest. Coming back stronger.</p>
    </div>
  </div>

  <!-- ── Workout ── -->
  <div class="section s5">
    <div class="section-header">
      <span class="section-label">05</span>
      <h2 class="section-title">Workout</h2>
      <div class="section-line"></div>
    </div>

    <div class="workout-grid">
      <div class="stat-card">
        <p class="stat-value">70<span>kg</span></p>
        <p class="stat-label">Current Weight</p>
        <p class="stat-desc">Gained 12 kg since June 2024. Started underweight, now in healthy range.</p>
      </div>
      <div class="stat-card">
        <p class="stat-value">22<span>%</span></p>
        <p class="stat-label">Body Fat</p>
        <p class="stat-desc">Goal is to reduce this while building lean muscle. Body recomposition phase.</p>
        <div class="progress-wrap">
          <div class="progress-label"><span>Target</span><span>~15%</span></div>
          <div class="progress-bar"><div class="progress-fill" style="width: 68%"></div></div>
        </div>
      </div>
      <div class="stat-card">
        <p class="stat-value" style="font-size:24px; padding-top:4px">Intermediate</p>
        <p class="stat-label">Training Level</p>
        <p class="stat-desc">Hypertrophy-focused training. Started as a beginner, earned this through consistency.</p>
        <div class="progress-wrap">
          <div class="progress-label"><span>Beginner</span><span>Advanced</span></div>
          <div class="progress-bar"><div class="progress-fill" style="width: 55%"></div></div>
        </div>
      </div>
      <div class="stat-card" style="display:flex;flex-direction:column;justify-content:center;align-items:center;text-align:center;">
        <span style="font-size: 36px; margin-bottom: 12px;">🏋️</span>
        <p class="stat-label" style="margin-bottom:8px">Focus</p>
        <p class="stat-desc">Hypertrophy training. 4–5 days/week push-pull-legs split.</p>
      </div>
    </div>

    <div class="recovery-notice">
      <span class="recovery-icon">⚠️</span>
      <p class="recovery-text"><strong>Training paused</strong> due to tibial stress fracture. Same injury, same comeback story.</p>
    </div>
  </div>

  <!-- ── Connect ── -->
  <div class="connect-block s6">
    <h2 class="connect-title">Let's connect</h2>
    <p class="connect-sub">Always open to good conversations — about Android, code, running, books, or just life.</p>
    <div class="connect-tags">
      <span class="connect-tag">Fellow developer</span>
      <span class="connect-tag">Running buddy</span>
      <span class="connect-tag">Book nerd</span>
      <span class="connect-tag">Open source</span>
      <span class="connect-tag">Just say hi</span>
    </div>
  </div>

</div>

<script>
/* ═══════════════════════════════════════════════════════════════════════
   🔑 PASTE YOUR TMDB API KEY HERE (same key as in watching.md)
   ═══════════════════════════════════════════════════════════════════════ */
var TMDB_API_KEY = '{{ site.tmdb_api_key }}';

/*
  The about page shows a preview of your WATCHLIST.
  It picks the first 3 items with status 'watched' that have a note.
  To control what shows here, just reorder items in watching.md's WATCHLIST —
  the about page always shows the first 3 watchable entries.
*/
var ABOUT_WATCHLIST = [
  { tmdbId: 155,   type: 'movie', rating: 5, note: "A masterclass in storytelling — chaos vs order, and why some people just want to watch the world burn." },
  { tmdbId: 274,   type: 'movie', rating: 5, note: "Carpe diem. Reminded me why passion over convention is always worth it." },
  { tmdbId: 72976, type: 'movie', rating: 4, note: "A love letter to nostalgia, creativity, and making peace with the present." }
];

(function () {
  var BASE_IMG = 'https://image.tmdb.org/t/p/w342';
  var grid = document.getElementById('about-movie-grid');
  if (!grid) return;

  ABOUT_WATCHLIST.forEach(function (item) {
    var card = document.createElement('div');
    card.className = 'movie-card';

    card.innerHTML =
      '<div class="movie-poster-wrap">' +
        '<div class="movie-poster-ph"><div class="movie-spinner"></div></div>' +
        '<span class="movie-type-badge">' + (item.type === 'tv' ? 'TV' : 'Film') + '</span>' +
      '</div>' +
      '<p class="movie-title">Loading…</p>' +
      '<p class="movie-year"></p>' +
      (item.note ? '<p class="movie-note">' + item.note + '</p>' : '') +
      (item.rating ? '<div class="movie-stars">' + [1,2,3,4,5].map(function(i){ return '<span class="movie-star' + (i <= item.rating ? ' on' : '') + '">★</span>'; }).join('') + '</div>' : '');

    grid.appendChild(card);

    if (TMDB_API_KEY) {
      var url = 'https://api.themoviedb.org/3/' + item.type + '/' + item.tmdbId + '?api_key=' + TMDB_API_KEY;
      fetch(url).then(function (r) { return r.json(); }).then(function (data) {
        var title  = data.title || data.name || '';
        var year   = (data.release_date || data.first_air_date || '').slice(0, 4);
        var poster = data.poster_path;
        var tmdbUrl = 'https://www.themoviedb.org/' + item.type + '/' + item.tmdbId;
        card.onclick = function () { window.open(tmdbUrl, '_blank'); };
        card.style.cursor = 'pointer';
        var pw = card.querySelector('.movie-poster-wrap');
        pw.innerHTML =
          (poster
            ? '<img class="movie-poster" src="' + BASE_IMG + poster + '" alt="' + title + '" onerror="this.style.display=\'none\';this.nextSibling.style.display=\'flex\'">'
              + '<div class="movie-poster-ph" style="display:none"><span class="movie-poster-ph-letter">' + title[0] + '</span></div>'
            : '<div class="movie-poster-ph"><span class="movie-poster-ph-letter">' + title[0] + '</span></div>') +
          '<span class="movie-type-badge">' + (item.type === 'tv' ? 'TV' : 'Film') + '</span>';
        card.querySelector('.movie-title').textContent = title;
        card.querySelector('.movie-year').textContent  = year;
      }).catch(function () {
        card.querySelector('.movie-title').textContent = 'TMDB #' + item.tmdbId;
        card.querySelector('.movie-poster-wrap').querySelector('.movie-spinner').style.display = 'none';
      });
    } else {
      var pw = card.querySelector('.movie-poster-wrap');
      pw.innerHTML = '<div class="movie-poster-ph"><span class="movie-poster-ph-letter">?</span></div><span class="movie-type-badge">' + (item.type === 'tv' ? 'TV' : 'Film') + '</span>';
      card.querySelector('.movie-title').textContent = 'Add TMDB API key';
    }
  });
})();

// Animate sections on scroll
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.style.opacity = '1';
      entry.target.style.transform = 'translateY(0)';
      observer.unobserve(entry.target);
    }
  });
}, { threshold: 0.1 });

document.querySelectorAll('.section').forEach(el => {
  el.style.transition = 'opacity 0.7s ease, transform 0.7s ease';
  observer.observe(el);
});

// Animate progress bars
const barObserver = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.querySelectorAll('.progress-fill').forEach(fill => {
        const w = fill.style.width;
        fill.style.width = '0%';
        setTimeout(() => { fill.style.width = w; }, 100);
      });
      barObserver.unobserve(entry.target);
    }
  });
}, { threshold: 0.3 });

document.querySelectorAll('.stat-card').forEach(el => barObserver.observe(el));
</script>

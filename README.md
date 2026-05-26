<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Rishi — Achievement Timeline</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=JetBrains+Mono:wght@400;700&display=swap');

  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: #050a0f;
    font-family: 'Space Grotesk', sans-serif;
    min-height: 100vh;
    overflow-x: hidden;
  }

  .grid-bg {
    position: fixed; inset: 0;
    background-image:
      linear-gradient(rgba(0,255,136,0.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,255,136,0.04) 1px, transparent 1px);
    background-size: 40px 40px;
    pointer-events: none; z-index: 0;
  }

  .scanline {
    position: fixed; inset: 0;
    background: repeating-linear-gradient(0deg, transparent, transparent 2px, rgba(0,0,0,0.12) 2px, rgba(0,0,0,0.12) 4px);
    pointer-events: none; z-index: 1;
  }

  .particles {
    position: fixed; inset: 0;
    pointer-events: none; z-index: 0; overflow: hidden;
  }

  .particle {
    position: absolute;
    border-radius: 50%;
    animation: float linear infinite;
    opacity: 0;
  }

  @keyframes float {
    0%   { transform: translateY(100vh) translateX(0); opacity: 0; }
    10%  { opacity: 0.6; }
    90%  { opacity: 0.3; }
    100% { transform: translateY(-10vh) translateX(var(--drift)); opacity: 0; }
  }

  .scene {
    position: relative; z-index: 10;
    padding: 56px 32px 72px;
    max-width: 820px;
    margin: 0 auto;
  }

  /* ── HEADER ── */
  .header {
    text-align: center;
    margin-bottom: 60px;
    animation: fadeDown 0.9s ease both;
  }

  .header-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px; letter-spacing: 4px;
    color: #00ff88; text-transform: uppercase;
    margin-bottom: 14px; opacity: 0.7;
  }

  .header h1 {
    font-size: 34px; font-weight: 700;
    color: #fff; letter-spacing: -0.5px;
    text-shadow: 0 0 60px rgba(0,255,136,0.25);
  }

  .header h1 span { color: #00ff88; }

  .header-sub {
    margin-top: 10px; font-size: 14px;
    color: rgba(255,255,255,0.4);
    font-family: 'JetBrains Mono', monospace;
    letter-spacing: 1px;
  }

  .pulse-line {
    width: 80px; height: 2px;
    background: linear-gradient(90deg, transparent, #00ff88, transparent);
    margin: 18px auto 0;
    animation: pulseW 2.2s ease-in-out infinite;
  }

  @keyframes pulseW {
    0%,100% { width:80px; opacity:0.6; }
    50%      { width:130px; opacity:1; }
  }

  /* ── TIMELINE ── */
  .timeline {
    position: relative;
  }

  .spine {
    position: absolute;
    left: 29px; top: 0; bottom: 0; width: 2px;
    background: linear-gradient(180deg, #ff6b35 0%, #00aaff 35%, #00ff88 65%, #9b59b6 100%);
    box-shadow: 0 0 14px rgba(0,255,136,0.35);
  }

  .spine::after {
    content: '';
    position: absolute;
    left: -2px; width: 6px; height: 40px;
    background: white; filter: blur(4px); opacity: 0.7;
    animation: travel 4.5s ease-in-out infinite;
  }

  @keyframes travel {
    0%   { top:0%;   opacity:0; }
    8%   { opacity:0.8; }
    92%  { opacity:0.5; }
    100% { top:100%; opacity:0; }
  }

  /* ── YEAR GROUP ── */
  .year-group {
    margin-bottom: 44px;
    animation: slideIn 0.7s ease both;
  }
  .year-group:nth-child(1) { animation-delay: 0.15s; }
  .year-group:nth-child(2) { animation-delay: 0.35s; }
  .year-group:nth-child(3) { animation-delay: 0.55s; }
  .year-group:nth-child(4) { animation-delay: 0.75s; }

  @keyframes slideIn {
    from { opacity:0; transform:translateX(28px); }
    to   { opacity:1; transform:translateX(0); }
  }

  .year-marker {
    display: flex; align-items: center;
    gap: 18px; margin-bottom: 20px;
  }

  .year-node {
    width: 60px; height: 60px; border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-family: 'JetBrains Mono', monospace;
    font-weight: 700; font-size: 13px;
    flex-shrink: 0; position: relative; z-index: 2;
    cursor: default;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }
  .year-node:hover { transform: scale(1.12) rotate(6deg); }

  .y2024 {
    background: linear-gradient(135deg,#1a0800,#3d1500);
    border: 2px solid #ff6b35; color: #ff6b35;
    box-shadow: 0 0 22px rgba(255,107,53,0.45), inset 0 0 16px rgba(255,107,53,0.1);
  }
  .y2025 {
    background: linear-gradient(135deg,#001a0a,#003d18);
    border: 2px solid #00ff88; color: #00ff88;
    box-shadow: 0 0 22px rgba(0,255,136,0.45), inset 0 0 16px rgba(0,255,136,0.1);
  }
  .yrange {
    background: linear-gradient(135deg,#0e0020,#200046);
    border: 2px solid #9b59b6; color: #b27fd6;
    box-shadow: 0 0 22px rgba(155,89,182,0.45), inset 0 0 16px rgba(155,89,182,0.1);
    font-size: 10px; text-align: center; line-height: 1.3;
  }

  .year-label {
    font-size: 19px; font-weight: 700;
    color: rgba(255,255,255,0.88); letter-spacing: 0.5px;
  }

  /* ── CARDS ── */
  .cards-container {
    padding-left: 80px;
    display: flex; flex-direction: column; gap: 14px;
  }

  .achievement-card {
    position: relative;
    background: rgba(255,255,255,0.03);
    border-radius: 18px;
    padding: 22px 26px;
    border: 1px solid rgba(255,255,255,0.07);
    cursor: pointer;
    transition: transform 0.32s cubic-bezier(0.23,1,0.32,1),
                box-shadow 0.32s ease,
                border-color 0.32s ease;
    transform-style: preserve-3d;
    transform: perspective(900px) rotateX(0deg) rotateY(0deg);
    overflow: hidden;
    will-change: transform;
  }

  /* glow layer */
  .achievement-card::before {
    content: ''; position: absolute; inset: 0;
    border-radius: 18px; opacity: 0;
    transition: opacity 0.3s; pointer-events: none;
  }
  .achievement-card.orange::before { background: linear-gradient(135deg, rgba(255,107,53,0.09), transparent 55%); border: 1px solid rgba(255,107,53,0.35); }
  .achievement-card.blue::before   { background: linear-gradient(135deg, rgba(0,170,255,0.09),  transparent 55%); border: 1px solid rgba(0,170,255,0.35); }
  .achievement-card.green::before  { background: linear-gradient(135deg, rgba(0,255,136,0.09),  transparent 55%); border: 1px solid rgba(0,255,136,0.35); }
  .achievement-card.purple::before { background: linear-gradient(135deg, rgba(155,89,182,0.09), transparent 55%); border: 1px solid rgba(155,89,182,0.35); }

  .achievement-card:hover::before { opacity: 1; }

  .achievement-card.orange:hover { box-shadow: -10px 10px 36px rgba(255,107,53,0.22), 0 0 0 1px rgba(255,107,53,0.3); border-color:transparent; }
  .achievement-card.blue:hover   { box-shadow: -10px 10px 36px rgba(0,170,255,0.22),  0 0 0 1px rgba(0,170,255,0.3);  border-color:transparent; }
  .achievement-card.green:hover  { box-shadow: -10px 10px 36px rgba(0,255,136,0.22),  0 0 0 1px rgba(0,255,136,0.3);  border-color:transparent; }
  .achievement-card.purple:hover { box-shadow: -10px 10px 36px rgba(155,89,182,0.22), 0 0 0 1px rgba(155,89,182,0.3); border-color:transparent; }

  /* shine sweep */
  .shine {
    position: absolute;
    top:-100%; left:-100%;
    width:300%; height:300%;
    background: linear-gradient(135deg,transparent 40%,rgba(255,255,255,0.055) 50%,transparent 60%);
    pointer-events: none;
    transition: transform 0s;
  }
  .achievement-card:hover .shine {
    transform: translate(55%,55%);
    transition: transform 0.65s ease;
  }

  /* right accent bar */
  .card-accent {
    position: absolute; right:0; top:0; bottom:0;
    width: 3px; border-radius: 0 18px 18px 0;
    transition: width 0.25s ease;
  }
  .achievement-card:hover .card-accent { width: 5px; }
  .accent-orange { background: linear-gradient(180deg,#ff6b35,#ff3200); }
  .accent-blue   { background: linear-gradient(180deg,#00aaff,#0055cc); }
  .accent-green  { background: linear-gradient(180deg,#00ff88,#00cc66); }
  .accent-purple { background: linear-gradient(180deg,#9b59b6,#6c3483); }

  .card-inner {
    display: flex; align-items: flex-start; gap: 18px;
    position: relative; z-index: 2;
  }

  .card-icon {
    width: 48px; height: 48px; border-radius: 14px;
    display: flex; align-items: center; justify-content: center;
    font-size: 22px; flex-shrink: 0;
    transition: transform 0.3s ease;
  }
  .achievement-card:hover .card-icon { transform: scale(1.12) rotate(-5deg); }

  .card-icon.orange { background:rgba(255,107,53,0.14); border:1px solid rgba(255,107,53,0.25); }
  .card-icon.blue   { background:rgba(0,170,255,0.14);  border:1px solid rgba(0,170,255,0.25); }
  .card-icon.green  { background:rgba(0,255,136,0.14);  border:1px solid rgba(0,255,136,0.25); }
  .card-icon.purple { background:rgba(155,89,182,0.14); border:1px solid rgba(155,89,182,0.25); }

  .card-text { flex: 1; }

  .card-title {
    font-size: 15px; font-weight: 600;
    color: #fff; margin-bottom: 5px; line-height: 1.35;
  }

  .card-sub {
    font-size: 13px; color: rgba(255,255,255,0.48); line-height: 1.55;
  }

  .card-badge {
    display: inline-flex; align-items: center; gap: 6px;
    padding: 5px 14px; border-radius: 20px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px; font-weight: 700; margin-top: 12px;
    letter-spacing: 0.4px; transition: transform 0.2s ease;
  }
  .achievement-card:hover .card-badge { transform: translateX(4px); }

  .badge-orange { background:rgba(255,107,53,0.14); color:#ff6b35; border:1px solid rgba(255,107,53,0.3); }
  .badge-blue   { background:rgba(0,170,255,0.14);  color:#00aaff; border:1px solid rgba(0,170,255,0.3); }
  .badge-green  { background:rgba(0,255,136,0.14);  color:#00ff88; border:1px solid rgba(0,255,136,0.3); }
  .badge-purple { background:rgba(155,89,182,0.14); color:#c39bd3; border:1px solid rgba(155,89,182,0.3); }

  /* ── SOCIAL FOOTER ── */
  .social-footer {
    margin-top: 64px; text-align: center;
    animation: fadeUp 1s ease 0.9s both;
  }

  .footer-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px; letter-spacing: 3px;
    color: rgba(255,255,255,0.28); text-transform: uppercase;
    margin-bottom: 22px;
  }

  .social-links {
    display: flex; justify-content: center;
    flex-wrap: wrap; gap: 10px;
  }

  .social-btn {
    display: inline-flex; align-items: center; gap: 9px;
    padding: 11px 20px; border-radius: 13px;
    text-decoration: none; font-size: 13px; font-weight: 600;
    letter-spacing: 0.2px; border: 1px solid;
    transition: all 0.28s cubic-bezier(0.23,1,0.32,1);
    position: relative; overflow: hidden; cursor: pointer;
  }
  .social-btn::before {
    content:''; position:absolute; inset:0; opacity:0; transition:opacity 0.25s;
  }
  .social-btn:hover { transform: translateY(-4px) scale(1.05); }
  .social-btn:hover::before { opacity:1; }
  .social-btn svg { flex-shrink: 0; }

  .btn-github   { color:#fff;    border-color:rgba(255,255,255,0.18); background:rgba(255,255,255,0.05); }
  .btn-github::before   { background:rgba(255,255,255,0.07); }
  .btn-github:hover     { box-shadow:0 10px 28px rgba(255,255,255,0.1); }

  .btn-linkedin { color:#38bdf8; border-color:rgba(56,189,248,0.3); background:rgba(56,189,248,0.07); }
  .btn-linkedin::before { background:rgba(56,189,248,0.1); }
  .btn-linkedin:hover   { box-shadow:0 10px 28px rgba(56,189,248,0.2); }

  .btn-email    { color:#ff6b35; border-color:rgba(255,107,53,0.3); background:rgba(255,107,53,0.07); }
  .btn-email::before    { background:rgba(255,107,53,0.1); }
  .btn-email:hover      { box-shadow:0 10px 28px rgba(255,107,53,0.2); }

  .btn-whatsapp { color:#00ff88; border-color:rgba(0,255,136,0.3); background:rgba(0,255,136,0.07); }
  .btn-whatsapp::before { background:rgba(0,255,136,0.1); }
  .btn-whatsapp:hover   { box-shadow:0 10px 28px rgba(0,255,136,0.2); }

  .btn-portfolio { color:#c39bd3; border-color:rgba(155,89,182,0.3); background:rgba(155,89,182,0.07); }
  .btn-portfolio::before { background:rgba(155,89,182,0.1); }
  .btn-portfolio:hover   { box-shadow:0 10px 28px rgba(155,89,182,0.2); }

  /* ── KEYFRAMES ── */
  @keyframes fadeDown {
    from { opacity:0; transform:translateY(-22px); }
    to   { opacity:1; transform:translateY(0); }
  }
  @keyframes fadeUp {
    from { opacity:0; transform:translateY(22px); }
    to   { opacity:1; transform:translateY(0); }
  }

  /* ── CURSOR GLOW ── */
  .cursor-glow {
    position: fixed; pointer-events: none;
    width: 320px; height: 320px;
    border-radius: 50%; z-index: 0;
    background: radial-gradient(circle, rgba(0,255,136,0.06) 0%, transparent 70%);
    transform: translate(-50%, -50%);
    transition: left 0.08s, top 0.08s;
  }
</style>
</head>
<body>

<div class="cursor-glow" id="cursorGlow"></div>
<div class="particles" id="particles"></div>
<div class="grid-bg"></div>
<div class="scanline"></div>

<div class="scene">

  <!-- HEADER -->
  <div class="header">
    <div class="header-label">// achievement_timeline.log</div>
    <h1>Hall of <span>Wins</span></h1>
    <div class="header-sub">M Anantha Krishna Rishi · Bangalore, India</div>
    <div class="pulse-line"></div>
  </div>

  <!-- TIMELINE -->
  <div class="timeline">
    <div class="spine"></div>

    <!-- ── 2024 ── -->
    <div class="year-group">
      <div class="year-marker">
        <div class="year-node y2024">2024</div>
        <div class="year-label">The Breakthrough Year 🔥</div>
      </div>
      <div class="cards-container">

        <div class="achievement-card orange" onmousemove="tilt(event,this)" onmouseleave="resetTilt(this)">
          <div class="shine"></div>
          <div class="card-accent accent-orange"></div>
          <div class="card-inner">
            <div class="card-icon orange">🥉</div>
            <div class="card-text">
              <div class="card-title">Codeathon 2024 — 2nd Runner Up</div>
              <div class="card-sub">IIIT Bangalore Innovation Center × RBIH</div>
              <div class="card-badge badge-orange">💰 ₹75,000 Prize Money</div>
            </div>
          </div>
        </div>

        <div class="achievement-card blue" onmousemove="tilt(event,this)" onmouseleave="resetTilt(this)">
          <div class="shine"></div>
          <div class="card-accent accent-blue"></div>
          <div class="card-inner">
            <div class="card-icon blue">⛓️</div>
            <div class="card-text">
              <div class="card-title">Algorand Global Hackathon — Best Use of Blockchain</div>
              <div class="card-sub">Built Campus Founders · Blockchain-verified startup platform</div>
              <div class="card-badge badge-blue">🌐 $500 USD Award</div>
            </div>
          </div>
        </div>

      </div>
    </div>

    <!-- ── 2025 ── -->
    <div class="year-group">
      <div class="year-marker">
        <div class="year-node y2025">2025</div>
        <div class="year-label">The Ecosystem Entry 🚀</div>
      </div>
      <div class="cards-container">

        <div class="achievement-card green" onmousemove="tilt(event,this)" onmouseleave="resetTilt(this)">
          <div class="shine"></div>
          <div class="card-accent accent-green"></div>
          <div class="card-inner">
            <div class="card-icon green">🎯</div>
            <div class="card-text">
              <div class="card-title">RBIH Co-Incubation Program</div>
              <div class="card-sub">Selected by RBIH × VTU × KSHEC — Top entrepreneur from Karnataka</div>
              <div class="card-badge badge-green">🚀 Top 100 of 7,000+ Students</div>
            </div>
          </div>
        </div>

      </div>
    </div>

    <!-- ── 2022–Present ── -->
    <div class="year-group">
      <div class="year-marker">
        <div class="year-node yrange">2022<br/>–Now</div>
        <div class="year-label">Beyond the Code 🏏</div>
      </div>
      <div class="cards-container">

        <div class="achievement-card purple" onmousemove="tilt(event,this)" onmouseleave="resetTilt(this)">
          <div class="shine"></div>
          <div class="card-accent accent-purple"></div>
          <div class="card-inner">
            <div class="card-icon purple">🏏</div>
            <div class="card-text">
              <div class="card-title">College Cricket Team — Official Representative</div>
              <div class="card-sub">East Point College of Engineering & Technology · Inter-college tournament player</div>
              <div class="card-badge badge-purple">⚾ Team Player On & Off the Field</div>
            </div>
          </div>
        </div>

      </div>
    </div>
  </div><!-- /timeline -->

  <!-- SOCIAL FOOTER -->
  <div class="social-footer">
    <div class="footer-label">// connect.with(rishi)</div>
    <div class="social-links">

      <a class="social-btn btn-github" href="https://github.com/RISHIMAJETI" target="_blank">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z"/></svg>
        GitHub
      </a>

      <a class="social-btn btn-linkedin" href="https://www.linkedin.com/in/m-anantha-krishna-rishi-01b6102b4/" target="_blank">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
        LinkedIn
      </a>

      <a class="social-btn btn-email" href="mailto:rishimajeti060@gmail.com">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>
        Email Me
      </a>

      <a class="social-btn btn-whatsapp" href="https://wa.me/917021983368?text=Hey%20Rishi!%20I%20saw%20your%20GitHub%20profile%20%E2%80%94%20let%27s%20connect!%20%F0%9F%9A%80" target="_blank">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 0 1-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 0 1-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 0 1 2.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0 0 12.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 0 0 5.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 0 0-3.48-8.413z"/></svg>
        WhatsApp
      </a>

      <a class="social-btn btn-portfolio" href="https://myportfolio-rishimajeti.vercel.app/" target="_blank">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><line x1="2" y1="12" x2="22" y2="12"/><path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"/></svg>
        Portfolio
      </a>

    </div>
  </div>

</div><!-- /scene -->

<script>
  /* 3D TILT */
  function tilt(e, card) {
    const r = card.getBoundingClientRect();
    const x = e.clientX - r.left, y = e.clientY - r.top;
    const cx = r.width / 2, cy = r.height / 2;
    const rx = ((y - cy) / cy) * 7;
    const ry = ((cx - x) / cx) * 7;
    card.style.transform = `perspective(900px) rotateX(${rx}deg) rotateY(${ry}deg) translateZ(10px) scale(1.025)`;
  }
  function resetTilt(card) {
    card.style.transform = 'perspective(900px) rotateX(0deg) rotateY(0deg) translateZ(0) scale(1)';
  }

  /* CURSOR GLOW */
  const glow = document.getElementById('cursorGlow');
  document.addEventListener('mousemove', e => {
    glow.style.left = e.clientX + 'px';
    glow.style.top  = e.clientY + 'px';
  });

  /* FLOATING PARTICLES */
  const colors = ['#00ff88','#ff6b35','#00aaff','#9b59b6','#ffffff'];
  const pc = document.getElementById('particles');
  for (let i = 0; i < 30; i++) {
    const p = document.createElement('div');
    p.className = 'particle';
    const size = 1.5 + Math.random() * 2.5;
    p.style.cssText = `
      left:${Math.random()*100}%;
      background:${colors[Math.floor(Math.random()*colors.length)]};
      animation-duration:${7+Math.random()*11}s;
      animation-delay:${Math.random()*10}s;
      --drift:${(Math.random()-.5)*100}px;
      width:${size}px; height:${size}px; opacity:0;
    `;
    pc.appendChild(p);
  }
</script>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>RISHIMAJETI — GitHub Profile</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;600&family=Syne:wght@700;800&display=swap" rel="stylesheet"/>
<style>
  :root {
    --cyan: #00f5ff;
    --violet: #7b2fff;
    --pink: #ff2d78;
    --dark: #020408;
    --dark2: #080d14;
    --dark3: #0d1520;
    --glass: rgba(255,255,255,0.04);
    --glass-border: rgba(0,245,255,0.15);
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--dark);
    color: #e8eaf0;
    font-family: 'Space Grotesk', sans-serif;
    overflow-x: hidden;
    min-height: 100vh;
  }

  /* ── CANVAS BACKGROUND ── */
  #bg-canvas {
    position: fixed;
    inset: 0;
    z-index: 0;
    pointer-events: none;
  }

  /* ── NOISE OVERLAY ── */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 1;
    opacity: 0.6;
  }

  .content { position: relative; z-index: 2; }

  /* ── HERO ── */
  .hero {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
    padding: 2rem;
    position: relative;
  }

  .hero-badge {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: rgba(0,245,255,0.08);
    border: 1px solid rgba(0,245,255,0.25);
    border-radius: 100px;
    padding: 6px 18px;
    font-size: 12px;
    font-family: 'JetBrains Mono', monospace;
    color: var(--cyan);
    letter-spacing: 0.08em;
    margin-bottom: 2rem;
    animation: fadeSlideDown 0.8s ease both;
  }

  .hero-badge::before {
    content: '';
    width: 6px; height: 6px;
    background: var(--cyan);
    border-radius: 50%;
    box-shadow: 0 0 8px var(--cyan);
    animation: pulse 2s infinite;
  }

  .hero-name {
    font-family: 'Syne', sans-serif;
    font-size: clamp(3rem, 8vw, 7rem);
    font-weight: 800;
    line-height: 1;
    letter-spacing: -0.02em;
    background: linear-gradient(135deg, #fff 0%, var(--cyan) 50%, var(--violet) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    animation: fadeSlideUp 0.8s 0.2s ease both;
    margin-bottom: 0.5rem;
  }

  .hero-sub {
    font-size: clamp(1rem, 2.5vw, 1.4rem);
    color: rgba(255,255,255,0.45);
    font-weight: 300;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    animation: fadeSlideUp 0.8s 0.35s ease both;
    margin-bottom: 2.5rem;
  }

  /* ── TYPING ── */
  .typing-wrap {
    height: 2.2rem;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 3rem;
    animation: fadeSlideUp 0.8s 0.5s ease both;
  }

  .typing-text {
    font-family: 'JetBrains Mono', monospace;
    font-size: clamp(0.85rem, 2vw, 1.1rem);
    color: var(--cyan);
    border-right: 2px solid var(--cyan);
    white-space: nowrap;
    overflow: hidden;
    animation: blink 0.8s step-end infinite;
  }

  /* ── HERO BUTTONS ── */
  .hero-btns {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    justify-content: center;
    animation: fadeSlideUp 0.8s 0.65s ease both;
  }

  .btn-primary {
    padding: 14px 32px;
    background: linear-gradient(135deg, var(--cyan), var(--violet));
    color: #000;
    font-weight: 700;
    font-size: 14px;
    border-radius: 100px;
    border: none;
    cursor: pointer;
    text-decoration: none;
    display: inline-block;
    transition: transform 0.2s, box-shadow 0.2s;
    letter-spacing: 0.04em;
    box-shadow: 0 0 30px rgba(0,245,255,0.3);
  }

  .btn-primary:hover {
    transform: translateY(-2px) scale(1.03);
    box-shadow: 0 0 50px rgba(0,245,255,0.5);
  }

  .btn-ghost {
    padding: 13px 32px;
    background: transparent;
    color: #fff;
    font-weight: 600;
    font-size: 14px;
    border-radius: 100px;
    border: 1px solid rgba(255,255,255,0.2);
    cursor: pointer;
    text-decoration: none;
    display: inline-block;
    transition: transform 0.2s, border-color 0.2s, box-shadow 0.2s;
    letter-spacing: 0.04em;
    backdrop-filter: blur(10px);
  }

  .btn-ghost:hover {
    transform: translateY(-2px);
    border-color: var(--cyan);
    box-shadow: 0 0 20px rgba(0,245,255,0.15);
  }

  /* ── SCROLL INDICATOR ── */
  .scroll-hint {
    position: absolute;
    bottom: 2.5rem;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 6px;
    opacity: 0.4;
    animation: fadeIn 1.5s 1.5s ease both;
  }

  .scroll-hint span { font-size: 11px; letter-spacing: 0.1em; text-transform: uppercase; color: #fff; }

  .scroll-arrow {
    width: 24px; height: 24px;
    border-right: 1.5px solid #fff;
    border-bottom: 1.5px solid #fff;
    transform: rotate(45deg);
    animation: scrollBounce 1.5s ease-in-out infinite;
  }

  /* ── SECTION BASE ── */
  section {
    padding: 6rem 2rem;
    max-width: 1100px;
    margin: 0 auto;
  }

  .section-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--cyan);
    margin-bottom: 0.75rem;
    opacity: 0.8;
  }

  .section-title {
    font-family: 'Syne', sans-serif;
    font-size: clamp(2rem, 4vw, 3rem);
    font-weight: 800;
    line-height: 1.1;
    color: #fff;
    margin-bottom: 1rem;
  }

  .section-title span {
    background: linear-gradient(135deg, var(--cyan), var(--violet));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .divider {
    width: 100%;
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--cyan), var(--violet), transparent);
    margin: 0;
    opacity: 0.3;
  }

  /* ── ABOUT ── */
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 3rem;
    align-items: start;
    margin-top: 3rem;
  }

  .about-code {
    background: var(--dark2);
    border: 1px solid var(--glass-border);
    border-radius: 16px;
    overflow: hidden;
    position: relative;
  }

  .code-header {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 14px 18px;
    background: rgba(255,255,255,0.03);
    border-bottom: 1px solid rgba(255,255,255,0.05);
  }

  .dot { width: 12px; height: 12px; border-radius: 50%; }
  .dot.r { background: #ff5f57; }
  .dot.y { background: #febc2e; }
  .dot.g { background: #28c840; }

  .code-file {
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    color: rgba(255,255,255,0.35);
    margin-left: 8px;
  }

  .code-body {
    padding: 1.5rem;
    font-family: 'JetBrains Mono', monospace;
    font-size: 13px;
    line-height: 2;
    color: #cdd6f4;
  }

  .kw { color: #cba6f7; }
  .fn { color: #89b4fa; }
  .str { color: #a6e3a1; }
  .cm { color: #585b70; }
  .num { color: #fab387; }
  .prop { color: #89dceb; }

  .about-info { display: flex; flex-direction: column; gap: 1.5rem; }

  .info-card {
    background: var(--glass);
    border: 1px solid var(--glass-border);
    border-radius: 16px;
    padding: 1.5rem;
    backdrop-filter: blur(10px);
    transition: transform 0.3s, border-color 0.3s, box-shadow 0.3s;
  }

  .info-card:hover {
    transform: translateY(-4px);
    border-color: rgba(0,245,255,0.4);
    box-shadow: 0 20px 40px rgba(0,0,0,0.4), 0 0 30px rgba(0,245,255,0.08);
  }

  .info-card h3 {
    font-size: 13px;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    color: var(--cyan);
    margin-bottom: 0.5rem;
    font-family: 'JetBrains Mono', monospace;
  }

  .info-card p { color: rgba(255,255,255,0.7); line-height: 1.6; font-size: 15px; }

  /* ── TECH STACK ── */
  .tech-section { padding: 6rem 2rem; }
  .tech-inner { max-width: 1100px; margin: 0 auto; }

  .tech-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
    gap: 1rem;
    margin-top: 3rem;
  }

  .tech-card {
    background: var(--glass);
    border: 1px solid rgba(255,255,255,0.06);
    border-radius: 14px;
    padding: 1.25rem 1rem;
    text-align: center;
    cursor: default;
    transition: transform 0.3s cubic-bezier(.34,1.56,.64,1), border-color 0.3s, box-shadow 0.3s;
    position: relative;
    overflow: hidden;
  }

  .tech-card::before {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(circle at 50% 0%, rgba(0,245,255,0.1) 0%, transparent 70%);
    opacity: 0;
    transition: opacity 0.3s;
  }

  .tech-card:hover {
    transform: translateY(-8px) scale(1.03);
    border-color: rgba(0,245,255,0.35);
    box-shadow: 0 20px 40px rgba(0,0,0,0.5), 0 0 25px rgba(0,245,255,0.1);
  }

  .tech-card:hover::before { opacity: 1; }

  .tech-icon { font-size: 2rem; margin-bottom: 0.5rem; display: block; }
  .tech-name { font-size: 12px; font-weight: 600; color: rgba(255,255,255,0.8); letter-spacing: 0.04em; }
  .tech-cat { font-size: 10px; color: rgba(255,255,255,0.3); font-family: 'JetBrains Mono', monospace; margin-top: 2px; }

  /* ── STATS ── */
  .stats-section { padding: 6rem 2rem; background: rgba(0,0,0,0.2); }
  .stats-inner { max-width: 1100px; margin: 0 auto; }

  .stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1.5rem;
    margin-top: 3rem;
  }

  .stat-card {
    background: var(--dark2);
    border: 1px solid var(--glass-border);
    border-radius: 20px;
    padding: 2rem;
    text-align: center;
    position: relative;
    overflow: hidden;
    transition: transform 0.3s, box-shadow 0.3s;
  }

  .stat-card::after {
    content: '';
    position: absolute;
    bottom: 0; left: 0; right: 0;
    height: 3px;
    background: linear-gradient(90deg, var(--cyan), var(--violet));
  }

  .stat-card:hover {
    transform: translateY(-6px);
    box-shadow: 0 25px 50px rgba(0,0,0,0.5), 0 0 40px rgba(0,245,255,0.08);
  }

  .stat-num {
    font-family: 'Syne', sans-serif;
    font-size: 3.5rem;
    font-weight: 800;
    background: linear-gradient(135deg, var(--cyan), var(--violet));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    line-height: 1;
    margin-bottom: 0.5rem;
  }

  .stat-label { font-size: 13px; color: rgba(255,255,255,0.5); text-transform: uppercase; letter-spacing: 0.1em; }

  /* ── GITHUB STATS CARDS ── */
  .gh-stats { margin-top: 3rem; }
  .gh-stats-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 1.5rem; margin-top: 1.5rem; }

  .gh-card {
    background: var(--dark2);
    border: 1px solid var(--glass-border);
    border-radius: 16px;
    overflow: hidden;
    transition: transform 0.3s, box-shadow 0.3s;
  }

  .gh-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 20px 40px rgba(0,0,0,0.5), 0 0 30px rgba(0,245,255,0.1);
  }

  .gh-card img { width: 100%; display: block; }

  .gh-streak { grid-column: 1 / -1; }

  /* ── PROJECTS ── */
  .projects-section { padding: 6rem 2rem; }
  .projects-inner { max-width: 1100px; margin: 0 auto; }

  .projects-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 1.5rem; margin-top: 3rem; }

  .project-card {
    background: var(--dark2);
    border: 1px solid rgba(255,255,255,0.06);
    border-radius: 20px;
    padding: 2rem;
    position: relative;
    overflow: hidden;
    cursor: default;
    transition: transform 0.4s cubic-bezier(.34,1.2,.64,1), box-shadow 0.4s, border-color 0.3s;
    transform-style: preserve-3d;
  }

  .project-card::before {
    content: '';
    position: absolute;
    top: -50%; left: -50%;
    width: 200%; height: 200%;
    background: conic-gradient(from 0deg, transparent 0deg, rgba(0,245,255,0.06) 60deg, transparent 120deg);
    animation: rotateBg 8s linear infinite;
    opacity: 0;
    transition: opacity 0.4s;
  }

  .project-card:hover {
    transform: translateY(-10px) rotateX(3deg);
    box-shadow: 0 30px 60px rgba(0,0,0,0.6), 0 0 50px rgba(0,245,255,0.12);
    border-color: rgba(0,245,255,0.3);
  }

  .project-card:hover::before { opacity: 1; }

  .project-header {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    margin-bottom: 1rem;
  }

  .project-icon { font-size: 2.5rem; }

  .project-tag {
    font-size: 10px;
    font-family: 'JetBrains Mono', monospace;
    padding: 4px 10px;
    border-radius: 100px;
    border: 1px solid;
    text-transform: uppercase;
    letter-spacing: 0.08em;
  }

  .tag-live { color: #28c840; border-color: rgba(40,200,64,0.3); background: rgba(40,200,64,0.08); }
  .tag-build { color: var(--cyan); border-color: rgba(0,245,255,0.3); background: rgba(0,245,255,0.06); }

  .project-title {
    font-family: 'Syne', sans-serif;
    font-size: 1.4rem;
    font-weight: 800;
    color: #fff;
    margin-bottom: 0.5rem;
  }

  .project-desc { color: rgba(255,255,255,0.55); font-size: 14px; line-height: 1.7; margin-bottom: 1.5rem; }

  .project-stack { display: flex; flex-wrap: wrap; gap: 6px; margin-bottom: 1.5rem; }

  .stack-pill {
    font-size: 11px;
    font-family: 'JetBrains Mono', monospace;
    padding: 4px 10px;
    background: rgba(123,47,255,0.12);
    border: 1px solid rgba(123,47,255,0.25);
    border-radius: 100px;
    color: rgba(200,180,255,0.9);
  }

  .project-links { display: flex; gap: 10px; }

  .proj-link {
    display: inline-flex;
    align-items: center;
    gap: 5px;
    font-size: 12px;
    font-weight: 600;
    color: var(--cyan);
    text-decoration: none;
    padding: 7px 14px;
    border: 1px solid rgba(0,245,255,0.25);
    border-radius: 100px;
    transition: background 0.2s, box-shadow 0.2s;
  }

  .proj-link:hover {
    background: rgba(0,245,255,0.1);
    box-shadow: 0 0 15px rgba(0,245,255,0.15);
  }

  /* ── ACHIEVEMENTS ── */
  .achievements-section { padding: 6rem 2rem; background: rgba(0,0,0,0.2); }
  .achievements-inner { max-width: 1100px; margin: 0 auto; }

  .achievements-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 1.5rem; margin-top: 3rem; }

  .achievement-card {
    background: var(--dark2);
    border: 1px solid var(--glass-border);
    border-radius: 20px;
    padding: 2rem 1.5rem;
    position: relative;
    overflow: hidden;
    transition: transform 0.3s, box-shadow 0.3s;
  }

  .achievement-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 3px;
    background: linear-gradient(90deg, var(--cyan), var(--violet), var(--pink));
  }

  .achievement-card:hover {
    transform: translateY(-6px) scale(1.02);
    box-shadow: 0 20px 40px rgba(0,0,0,0.5), 0 0 30px rgba(123,47,255,0.1);
  }

  .achievement-icon { font-size: 2.5rem; margin-bottom: 1rem; display: block; }
  .achievement-title { font-family: 'Syne', sans-serif; font-size: 1.1rem; font-weight: 800; color: #fff; margin-bottom: 0.4rem; }
  .achievement-desc { font-size: 13px; color: rgba(255,255,255,0.5); line-height: 1.6; }
  .achievement-value { font-family: 'JetBrains Mono', monospace; font-size: 1.4rem; font-weight: 600; color: var(--cyan); margin-bottom: 0.3rem; }

  /* ── EXPERIENCE ── */
  .exp-section { padding: 6rem 2rem; }
  .exp-inner { max-width: 1100px; margin: 0 auto; }

  .exp-card {
    background: var(--dark2);
    border: 1px solid var(--glass-border);
    border-radius: 20px;
    padding: 2.5rem;
    margin-top: 3rem;
    position: relative;
    overflow: hidden;
    display: grid;
    grid-template-columns: auto 1fr;
    gap: 2rem;
    align-items: start;
    transition: transform 0.3s, box-shadow 0.3s;
  }

  .exp-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 20px 40px rgba(0,0,0,0.5), 0 0 40px rgba(0,245,255,0.07);
  }

  .exp-logo {
    width: 60px; height: 60px;
    background: linear-gradient(135deg, var(--cyan), var(--violet));
    border-radius: 14px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'Syne', sans-serif;
    font-size: 1.2rem;
    font-weight: 800;
    color: #000;
    flex-shrink: 0;
  }

  .exp-info h3 { font-family: 'Syne', sans-serif; font-size: 1.3rem; font-weight: 800; color: #fff; margin-bottom: 0.25rem; }
  .exp-info h4 { font-size: 14px; color: var(--cyan); margin-bottom: 0.5rem; font-weight: 500; }
  .exp-meta { font-size: 12px; color: rgba(255,255,255,0.35); font-family: 'JetBrains Mono', monospace; margin-bottom: 1rem; }
  .exp-desc { color: rgba(255,255,255,0.6); font-size: 14px; line-height: 1.7; }

  .exp-tags { display: flex; flex-wrap: wrap; gap: 6px; margin-top: 1rem; }
  .exp-tag {
    font-size: 11px;
    font-family: 'JetBrains Mono', monospace;
    padding: 4px 10px;
    background: rgba(0,245,255,0.07);
    border: 1px solid rgba(0,245,255,0.2);
    border-radius: 100px;
    color: rgba(0,245,255,0.8);
  }

  /* ── QUOTE ── */
  .quote-section {
    padding: 6rem 2rem;
    text-align: center;
    background: radial-gradient(ellipse at 50% 50%, rgba(123,47,255,0.06) 0%, transparent 70%);
  }

  .quote-mark { font-family: 'Syne', sans-serif; font-size: 8rem; line-height: 0.5; color: rgba(0,245,255,0.15); font-weight: 800; display: block; margin-bottom: 2rem; }

  .quote-text {
    font-family: 'Syne', sans-serif;
    font-size: clamp(1.2rem, 3vw, 2rem);
    font-weight: 700;
    color: rgba(255,255,255,0.85);
    max-width: 750px;
    margin: 0 auto 1.5rem;
    line-height: 1.4;
  }

  .quote-author { font-family: 'JetBrains Mono', monospace; font-size: 13px; color: var(--cyan); opacity: 0.8; }

  /* ── CONTACT ── */
  .contact-section { padding: 6rem 2rem; }
  .contact-inner { max-width: 800px; margin: 0 auto; text-align: center; }

  .contact-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); gap: 1rem; margin-top: 3rem; }

  .contact-card {
    background: var(--dark2);
    border: 1px solid rgba(255,255,255,0.06);
    border-radius: 16px;
    padding: 1.75rem 1.25rem;
    text-decoration: none;
    color: inherit;
    transition: transform 0.3s cubic-bezier(.34,1.56,.64,1), border-color 0.3s, box-shadow 0.3s;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.75rem;
  }

  .contact-card:hover {
    transform: translateY(-8px) scale(1.03);
    border-color: var(--cyan);
    box-shadow: 0 20px 40px rgba(0,0,0,0.5), 0 0 30px rgba(0,245,255,0.12);
  }

  .contact-icon { font-size: 2rem; }
  .contact-name { font-weight: 700; font-size: 14px; color: #fff; }
  .contact-handle { font-size: 12px; color: rgba(255,255,255,0.4); font-family: 'JetBrains Mono', monospace; }

  /* ── FOOTER ── */
  footer {
    padding: 3rem 2rem;
    text-align: center;
    border-top: 1px solid rgba(255,255,255,0.05);
    color: rgba(255,255,255,0.2);
    font-size: 13px;
    font-family: 'JetBrains Mono', monospace;
  }

  footer span { color: var(--cyan); }

  /* ── SCROLL REVEAL ── */
  .reveal {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }

  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }

  /* ── ANIMATIONS ── */
  @keyframes fadeSlideDown {
    from { opacity: 0; transform: translateY(-20px); }
    to { opacity: 1; transform: translateY(0); }
  }

  @keyframes fadeSlideUp {
    from { opacity: 0; transform: translateY(25px); }
    to { opacity: 1; transform: translateY(0); }
  }

  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 0.4; }
  }

  @keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.5; transform: scale(0.8); }
  }

  @keyframes blink {
    0%, 100% { border-color: var(--cyan); }
    50% { border-color: transparent; }
  }

  @keyframes scrollBounce {
    0%, 100% { transform: rotate(45deg) translate(0, 0); }
    50% { transform: rotate(45deg) translate(4px, 4px); }
  }

  @keyframes rotateBg {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }

  @keyframes floatY {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-12px); }
  }

  /* ── 3D TILT ON PROJECT CARDS ── */
  .tilt { transform-style: preserve-3d; }

  /* ── RESPONSIVE ── */
  @media (max-width: 768px) {
    .about-grid { grid-template-columns: 1fr; }
    .gh-stats-grid { grid-template-columns: 1fr; }
    .exp-card { grid-template-columns: 1fr; }
    .hero-name { font-size: 2.8rem; }
  }
</style>
</head>
<body>

<!-- PARTICLE CANVAS -->
<canvas id="bg-canvas"></canvas>

<div class="content">

<!-- ═══ HERO ═══ -->
<div class="hero">
  <div class="hero-badge">// Available for opportunities · Bangalore, India</div>

  <h1 class="hero-name">M Anantha<br/>Krishna Rishi</h1>
  <p class="hero-sub">B.E. Computer Science · AI Engineer · Builder</p>

  <div class="typing-wrap">
    <span class="typing-text" id="typing"></span>
  </div>

  <div class="hero-btns">
    <a href="https://linkedin.com/in/RISHIMAJETI" target="_blank" class="btn-primary">Connect on LinkedIn</a>
    <a href="mailto:ananthakrishnarishi@gmail.com" class="btn-ghost">Send an Email</a>
  </div>

  <div class="scroll-hint">
    <span>Scroll</span>
    <div class="scroll-arrow"></div>
  </div>
</div>

<div class="divider"></div>

<!-- ═══ ABOUT ═══ -->
<section>
  <div class="section-label reveal">01 / About</div>
  <h2 class="section-title reveal">Coding with <span>purpose</span>,<br/>building with passion</h2>

  <div class="about-grid">
    <div class="about-code reveal">
      <div class="code-header">
        <div class="dot r"></div>
        <div class="dot y"></div>
        <div class="dot g"></div>
        <span class="code-file">rishi.py</span>
      </div>
      <div class="code-body">
<span class="cm"># CS undergrad → AI Engineer → Founder</span><br/>
<span class="kw">class</span> <span class="fn">Rishi</span>:<br/>
&nbsp;&nbsp;<span class="prop">name</span> = <span class="str">"M Anantha Krishna Rishi"</span><br/>
&nbsp;&nbsp;<span class="prop">role</span> = [<span class="str">"Data Scientist"</span>,<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="str">"Full Stack Dev"</span>,<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="str">"AI Builder"</span>]<br/>
&nbsp;&nbsp;<span class="prop">location</span> = <span class="str">"Bangalore 🇮🇳"</span><br/><br/>
&nbsp;&nbsp;<span class="kw">def</span> <span class="fn">focus</span>(<span class="prop">self</span>):<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="kw">return</span> {<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="str">"building"</span>: <span class="str">"AI-native products"</span>,<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="str">"learning"</span>: <span class="str">"MLOps · LangChain"</span>,<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="str">"mantra"</span>: <span class="str">"Ship. Learn. Repeat."</span><br/>
&nbsp;&nbsp;&nbsp;&nbsp;}<br/><br/>
&nbsp;&nbsp;<span class="kw">def</span> <span class="fn">fun_fact</span>(<span class="prop">self</span>):<br/>
&nbsp;&nbsp;&nbsp;&nbsp;<span class="kw">return</span> <span class="str">"Cricket 🏏 = strategy on and off field"</span>
      </div>
    </div>

    <div class="about-info">
      <div class="info-card reveal">
        <h3>🎯 Currently Building</h3>
        <p>AI-powered platforms solving real-world problems — from credit assessment to farmer empowerment.</p>
      </div>
      <div class="info-card reveal">
        <h3>📚 Currently Learning</h3>
        <p>MLOps pipelines, LangChain agents, advanced system design at scale, and deep reinforcement learning.</p>
      </div>
      <div class="info-card reveal">
        <h3>🤝 Open To</h3>
        <p>Internships · Research collaborations · Startup roles · High-impact engineering opportunities globally.</p>
      </div>
      <div class="info-card reveal">
        <h3>🏏 Beyond Code</h3>
        <p>College cricket team representative — discipline, team strategy, and performance under pressure.</p>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ═══ TECH STACK ═══ -->
<div class="tech-section">
  <div class="tech-inner">
    <div class="section-label reveal">02 / Arsenal</div>
    <h2 class="section-title reveal">Technology <span>stack</span></h2>

    <div class="tech-grid">
      <!-- Languages -->
      <div class="tech-card reveal"><span class="tech-icon">🐍</span><div class="tech-name">Python</div><div class="tech-cat">language</div></div>
      <div class="tech-card reveal"><span class="tech-icon">☕</span><div class="tech-name">Java</div><div class="tech-cat">language</div></div>
      <div class="tech-card reveal"><span class="tech-icon">🌐</span><div class="tech-name">JavaScript</div><div class="tech-cat">language</div></div>
      <div class="tech-card reveal"><span class="tech-icon">⚙️</span><div class="tech-name">C</div><div class="tech-cat">language</div></div>
      <!-- Frontend -->
      <div class="tech-card reveal"><span class="tech-icon">⚛️</span><div class="tech-name">React.js</div><div class="tech-cat">frontend</div></div>
      <div class="tech-card reveal"><span class="tech-icon">🎨</span><div class="tech-name">Tailwind</div><div class="tech-cat">frontend</div></div>
      <div class="tech-card reveal"><span class="tech-icon">🏗️</span><div class="tech-name">HTML5</div><div class="tech-cat">frontend</div></div>
      <div class="tech-card reveal"><span class="tech-icon">💄</span><div class="tech-name">CSS3</div><div class="tech-cat">frontend</div></div>
      <!-- Backend -->
      <div class="tech-card reveal"><span class="tech-icon">🟢</span><div class="tech-name">Node.js</div><div class="tech-cat">backend</div></div>
      <div class="tech-card reveal"><span class="tech-icon">🚂</span><div class="tech-name">Express.js</div><div class="tech-cat">backend</div></div>
      <div class="tech-card reveal"><span class="tech-icon">🔥</span><div class="tech-name">Firebase</div><div class="tech-cat">database</div></div>
      <div class="tech-card reveal"><span class="tech-icon">🗃️</span><div class="tech-name">SQL</div><div class="tech-cat">database</div></div>
      <!-- AI/ML -->
      <div class="tech-card reveal"><span class="tech-icon">🔢</span><div class="tech-name">NumPy</div><div class="tech-cat">ai / ml</div></div>
      <div class="tech-card reveal"><span class="tech-icon">🐼</span><div class="tech-name">Pandas</div><div class="tech-cat">ai / ml</div></div>
      <div class="tech-card reveal"><span class="tech-icon">📊</span><div class="tech-name">Matplotlib</div><div class="tech-cat">ai / ml</div></div>
      <div class="tech-card reveal"><span class="tech-icon">🤖</span><div class="tech-name">scikit-learn</div><div class="tech-cat">ai / ml</div></div>
      <!-- Tools -->
      <div class="tech-card reveal"><span class="tech-icon">🐙</span><div class="tech-name">Git / GitHub</div><div class="tech-cat">devops</div></div>
      <div class="tech-card reveal"><span class="tech-icon">💻</span><div class="tech-name">VS Code</div><div class="tech-cat">tooling</div></div>
      <div class="tech-card reveal"><span class="tech-icon">▲</span><div class="tech-name">Vercel</div><div class="tech-cat">deployment</div></div>
    </div>
  </div>
</div>

<div class="divider"></div>

<!-- ═══ STATS ═══ -->
<div class="stats-section">
  <div class="stats-inner">
    <div class="section-label reveal">03 / Metrics</div>
    <h2 class="section-title reveal">GitHub <span>intelligence</span></h2>

    <div class="stats-grid">
      <div class="stat-card reveal">
        <div class="stat-num" data-target="3">0</div>
        <div class="stat-label">Flagship Projects</div>
      </div>
      <div class="stat-card reveal">
        <div class="stat-num" data-target="4">0</div>
        <div class="stat-label">Awards Won</div>
      </div>
      <div class="stat-card reveal">
        <div class="stat-num" data-prefix="₹" data-target="75">0</div>
        <div class="stat-label">Prize Money (K)</div>
      </div>
      <div class="stat-card reveal">
        <div class="stat-num" data-prefix="$" data-target="500">0</div>
        <div class="stat-label">Blockchain Prize</div>
      </div>
    </div>

    <div class="gh-stats">
      <div class="gh-stats-grid">
        <div class="gh-card reveal">
          <img src="https://github-readme-stats.vercel.app/api?username=RISHIMAJETI&show_icons=true&theme=tokyonight&hide_border=true&bg_color=080d14&title_color=00f5ff&icon_color=7b2fff&text_color=ffffff&count_private=true&include_all_commits=true" alt="GitHub Stats"/>
        </div>
        <div class="gh-card reveal">
          <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=RISHIMAJETI&layout=compact&theme=tokyonight&hide_border=true&bg_color=080d14&title_color=00f5ff&text_color=ffffff&langs_count=8" alt="Top Languages"/>
        </div>
        <div class="gh-card gh-streak reveal">
          <img src="https://github-readme-streak-stats.herokuapp.com/?user=RISHIMAJETI&theme=tokyonight&hide_border=true&background=080d14&ring=00f5ff&fire=7b2fff&currStreakLabel=00f5ff&stroke=7b2fff&border=080d14" alt="Streak Stats"/>
        </div>
      </div>
    </div>

    <!-- Trophies -->
    <div style="margin-top:2rem; background:var(--dark2); border:1px solid var(--glass-border); border-radius:16px; overflow:hidden;" class="reveal">
      <img src="https://github-profile-trophy.vercel.app/?username=RISHIMAJETI&theme=onestar&no-frame=true&row=1&column=7&margin-w=4&no-bg=true" style="width:100%; display:block;" alt="Trophies"/>
    </div>
  </div>
</div>

<div class="divider"></div>

<!-- ═══ PROJECTS ═══ -->
<div class="projects-section">
  <div class="projects-inner">
    <div class="section-label reveal">04 / Work</div>
    <h2 class="section-title reveal">Flagship <span>projects</span></h2>

    <div class="projects-grid">

      <div class="project-card tilt reveal">
        <div class="project-header">
          <span class="project-icon">🧠</span>
          <span class="project-tag tag-live">● Live</span>
        </div>
        <div class="project-title">CreditWorthy</div>
        <p class="project-desc">AI-powered credit assessment platform using ML models to evaluate financial risk with precision and full transparency. Democratizing credit access for underserved populations.</p>
        <div class="project-stack">
          <span class="stack-pill">Python</span>
          <span class="stack-pill">ML</span>
          <span class="stack-pill">React</span>
          <span class="stack-pill">Node.js</span>
          <span class="stack-pill">XAI</span>
        </div>
        <div class="project-links">
          <a href="#" class="proj-link">↗ GitHub</a>
          <a href="#" class="proj-link">↗ Live Demo</a>
        </div>
      </div>

      <div class="project-card tilt reveal">
        <div class="project-header">
          <span class="project-icon">🌐</span>
          <span class="project-tag tag-build">⬡ Building</span>
        </div>
        <div class="project-title">Campus Founders</div>
        <p class="project-desc">AI + Blockchain startup ecosystem connecting student entrepreneurs with resources, mentors, and on-chain funding. $500 Algorand Hackathon Winner.</p>
        <div class="project-stack">
          <span class="stack-pill">Algorand</span>
          <span class="stack-pill">AI</span>
          <span class="stack-pill">React</span>
          <span class="stack-pill">Web3</span>
          <span class="stack-pill">Smart Contracts</span>
        </div>
        <div class="project-links">
          <a href="#" class="proj-link">↗ GitHub</a>
          <a href="#" class="proj-link">↗ Live Demo</a>
        </div>
      </div>

      <div class="project-card tilt reveal">
        <div class="project-header">
          <span class="project-icon">🌾</span>
          <span class="project-tag tag-live">● Live</span>
        </div>
        <div class="project-title">FARM2CONSUMER</div>
        <p class="project-desc">Smart AgriTech platform bridging farmers directly to consumers — cutting middlemen, boosting farmer income, and enabling real-time inventory sync across India.</p>
        <div class="project-stack">
          <span class="stack-pill">Python</span>
          <span class="stack-pill">Firebase</span>
          <span class="stack-pill">React</span>
          <span class="stack-pill">Node.js</span>
          <span class="stack-pill">Maps API</span>
        </div>
        <div class="project-links">
          <a href="#" class="proj-link">↗ GitHub</a>
          <a href="#" class="proj-link">↗ Live Demo</a>
        </div>
      </div>

    </div>
  </div>
</div>

<div class="divider"></div>

<!-- ═══ ACHIEVEMENTS ═══ -->
<div class="achievements-section">
  <div class="achievements-inner">
    <div class="section-label reveal">05 / Recognition</div>
    <h2 class="section-title reveal">Achievements & <span>Awards</span></h2>

    <div class="achievements-grid">
      <div class="achievement-card reveal">
        <span class="achievement-icon">🚀</span>
        <div class="achievement-value">Top 100</div>
        <div class="achievement-title">RBIH Co-Incubation</div>
        <div class="achievement-desc">Reserve Bank of India Innovation Hub — top 100 entrepreneur nationally</div>
      </div>
      <div class="achievement-card reveal">
        <span class="achievement-icon">💰</span>
        <div class="achievement-value">₹75,000</div>
        <div class="achievement-title">Codeathon Runner-Up</div>
        <div class="achievement-desc">Competitive coding & product hackathon — second place nationally</div>
      </div>
      <div class="achievement-card reveal">
        <span class="achievement-icon">🔗</span>
        <div class="achievement-value">$500</div>
        <div class="achievement-title">Algorand Blockchain</div>
        <div class="achievement-desc">Web3 innovation and smart contract development winner</div>
      </div>
      <div class="achievement-card reveal">
        <span class="achievement-icon">🏏</span>
        <div class="achievement-value">Rep</div>
        <div class="achievement-title">College Cricket Team</div>
        <div class="achievement-desc">University cricket representative — strategy, discipline, teamwork</div>
      </div>
    </div>
  </div>
</div>

<div class="divider"></div>

<!-- ═══ EXPERIENCE ═══ -->
<div class="exp-section">
  <div class="exp-inner">
    <div class="section-label reveal">06 / Experience</div>
    <h2 class="section-title reveal">Where I've <span>worked</span></h2>

    <div class="exp-card reveal">
      <div class="exp-logo">SM</div>
      <div class="exp-info">
        <h3>Web Development Intern</h3>
        <h4>SuprMentr Technologies Pvt. Ltd.</h4>
        <div class="exp-meta">2024 · Bangalore, India · Full-time Internship</div>
        <p class="exp-desc">Built and deployed production-grade web features using React.js and Node.js. Contributed to real client-facing products, shipping features end-to-end under senior engineering mentorship in a startup environment.</p>
        <div class="exp-tags">
          <span class="exp-tag">React.js</span>
          <span class="exp-tag">Node.js</span>
          <span class="exp-tag">REST APIs</span>
          <span class="exp-tag">Git</span>
          <span class="exp-tag">Agile</span>
        </div>
      </div>
    </div>
  </div>
</div>

<div class="divider"></div>

<!-- ═══ QUOTE ═══ -->
<div class="quote-section">
  <span class="quote-mark">"</span>
  <p class="quote-text reveal">The best AI systems aren't just technically sound — they solve real problems for real people. Build with empathy. Ship with precision. Scale with purpose.</p>
  <div class="quote-author reveal">— M Anantha Krishna Rishi</div>
</div>

<div class="divider"></div>

<!-- ═══ CONTACT ═══ -->
<div class="contact-section">
  <div class="contact-inner">
    <div class="section-label reveal">07 / Contact</div>
    <h2 class="section-title reveal">Let's <span>connect</span></h2>
    <p style="color:rgba(255,255,255,0.5); margin-top:1rem; line-height:1.7;" class="reveal">Open to internships, research collaborations, startup ventures, and high-impact engineering roles. Response within 24 hours.</p>

    <div class="contact-grid">
      <a href="https://linkedin.com/in/RISHIMAJETI" target="_blank" class="contact-card reveal">
        <span class="contact-icon">💼</span>
        <span class="contact-name">LinkedIn</span>
        <span class="contact-handle">in/RISHIMAJETI</span>
      </a>
      <a href="https://github.com/RISHIMAJETI" target="_blank" class="contact-card reveal">
        <span class="contact-icon">🐙</span>
        <span class="contact-name">GitHub</span>
        <span class="contact-handle">@RISHIMAJETI</span>
      </a>
      <a href="mailto:ananthakrishnarishi@gmail.com" class="contact-card reveal">
        <span class="contact-icon">📧</span>
        <span class="contact-name">Email</span>
        <span class="contact-handle">Gmail</span>
      </a>
      <a href="https://RISHIMAJETI.vercel.app" target="_blank" class="contact-card reveal">
        <span class="contact-icon">🌐</span>
        <span class="contact-name">Portfolio</span>
        <span class="contact-handle">vercel.app</span>
      </a>
    </div>
  </div>
</div>

<footer>
  <p>Crafted with intention · <span>RISHIMAJETI</span> · Powered by curiosity · Built to last</p>
</footer>

</div><!-- /content -->

<script>
/* ── PARTICLE CANVAS ── */
const canvas = document.getElementById('bg-canvas');
const ctx = canvas.getContext('2d');
let W, H, particles = [];

function resize() {
  W = canvas.width = window.innerWidth;
  H = canvas.height = window.innerHeight;
}

class Particle {
  constructor() { this.reset(); }
  reset() {
    this.x = Math.random() * W;
    this.y = Math.random() * H;
    this.size = Math.random() * 1.5 + 0.3;
    this.vx = (Math.random() - 0.5) * 0.3;
    this.vy = (Math.random() - 0.5) * 0.3;
    this.alpha = Math.random() * 0.5 + 0.1;
    this.color = Math.random() > 0.6 ? '#00f5ff' : '#7b2fff';
  }
  update() {
    this.x += this.vx; this.y += this.vy;
    if (this.x < 0 || this.x > W || this.y < 0 || this.y > H) this.reset();
  }
  draw() {
    ctx.beginPath();
    ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
    ctx.fillStyle = this.color;
    ctx.globalAlpha = this.alpha;
    ctx.fill();
  }
}

function initParticles() {
  particles = [];
  for (let i = 0; i < 120; i++) particles.push(new Particle());
}

function drawConnections() {
  for (let i = 0; i < particles.length; i++) {
    for (let j = i + 1; j < particles.length; j++) {
      const dx = particles[i].x - particles[j].x;
      const dy = particles[i].y - particles[j].y;
      const dist = Math.sqrt(dx*dx + dy*dy);
      if (dist < 100) {
        ctx.beginPath();
        ctx.moveTo(particles[i].x, particles[i].y);
        ctx.lineTo(particles[j].x, particles[j].y);
        ctx.strokeStyle = '#00f5ff';
        ctx.globalAlpha = (1 - dist/100) * 0.08;
        ctx.lineWidth = 0.5;
        ctx.stroke();
      }
    }
  }
}

function animate() {
  ctx.clearRect(0, 0, W, H);
  particles.forEach(p => { p.update(); p.draw(); });
  drawConnections();
  ctx.globalAlpha = 1;
  requestAnimationFrame(animate);
}

resize();
initParticles();
animate();
window.addEventListener('resize', () => { resize(); initParticles(); });

/* ── TYPING EFFECT ── */
const phrases = [
  'Data Scientist | AI Engineer',
  'Full Stack Developer',
  'ML · Deep Learning · LLMs',
  'RBIH Top 100 Entrepreneur 🚀',
  'Building Intelligent Products',
];
let pi = 0, ci = 0, deleting = false;
const el = document.getElementById('typing');

function type() {
  const phrase = phrases[pi];
  el.textContent = deleting ? phrase.slice(0, ci--) : phrase.slice(0, ci++);
  if (!deleting && ci > phrase.length) { setTimeout(() => { deleting = true; }, 1800); }
  if (deleting && ci < 0) { deleting = false; pi = (pi + 1) % phrases.length; ci = 0; }
  setTimeout(type, deleting ? 40 : 75);
}
type();

/* ── SCROLL REVEAL ── */
const observer = new IntersectionObserver((entries) => {
  entries.forEach(e => { if (e.isIntersecting) { e.target.classList.add('visible'); } });
}, { threshold: 0.1 });

document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

/* ── COUNTER ANIMATION ── */
function animateCounter(el) {
  const target = parseInt(el.dataset.target);
  const prefix = el.dataset.prefix || '';
  const suffix = el.dataset.suffix || '';
  const duration = 1500;
  const step = target / (duration / 16);
  let current = 0;
  const timer = setInterval(() => {
    current = Math.min(current + step, target);
    el.textContent = prefix + Math.floor(current) + suffix;
    if (current >= target) clearInterval(timer);
  }, 16);
}

const counterObserver = new IntersectionObserver((entries) => {
  entries.forEach(e => {
    if (e.isIntersecting && e.target.dataset.target) {
      animateCounter(e.target);
      counterObserver.unobserve(e.target);
    }
  });
}, { threshold: 0.5 });

document.querySelectorAll('[data-target]').forEach(el => counterObserver.observe(el));

/* ── 3D TILT ON PROJECT CARDS ── */
document.querySelectorAll('.tilt').forEach(card => {
  card.addEventListener('mousemove', e => {
    const rect = card.getBoundingClientRect();
    const cx = rect.left + rect.width / 2;
    const cy = rect.top + rect.height / 2;
    const rx = ((e.clientY - cy) / rect.height) * -10;
    const ry = ((e.clientX - cx) / rect.width) * 10;
    card.style.transform = `perspective(800px) rotateX(${rx}deg) rotateY(${ry}deg) translateY(-10px)`;
  });
  card.addEventListener('mouseleave', () => {
    card.style.transform = '';
  });
});
</script>
</body>
</html>

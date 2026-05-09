<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FlowState — Investor Pitch Deck</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Bodoni+Moda:ital,opsz,wght@0,6..96,400..900;1,6..96,400..900&family=Outfit:wght@300;400;500;600&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0e17;
    --bg-elevated: #111827;
    --text: #f5f0e8;
    --text-muted: #8b95a5;
    --accent: #d4a373;
    --accent-soft: rgba(212, 163, 115, 0.12);
    --accent-glow: rgba(212, 163, 115, 0.25);
    --secondary: #5e7a9e;
    --gold: #c9b037;
    --border: rgba(245, 240, 232, 0.08);
    --surface: rgba(245, 240, 232, 0.03);
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  html, body {
    width: 100%; height: 100%;
    overflow: hidden;
    font-family: 'Outfit', sans-serif;
    background: var(--bg);
    color: var(--text);
    -webkit-font-smoothing: antialiased;
  }

  /* Noise texture overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.03'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 9999;
    opacity: 0.6;
  }

  /* Slides container */
  .slides-container {
    width: 100%; height: 100%;
    position: relative;
  }

  .slide {
    position: absolute;
    inset: 0;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 6vh 8vw;
    opacity: 0;
    pointer-events: none;
    transform: translateY(30px);
    transition: opacity 0.7s cubic-bezier(0.4, 0, 0.2, 1), transform 0.7s cubic-bezier(0.4, 0, 0.2, 1);
    overflow-y: auto;
  }

  .slide.active {
    opacity: 1;
    pointer-events: all;
    transform: translateY(0);
  }

  .slide.left { transform: translateX(-60px); }
  .slide.right { transform: translateX(60px); }

  /* Typography */
  h1, h2, h3 {
    font-family: 'Bodoni Moda', serif;
    font-weight: 500;
    line-height: 1.05;
    letter-spacing: -0.02em;
  }

  h1 { font-size: clamp(2.2rem, 5vw, 4.5rem); }
  h2 { font-size: clamp(1.6rem, 3.5vw, 3rem); }
  h3 { font-size: clamp(1.1rem, 2vw, 1.5rem); font-weight: 600; }

  p, li {
    font-size: clamp(0.95rem, 1.3vw, 1.15rem);
    line-height: 1.7;
    color: var(--text-muted);
    font-weight: 300;
  }

  .mono {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.9em;
    letter-spacing: -0.01em;
  }

  .accent { color: var(--accent); }
  .gold { color: var(--gold); }
  .muted { color: var(--text-muted); }

  /* Layout helpers */
  .grid-2 {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 4vw;
    align-items: start;
    width: 100%;
    max-width: 1400px;
    margin: 0 auto;
  }

  .grid-3 {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 3vw;
    width: 100%;
    max-width: 1400px;
    margin: 0 auto;
  }

  .grid-4 {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 2.5vw;
    width: 100%;
    max-width: 1400px;
    margin: 0 auto;
  }

  .label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.75rem;
    text-transform: uppercase;
    letter-spacing: 0.12em;
    color: var(--accent);
    margin-bottom: 1.5rem;
    display: block;
  }

  .divider {
    width: 60px;
    height: 1px;
    background: var(--accent);
    margin: 2rem 0;
  }

  /* Cards */
  .card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 2px;
    padding: 2rem;
    transition: border-color 0.3s, background 0.3s;
  }

  .card:hover {
    border-color: var(--accent);
    background: var(--accent-soft);
  }

  .stat-card {
    text-align: center;
  }

  .stat-card .number {
    font-family: 'Bodoni Moda', serif;
    font-size: clamp(2rem, 4vw, 3.5rem);
    color: var(--accent);
    line-height: 1;
    margin-bottom: 0.5rem;
  }

  .stat-card .label {
    margin-bottom: 0;
    color: var(--text-muted);
  }

  /* Tables */
  table {
    width: 100%;
    border-collapse: collapse;
    font-size: 0.95rem;
    max-width: 900px;
  }

  th {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.7rem;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    color: var(--accent);
    text-align: left;
    padding: 1rem 1.2rem;
    border-bottom: 1px solid var(--border);
    font-weight: 500;
  }

  td {
    padding: 1rem 1.2rem;
    border-bottom: 1px solid var(--border);
    color: var(--text-muted);
    font-weight: 300;
  }

  tr:hover td { color: var(--text); }

  /* Progress bar */
  .progress-bar {
    position: fixed;
    bottom: 0; left: 0;
    height: 2px;
    background: var(--accent);
    transition: width 0.5s cubic-bezier(0.4, 0, 0.2, 1);
    z-index: 100;
  }

  .slide-counter {
    position: fixed;
    bottom: 1.5rem;
    right: 2rem;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.75rem;
    color: var(--text-muted);
    z-index: 100;
    letter-spacing: 0.05em;
  }

  /* Navigation */
  .nav-hint {
    position: fixed;
    bottom: 1.5rem;
    left: 2rem;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.65rem;
    color: var(--text-muted);
    opacity: 0.5;
    z-index: 100;
    letter-spacing: 0.05em;
  }

  /* Market size circles */
  .market-circles {
    position: relative;
    width: 320px;
    height: 320px;
    margin: 0 auto;
  }

  .circle {
    position: absolute;
    border-radius: 50%;
    border: 1px solid var(--border);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
    transition: border-color 0.3s, transform 0.3s;
  }

  .circle:hover { border-color: var(--accent); transform: scale(1.02); }

  .circle.tam { width: 320px; height: 320px; top: 0; left: 0; }
  .circle.sam { width: 220px; height: 220px; top: 50px; left: 50px; background: var(--bg-elevated); }
  .circle.som { width: 130px; height: 130px; top: 95px; left: 95px; background: var(--accent-soft); border-color: var(--accent); }

  .circle .c-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.65rem;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    color: var(--text-muted);
    margin-bottom: 0.3rem;
  }

  .circle .c-value {
    font-family: 'Bodoni Moda', serif;
    font-size: 1.4rem;
    color: var(--text);
  }

  .circle.som .c-value { color: var(--accent); font-size: 1.8rem; }

  /* Matrix */
  .matrix {
    display: grid;
    grid-template-columns: auto 1fr 1fr;
    grid-template-rows: auto 1fr 1fr;
    gap: 1px;
    background: var(--border);
    border: 1px solid var(--border);
    max-width: 600px;
  }

  .matrix > div {
    background: var(--bg);
    padding: 1.2rem 1.5rem;
    font-size: 0.85rem;
  }

  .matrix .axis-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.6rem;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    color: var(--text-muted);
  }

  .matrix .cell { color: var(--text-muted); font-weight: 300; }
  .matrix .cell.highlight {
    background: var(--accent-soft);
    color: var(--accent);
    font-weight: 500;
    border: 1px solid var(--accent);
  }

  /* Ask layout */
  .ask-amount {
    font-family: 'Bodoni Moda', serif;
    font-size: clamp(3rem, 7vw, 6rem);
    color: var(--accent);
    line-height: 1;
  }

  /* Contact */
  .contact-link {
    font-family: 'JetBrains Mono', monospace;
    font-size: 1rem;
    color: var(--accent);
    text-decoration: none;
    border-bottom: 1px solid transparent;
    transition: border-color 0.3s;
  }

  .contact-link:hover { border-bottom-color: var(--accent); }

  /* Animations */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .animate-in > * {
    opacity: 0;
    animation: fadeUp 0.6s cubic-bezier(0.4, 0, 0.2, 1) forwards;
  }

  .active .animate-in > *:nth-child(1) { animation-delay: 0.1s; }
  .active .animate-in > *:nth-child(2) { animation-delay: 0.2s; }
  .active .animate-in > *:nth-child(3) { animation-delay: 0.3s; }
  .active .animate-in > *:nth-child(4) { animation-delay: 0.4s; }
  .active .animate-in > *:nth-child(5) { animation-delay: 0.5s; }
  .active .animate-in > *:nth-child(6) { animation-delay: 0.6s; }
  .active .animate-in > *:nth-child(7) { animation-delay: 0.7s; }
  .active .animate-in > *:nth-child(8) { animation-delay: 0.8s; }

  /* Responsive */
  @media (max-width: 900px) {
    .grid-2, .grid-3, .grid-4 { grid-template-columns: 1fr; }
    .slide { padding: 4vh 6vw; }
    .market-circles { transform: scale(0.8); }
    .matrix { max-width: 100%; }
  }

  @media (max-width: 600px) {
    .market-circles { transform: scale(0.6); }
    .nav-hint { display: none; }
  }

  /* Scrollbar */
  ::-webkit-scrollbar { width: 4px; }
  ::-webkit-scrollbar-track { background: transparent; }
  ::-webkit-scrollbar-thumb { background: var(--border); border-radius: 2px; }
  ::-webkit-scrollbar-thumb:hover { background: var(--accent); }
</style>
</head>
<body>

<div class="progress-bar" id="progressBar"></div>
<div class="slide-counter" id="slideCounter">01 / 15</div>
<div class="nav-hint">Use arrow keys or click to navigate</div>

<div class="slides-container">

<!-- Slide 1: Title -->
<div class="slide active">
  <div style="max-width: 1000px; margin: 0 auto;" class="animate-in">
    <span class="label">Seed Round — $2.5M</span>
    <h1 style="margin-bottom: 1.5rem;">Close Books <span class="accent">4× Faster</span> Without Hiring More Accountants</h1>
    <p style="font-size: 1.1rem; color: var(--text-muted); max-width: 600px; margin-bottom: 3rem;">AI workflow automation built for finance teams at 50–500 employee companies</p>
    <div style="display: flex; gap: 3rem; flex-wrap: wrap;">
      <div>
        <span class="mono" style="font-size: 1.6rem; color: var(--accent);">47</span>
        <p style="font-size: 0.8rem; margin-top: 0.3rem;">Customers</p>
      </div>
      <div>
        <span class="mono" style="font-size: 1.6rem; color: var(--accent);">$420K</span>
        <p style="font-size: 0.8rem; margin-top: 0.3rem;">ARR</p>
      </div>
      <div>
        <span class="mono" style="font-size: 1.6rem; color: var(--accent);">142%</span>
        <p style="font-size: 0.8rem; margin-top: 0.3rem;">YoY Growth</p>
      </div>
    </div>
    <div class="divider"></div>
    <p class="mono" style="font-size: 0.75rem; color: var(--text-muted);">FlowState — Confidential</p>
  </div>
</div>

<!-- Slide 2: Problem -->
<div class="slide">
  <div style="max-width: 1000px; margin: 0 auto;" class="animate-in">
    <span class="label">The Problem</span>
    <h2 style="margin-bottom: 2rem; max-width: 700px;">Finance teams spend <span class="accent">60%</span> of their time on manual reconciliation instead of analysis</h2>
    <div class="grid-2">
      <div>
        <div class="card" style="margin-bottom: 1.5rem;">
          <span class="mono" style="font-size: 2rem; color: var(--accent);">8–12</span>
          <p style="margin-top: 0.5rem;">Days for month-end close at mid-market companies</p>
        </div>
        <div class="card">
          <span class="mono" style="font-size: 2rem; color: var(--accent);">73%</span>
          <p style="margin-top: 0.5rem;">Of finance leaders cannot hire qualified accountants fast enough</p>
        </div>
      </div>
      <div>
        <ul style="list-style: none;">
          <li style="margin-bottom: 1.2rem; padding-left: 1.5rem; position: relative;">
            <span style="position: absolute; left: 0; color: var(--accent);">—</span>
            Month-end close takes 8–12 days for mid-market companies
          </li>
          <li style="margin-bottom: 1.2rem; padding-left: 1.5rem; position: relative;">
            <span style="position: absolute; left: 0; color: var(--accent);">—</span>
            Existing ERP add-ons are built for enterprises and require 6-month implementations
          </li>
          <li style="padding-left: 1.5rem; position: relative;">
            <span style="position: absolute; left: 0; color: var(--accent);">—</span>
            Teams hire expensive consultants or burn out their staff
          </li>
        </ul>
      </div>
    </div>
  </div>
</div>

<!-- Slide 3: Solution -->
<div class="slide">
  <div style="max-width: 1000px; margin: 0 auto;" class="animate-in">
    <span class="label">The Solution</span>
    <h2 style="margin-bottom: 2rem; max-width: 750px;">FlowState auto-reconciles transactions and flags anomalies <span class="accent">before they become errors</span></h2>
    <div class="grid-2">
      <div>
        <div class="card" style="border-color: var(--accent); background: var(--accent-soft);">
          <p style="color: var(--text); font-weight: 400;"><span class="accent">10 minutes</span> to connect QuickBooks, NetSuite, and Stripe</p>
        </div>
        <div class="card" style="margin-top: 1rem;">
          <p><span class="accent">99.3%</span> AI matching accuracy across sources</p>
        </div>
        <div class="card" style="margin-top: 1rem;">
          <p>Flags outliers and suggests corrections, learning from each user's feedback</p>
        </div>
      </div>
      <div style="display: flex; align-items: center; justify-content: center;">
        <div style="text-align: center;">
          <span class="mono" style="font-size: 5rem; color: var(--accent); line-height: 1;">8–12</span>
          <p style="margin: 0.5rem 0;">days</p>
          <div style="width: 1px; height: 40px; background: var(--border); margin: 1rem auto;"></div>
          <span class="mono" style="font-size: 5rem; color: var(--gold); line-height: 1;">2–3</span>
          <p style="margin: 0.5rem 0;">days with FlowState</p>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- Slide 4: Why Now -->
<div class="slide">
  <div style="max-width: 1100px; margin: 0 auto;" class="animate-in">
    <span class="label">Why Now</span>
    <h2 style="margin-bottom: 3rem;">Three converging forces make this <span class="accent">the moment</span></h2>
    <div class="grid-3">
      <div class="card" style="text-align: center;">
        <span class="mono" style="font-size: 2.5rem; color: var(--accent);">01</span>
        <h3 style="margin: 1rem 0 0.5rem;">Talent Shortage</h3>
        <p>340K accountant gap in the US by 2026. The problem is structural and accelerating.</p>
      </div>
      <div class="card" style="text-align: center;">
        <span class="mono" style="font-size: 2.5rem; color: var(--accent);">02</span>
        <h3 style="margin: 1rem 0 0.5rem;">API Maturity</h3>
        <p>Every major ERP and bank now offers robust, stable APIs. Integration friction is gone.</p>
      </div>
      <div class="card" style="text-align: center;">
        <span class="mono" style="font-size: 2.5rem; color: var(--accent);">03</span>
        <h3 style="margin: 1rem 0 0.5rem;">AI Readiness</h3>
        <p>LLMs now reliably parse unstructured financial data with &gt;99% accuracy.</p>
      </div>
    </div>
  </div>
</div>

<!-- Slide 5: Market Size -->
<div class="slide">
  <div style="max-width: 1100px; margin: 0 auto;" class="animate-in">
    <span class="label">Market Size</span>
    <h2 style="margin-bottom: 3rem;">A <span class="accent">$12B</span> serviceable market with a clear path to $100M+ revenue</h2>
    <div class="grid-2" style="align-items: center;">
      <div style="display: flex; justify-content: center;">
        <div class="market-circles">
          <div class="circle tam">
            <span class="c-label">TAM</span>
            <span class="c-value">$48B</span>
          </div>
          <div class="circle sam">
            <span class="c-label">SAM</span>
            <span class="c-value">$12B</span>
          </div>
          <div class="circle som">
            <span class="c-label">SOM</span>
            <span class="c-value">$420M</span>
          </div>
        </div>
      </div>
      <div>
        <p style="margin-bottom: 1.5rem; color: var(--text);"><strong>TAM</strong> — All SMB/mid-market accounting automation software globally</p>
        <p style="margin-bottom: 1.5rem; color: var(--text);"><strong>SAM</strong> — US-based companies, 50–500 employees, using cloud ERP</p>
        <p style="margin-bottom: 2rem; color: var(--accent);"><strong>SOM</strong> — Companies with 50+ FTE in finance, ACV $15K, reachable via partnerships</p>
        <p class="mono" style="font-size: 0.75rem;">Bottom-up SOM: 28 reps × $600K quota × 25% win rate = $4.2M per rep class. 10 rep classes = $42M Year 5.</p>
      </div>
    </div>
  </div>
</div>

<!-- Slide 6: Business Model -->
<div class="slide">
  <div style="max-width: 1100px; margin: 0 auto;" class="animate-in">
    <span class="label">Business Model</span>
    <h2 style="margin-bottom: 2rem;">Land-and-expand SaaS with <span class="accent">best-in-class</span> unit economics</h2>
    <div class="grid-4" style="margin-bottom: 3rem;">
      <div class="stat-card">
        <div class="number">$15K</div>
        <span class="label">Avg ACV</span>
      </div>
      <div class="stat-card">
        <div class="number">82%</div>
        <span class="label">Gross Margin</span>
      </div>
      <div class="stat-card">
        <div class="number">16:1</div>
        <span class="label">LTV:CAC</span>
      </div>
      <div class="stat-card">
        <div class="number">5mo</div>
        <span class="label">CAC Payback</span>
      </div>
    </div>
    <div class="grid-2" style="max-width: 800px; margin: 0 auto;">
      <div class="card">
        <p style="color: var(--text);"><span class="mono accent">$500</span>/mo base + <span class="mono accent">$25</span> per connected entity</p>
      </div>
      <div class="card">
        <p><span class="accent">118%</span> Net Revenue Retention (expansion via additional entities and modules)</p>
      </div>
    </div>
  </div>
</div>

<!-- Slide 7: Traction -->
<div class="slide">
  <div style="max-width: 1100px; margin: 0 auto;" class="animate-in">
    <span class="label">Traction</span>
    <h2 style="margin-bottom: 2rem;">Revenue grew <span class="accent">4×</span> in 12 months; 95% of customers expand within 6 months</h2>
    <div class="grid-4" style="margin-bottom: 3rem;">
      <div class="stat-card">
        <div class="number">$420K</div>
        <span class="label">ARR</span>
      </div>
      <div class="stat-card">
        <div class="number">47</div>
        <span class="label">Customers</span>
      </div>
      <div class="stat-card">
        <div class="number">100%</div>
        <span class="label">Logo Retention</span>
      </div>
      <div class="stat-card">
        <div class="number">118%</div>
        <span class="label">NRR</span>
      </div>
    </div>
    <p class="mono" style="text-align: center; font-size: 0.85rem;">Key customers: Segment (pilot) · Notion (full deployment) · Figma (expanding) · Sales cycle: 21 days</p>
  </div>
</div>

<!-- Slide 8: Product Demo -->
<div class="slide">
  <div style="max-width: 900px; margin: 0 auto; text-align: center;" class="animate-in">
    <span class="label">Product</span>
    <h2 style="margin-bottom: 2rem;">Watch how FlowState closes a month-end in <span class="accent">90 seconds</span></h2>
    <div style="background: var(--bg-elevated); border: 1px solid var(--border); border-radius: 4px; padding: 5rem 2rem; margin-bottom: 2rem; position: relative; overflow: hidden;">
      <div style="position: absolute; inset: 0; background: linear-gradient(135deg, rgba(212,163,115,0.05) 0%, transparent 50%);"></div>
      <div style="position: relative;">
        <div style="width: 80px; height: 80px; border: 2px solid var(--accent); border-radius: 50%; margin: 0 auto 1.5rem; display: flex; align-items: center; justify-content: center; cursor: pointer; transition: transform 0.3s, box-shadow 0.3s;" onmouseover="this.style.transform='scale(1.1)';this.style.boxShadow='0 0 40px rgba(212,163,115,0.3)'" onmouseout="this.style.transform='scale(1)';this.style.boxShadow='none'">
          <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="var(--accent)" stroke-width="2"><polygon points="5 3 19 12 5 21 5 3"/></svg>
        </div>
        <p style="color: var(--text); font-weight: 400;">Demo Video Placeholder</p>
        <p style="font-size: 0.85rem; margin-top: 0.5rem;">Connect → Reconcile → Review → Close</p>
      </div>
    </div>
    <p class="mono" style="font-size: 0.75rem;">Backup: Pre-recorded video saved locally + uploaded to DocSend</p>
  </div>
</div>

<!-- Slide 9: Competition -->
<div class="slide">
  <div style="max-width: 1000px; margin: 0 auto;" class="animate-in">
    <span class="label">Competition</span>
    <h2 style="margin-bottom: 2rem;">The only AI-native solution that integrates in <span class="accent">minutes</span>, not months</h2>
    <div style="display: flex; justify-content: center; margin-bottom: 3rem;">
      <div class="matrix">
        <div></div>
        <div class="axis-label" style="text-align: center;">Slow Implementation</div>
        <div class="axis-label" style="text-align: center;">Fast Implementation</div>

        <div class="axis-label" style="writing-mode: vertical-rl; transform: rotate(180deg); text-align: center;">High AI Automation</div>
        <div class="cell highlight">FlowState</div>
        <div class="cell"></div>

        <div class="axis-label" style="writing-mode: vertical-rl; transform: rotate(180deg); text-align: center;">Low AI Automation</div>
        <div class="cell">BlackLine, FloQast</div>
        <div class="cell">QuickBooks, Spreadsheets</div>
      </div>
    </div>
    <p class="mono" style="text-align: center; font-size: 0.85rem; max-width: 700px; margin: 0 auto;">Moat: Proprietary transaction-matching AI trained on 40M+ labeled examples. Improves with every customer.</p>
  </div>
</div>

<!-- Slide 10: Go-to-Market -->
<div class="slide">
  <div style="max-width: 1100px; margin: 0 auto;" class="animate-in">
    <span class="label">Go-to-Market</span>
    <h2 style="margin-bottom: 2rem;">Product-led trials convert to paid at <span class="accent">34%</span>; inside sales accelerates expansion</h2>
    <div class="grid-3" style="margin-bottom: 3rem;">
      <div class="card">
        <span class="mono" style="color: var(--accent);">01</span>
        <h3 style="margin: 0.8rem 0 0.5rem;">Product-Led</h3>
        <p>Free 14-day trial via marketplace integrations. 34% trial-to-paid conversion.</p>
      </div>
      <div class="card">
        <span class="mono" style="color: var(--accent);">02</span>
        <h3 style="margin: 0.8rem 0 0.5rem;">Inside Sales</h3>
        <p>2 reps today, adding 2 per quarter. Target: 10 reps by end of 2026.</p>
      </div>
      <div class="card">
        <span class="mono" style="color: var(--accent);">03</span>
        <h3 style="margin: 0.8rem 0 0.5rem;">Partnerships</h3>
        <p>Active with QuickBooks, Stripe, Mercury. NetSuite in final negotiation.</p>
      </div>
    </div>
    <table style="margin: 0 auto;">
      <tr>
        <th>Channel</th>
        <th>CAC</th>
        <th>% of New ARR</th>
      </tr>
      <tr>
        <td>Product-led</td>
        <td class="mono">$1,800</td>
        <td>45%</td>
      </tr>
      <tr>
        <td>Inside sales</td>
        <td class="mono">$7,200</td>
        <td>40%</td>
      </tr>
      <tr>
        <td>Partnerships</td>
        <td class="mono">$900</td>
        <td>15%</td>
      </tr>
    </table>
  </div>
</div>

<!-- Slide 11: Team -->
<div class="slide">
  <div style="max-width: 1100px; margin: 0 auto;" class="animate-in">
    <span class="label">Team</span>
    <h2 style="margin-bottom: 3rem;">Built by finance operators who have <span class="accent">done this before</span></h2>
    <div class="grid-4">
      <div class="card" style="text-align: center;">
        <div style="width: 60px; height: 60px; border-radius: 50%; background: var(--accent-soft); border: 1px solid var(--accent); margin: 0 auto 1rem; display: flex; align-items: center; justify-content: center; font-family: 'Bodoni Moda', serif; font-size: 1.5rem; color: var(--accent);">S</div>
        <h3 style="font-size: 1.1rem;">Sarah Chen</h3>
        <p class="mono" style="font-size: 0.7rem; color: var(--accent); margin-bottom: 0.8rem;">CEO</p>
        <p style="font-size: 0.85rem;">Former VP Finance at Stripe. Led 40-person team. Closed 200+ month-ends.</p>
      </div>
      <div class="card" style="text-align: center;">
        <div style="width: 60px; height: 60px; border-radius: 50%; background: var(--accent-soft); border: 1px solid var(--accent); margin: 0 auto 1rem; display: flex; align-items: center; justify-content: center; font-family: 'Bodoni Moda', serif; font-size: 1.5rem; color: var(--accent);">D</div>
        <h3 style="font-size: 1.1rem;">David Park</h3>
        <p class="mono" style="font-size: 0.7rem; color: var(--accent); margin-bottom: 0.8rem;">CTO</p>
        <p style="font-size: 0.85rem;">Former Staff Engineer at Plaid. Built banking pipelines processing $2B/day.</p>
      </div>
      <div class="card" style="text-align: center;">
        <div style="width: 60px; height: 60px; border-radius: 50%; background: var(--accent-soft); border: 1px solid var(--accent); margin: 0 auto 1rem; display: flex; align-items: center; justify-content: center; font-family: 'Bodoni Moda', serif; font-size: 1.5rem; color: var(--accent);">A</div>
        <h3 style="font-size: 1.1rem;">Aisha Johnson</h3>
        <p class="mono" style="font-size: 0.7rem; color: var(--accent); margin-bottom: 0.8rem;">Head of AI</p>
        <p style="font-size: 0.85rem;">PhD ML, Stanford. 8 years at Google Research. 12 papers on anomaly detection.</p>
      </div>
      <div class="card" style="text-align: center;">
        <div style="width: 60px; height: 60px; border-radius: 50%; background: var(--accent-soft); border: 1px solid var(--accent); margin: 0 auto 1rem; display: flex; align-items: center; justify-content: center; font-family: 'Bodoni Moda', serif; font-size: 1.5rem; color: var(--accent);">M</div>
        <h3 style="font-size: 1.1rem;">Marcus Reyes</h3>
        <p class="mono" style="font-size: 0.7rem; color: var(--accent); margin-bottom: 0.8rem;">Head of Sales</p>
        <p style="font-size: 0.85rem;">Former AE at FloQast. Closed $15M in ARR. Deep network in finance leadership.</p>
      </div>
    </div>
    <p class="mono" style="text-align: center; margin-top: 2rem; font-size: 0.85rem; color: var(--accent);">Collective prior exits: 3 (2 acquisitions, 1 IPO)</p>
  </div>
</div>

<!-- Slide 12: Financial Projections -->
<div class="slide">
  <div style="max-width: 1000px; margin: 0 auto;" class="animate-in">
    <span class="label">Financial Projections</span>
    <h2 style="margin-bottom: 2rem;">Path to <span class="accent">$10M ARR</span> in 36 months with disciplined capital efficiency</h2>
    <table style="margin: 0 auto 2rem;">
      <tr>
        <th>Metric</th>
        <th>2024 Actual</th>
        <th>2025 Actual</th>
        <th>2026 Proj</th>
        <th>2027 Proj</th>
      </tr>
      <tr>
        <td>ARR</td>
        <td class="mono">$105K</td>
        <td class="mono">$420K</td>
        <td class="mono accent">$1.8M</td>
        <td class="mono">$5.2M</td>
      </tr>
      <tr>
        <td>Customers</td>
        <td class="mono">12</td>
        <td class="mono">47</td>
        <td class="mono accent">180</td>
        <td class="mono">450</td>
      </tr>
      <tr>
        <td>Burn Multiple</td>
        <td class="mono">—</td>
        <td class="mono">2.1x</td>
        <td class="mono accent">1.4x</td>
        <td class="mono">1.1x</td>
      </tr>
      <tr>
        <td>Headcount</td>
        <td class="mono">4</td>
        <td class="mono">8</td>
        <td class="mono accent">18</td>
        <td class="mono">32</td>
      </tr>
    </table>
    <p class="mono" style="text-align: center; font-size: 0.75rem;">Key assumptions: ACV grows from $15K to $18K via expansion modules · Sales rep quota: $600K ARR, ramping over 6 months · CAC improves 15% YoY</p>
  </div>
</div>

<!-- Slide 13: The Ask -->
<div class="slide">
  <div style="max-width: 900px; margin: 0 auto;" class="animate-in">
    <span class="label">The Ask</span>
    <h2 style="margin-bottom: 2rem;">Raising <span class="ask-amount">$2.5M</span> to reach $1.8M ARR and 180 customers by December 2026</h2>
    <div class="grid-2" style="margin-bottom: 3rem;">
      <div>
        <h3 style="margin-bottom: 1rem;">Use of Funds</h3>
        <div style="margin-bottom: 1rem;">
          <div style="display: flex; justify-content: space-between; margin-bottom: 0.5rem;">
            <span>Product & Engineering</span>
            <span class="mono accent">45%</span>
          </div>
          <div style="height: 4px; background: var(--border); border-radius: 2px;"><div style="width: 45%; height: 100%; background: var(--accent); border-radius: 2px;"></div></div>
        </div>
        <div style="margin-bottom: 1rem;">
          <div style="display: flex; justify-content: space-between; margin-bottom: 0.5rem;">
            <span>Sales & Marketing</span>
            <span class="mono accent">30%</span>
          </div>
          <div style="height: 4px; background: var(--border); border-radius: 2px;"><div style="width: 30%; height: 100%; background: var(--secondary); border-radius: 2px;"></div></div>
        </div>
        <div style="margin-bottom: 1rem;">
          <div style="display: flex; justify-content: space-between; margin-bottom: 0.5rem;">
            <span>Operations & Support</span>
            <span class="mono accent">15%</span>
          </div>
          <div style="height: 4px; background: var(--border); border-radius: 2px;"><div style="width: 15%; height: 100%; background: var(--gold); border-radius: 2px;"></div></div>
        </div>
        <div>
          <div style="display: flex; justify-content: space-between; margin-bottom: 0.5rem;">
            <span>Reserve</span>
            <span class="mono accent">10%</span>
          </div>
          <div style="height: 4px; background: var(--border); border-radius: 2px;"><div style="width: 10%; height: 100%; background: var(--text-muted); border-radius: 2px;"></div></div>
        </div>
      </div>
      <div>
        <h3 style="margin-bottom: 1rem;">Milestones for Series A</h3>
        <ul style="list-style: none;">
          <li style="margin-bottom: 0.8rem; padding-left: 1.5rem; position: relative;"><span style="position: absolute; left: 0; color: var(--accent);">✓</span> $1.8M ARR</li>
          <li style="margin-bottom: 0.8rem; padding-left: 1.5rem; position: relative;"><span style="position: absolute; left: 0; color: var(--accent);">✓</span> 180 customers</li>
          <li style="margin-bottom: 0.8rem; padding-left: 1.5rem; position: relative;"><span style="position: absolute; left: 0; color: var(--accent);">✓</span> 2 non-founder reps closing independently</li>
          <li style="margin-bottom: 0.8rem; padding-left: 1.5rem; position: relative;"><span style="position: absolute; left: 0; color: var(--accent);">✓</span> NetSuite partnership live</li>
          <li style="padding-left: 1.5rem; position: relative;"><span style="position: absolute; left: 0; color: var(--accent);">✓</span> Burn multiple below 1.5x</li>
        </ul>
      </div>
    </div>
    <p class="mono" style="text-align: center; font-size: 0.85rem; color: var(--text-muted);">$12M post-money SAFE</p>
  </div>
</div>

<!-- Slide 14: Vision -->
<div class="slide">
  <div style="max-width: 900px; margin: 0 auto; text-align: center;" class="animate-in">
    <span class="label">Vision</span>
    <h1 style="margin-bottom: 3rem; font-size: clamp(2rem, 4vw, 3.5rem);">Every finance team deserves an AI colleague, <span class="accent">not another spreadsheet</span></h1>
    <div style="display: flex; justify-content: center; gap: 4rem; flex-wrap: wrap;">
      <div style="text-align: center;">
        <span class="mono" style="font-size: 0.75rem; color: var(--accent);">TODAY</span>
        <p style="margin-top: 0.5rem; color: var(--text);">Month-end reconciliation</p>
      </div>
      <div style="width: 1px; background: var(--border);"></div>
      <div style="text-align: center;">
        <span class="mono" style="font-size: 0.75rem; color: var(--accent);">NEXT YEAR</span>
        <p style="margin-top: 0.5rem; color: var(--text);">Full close automation, variance analysis, forecasting</p>
      </div>
      <div style="width: 1px; background: var(--border);"></div>
      <div style="text-align: center;">
        <span class="mono" style="font-size: 0.75rem; color: var(--accent);">5 YEARS</span>
        <p style="margin-top: 0.5rem; color: var(--text);">The autonomous finance function</p>
      </div>
    </div>
  </div>
</div>

<!-- Slide 15: Closing -->
<div class="slide">
  <div style="max-width: 700px; margin: 0 auto; text-align: center;" class="animate-in">
    <span class="label">Thank You</span>
    <h1 style="margin-bottom: 2rem;">Let's help finance teams <span class="accent">close faster</span></h1>
    <a href="mailto:sarah@flowstate.ai" class="contact-link">sarah@flowstate.ai</a>
    <p class="mono" style="margin-top: 1.5rem; font-size: 0.85rem; color: var(--text-muted);">+1-415-555-0199</p>
    <div class="divider" style="margin: 2rem auto;"></div>
    <p style="font-size: 0.85rem; color: var(--text-muted);">Appendices available: Detailed financial model · Cap table · Competitive deep-dive · Technical architecture</p>
    <p class="mono" style="margin-top: 1.5rem; font-size: 0.75rem; color: var(--accent);">Next step: Product demo for partners and associates</p>
  </div>
</div>

</div>

<script>
  const slides = document.querySelectorAll('.slide');
  let current = 0;
  const progressBar = document.getElementById('progressBar');
  const counter = document.getElementById('slideCounter');

  function updateSlide() {
    slides.forEach((s, i) => {
      s.classList.toggle('active', i === current);
    });
    progressBar.style.width = ((current + 1) / slides.length * 100) + '%';
    counter.textContent = String(current + 1).padStart(2, '0') + ' / ' + String(slides.length).padStart(2, '0');
  }

  function next() {
    if (current < slides.length - 1) { current++; updateSlide(); }
  }

  function prev() {
    if (current > 0) { current--; updateSlide(); }
  }

  document.addEventListener('keydown', (e) => {
    if (e.key === 'ArrowRight' || e.key === ' ' || e.key === 'ArrowDown') {
      e.preventDefault(); next();
    } else if (e.key === 'ArrowLeft' || e.key === 'ArrowUp') {
      e.preventDefault(); prev();
    }
  });

  document.addEventListener('click', (e) => {
    const x = e.clientX / window.innerWidth;
    if (x > 0.6) next();
    else if (x < 0.4) prev();
  });

  // Touch support
  let touchStartX = 0;
  document.addEventListener('touchstart', (e) => { touchStartX = e.changedTouches[0].screenX; });
  document.addEventListener('touchend', (e) => {
    const diff = touchStartX - e.changedTouches[0].screenX;
    if (Math.abs(diff) > 50) diff > 0 ? next() : prev();
  });

  updateSlide();
</script>

</body>
</html>

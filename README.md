<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Smart Wardrobe AI</title>
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet"/>
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --sky: #C8E6F7;
    --sky-mid: #6BB8E8;
    --sky-deep: #1A6FA8;
    --night: #0D1B2A;
    --night-soft: #162436;
    --sand: #F5EFE6;
    --sand-dark: #D4C4A8;
    --warm: #E8956A;
    --warm-deep: #C96B3A;
    --leaf: #4A8C5C;
    --snow: #FAFCFF;
    --muted: #6B7C8D;
    --text: #1A2733;
  }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--snow);
    color: var(--text);
    overflow-x: hidden;
  }

  /* HERO */
  .hero {
    min-height: 100vh;
    background: var(--night);
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 3rem 2rem 5rem;
    overflow: hidden;
  }

  .hero-bg {
    position: absolute;
    inset: 0;
    background: radial-gradient(ellipse 80% 60% at 50% 0%, #1A3A5C 0%, var(--night) 70%);
  }

  /* Animated sky orbs */
  .orb {
    position: absolute;
    border-radius: 50%;
    filter: blur(60px);
    opacity: 0.25;
    animation: float 8s ease-in-out infinite;
  }
  .orb1 { width: 400px; height: 400px; background: var(--sky-mid); top: -100px; left: -100px; animation-delay: 0s; }
  .orb2 { width: 300px; height: 300px; background: var(--warm); top: 50%; right: -80px; animation-delay: -3s; }
  .orb3 { width: 250px; height: 250px; background: #6B8CDA; bottom: 0; left: 30%; animation-delay: -5s; }

  @keyframes float {
    0%, 100% { transform: translateY(0px) scale(1); }
    50% { transform: translateY(-30px) scale(1.05); }
  }

  /* Season chips */
  .season-bar {
    display: flex;
    gap: 10px;
    margin-bottom: 2.5rem;
    position: relative;
    z-index: 1;
    flex-wrap: wrap;
    justify-content: center;
  }

  .chip {
    font-size: 13px;
    font-weight: 500;
    padding: 6px 16px;
    border-radius: 999px;
    letter-spacing: 0.04em;
    opacity: 0;
    animation: slideUp 0.6s ease forwards;
  }
  .chip:nth-child(1) { background: rgba(255,255,255,0.08); color: #A8D4F0; border: 1px solid rgba(168,212,240,0.3); animation-delay: 0.1s; }
  .chip:nth-child(2) { background: rgba(255,255,255,0.08); color: #A8D4A8; border: 1px solid rgba(168,212,168,0.3); animation-delay: 0.2s; }
  .chip:nth-child(3) { background: rgba(255,255,255,0.08); color: #F5C892; border: 1px solid rgba(245,200,146,0.3); animation-delay: 0.3s; }
  .chip:nth-child(4) { background: rgba(255,255,255,0.08); color: #E8956A; border: 1px solid rgba(232,149,106,0.3); animation-delay: 0.4s; }

  @keyframes slideUp {
    from { opacity: 0; transform: translateY(12px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .hero-content { position: relative; z-index: 1; text-align: center; max-width: 740px; }

  .hero h1 {
    font-family: 'DM Serif Display', serif;
    font-size: clamp(3rem, 8vw, 5.5rem);
    color: #FFFFFF;
    line-height: 1.05;
    margin-bottom: 1.5rem;
    opacity: 0;
    animation: slideUp 0.8s ease 0.3s forwards;
  }

  .hero h1 em {
    font-style: italic;
    color: var(--sky-mid);
  }

  .hero-sub {
    font-size: 1.15rem;
    color: rgba(255,255,255,0.55);
    line-height: 1.7;
    max-width: 520px;
    margin: 0 auto 2.5rem;
    font-weight: 300;
    opacity: 0;
    animation: slideUp 0.8s ease 0.5s forwards;
  }

  .cta-group {
    display: flex;
    gap: 14px;
    justify-content: center;
    flex-wrap: wrap;
    opacity: 0;
    animation: slideUp 0.8s ease 0.7s forwards;
  }

  .btn-primary {
    background: var(--warm);
    color: #fff;
    border: none;
    padding: 14px 32px;
    border-radius: 999px;
    font-size: 15px;
    font-weight: 600;
    font-family: 'DM Sans', sans-serif;
    cursor: pointer;
    transition: background 0.2s, transform 0.15s;
    text-decoration: none;
    display: inline-block;
  }
  .btn-primary:hover { background: var(--warm-deep); transform: translateY(-2px); }

  .btn-ghost {
    background: transparent;
    color: rgba(255,255,255,0.7);
    border: 1px solid rgba(255,255,255,0.2);
    padding: 14px 32px;
    border-radius: 999px;
    font-size: 15px;
    font-weight: 500;
    font-family: 'DM Sans', sans-serif;
    cursor: pointer;
    transition: border-color 0.2s, color 0.2s;
    text-decoration: none;
    display: inline-block;
  }
  .btn-ghost:hover { border-color: rgba(255,255,255,0.5); color: #fff; }

  /* WEATHER WIDGET */
  .weather-preview {
    position: relative; z-index: 1;
    margin-top: 4rem;
    background: rgba(255,255,255,0.06);
    backdrop-filter: blur(12px);
    border: 1px solid rgba(255,255,255,0.1);
    border-radius: 20px;
    padding: 1.5rem 2rem;
    display: flex;
    align-items: center;
    gap: 2rem;
    max-width: 500px;
    width: 100%;
    opacity: 0;
    animation: slideUp 0.8s ease 0.9s forwards;
    flex-wrap: wrap;
    justify-content: center;
  }

  .weather-temp {
    font-family: 'DM Serif Display', serif;
    font-size: 3.5rem;
    color: #fff;
    line-height: 1;
  }

  .weather-info { flex: 1; min-width: 160px; }
  .weather-city { font-size: 13px; color: rgba(255,255,255,0.5); margin-bottom: 4px; letter-spacing: 0.05em; text-transform: uppercase; }
  .weather-desc { font-size: 15px; color: rgba(255,255,255,0.85); font-weight: 400; }
  .weather-outfit { font-size: 13px; color: var(--sky-mid); margin-top: 6px; }

  .outfit-tags { display: flex; gap: 6px; margin-top: 8px; flex-wrap: wrap; }
  .outfit-tag {
    background: rgba(107,184,232,0.15);
    color: #8ECFEF;
    border: 1px solid rgba(107,184,232,0.3);
    border-radius: 999px;
    padding: 3px 10px;
    font-size: 12px;
  }

  /* SECTION SHARED */
  section { padding: 6rem 2rem; }

  .container { max-width: 1100px; margin: 0 auto; }

  .label {
    display: inline-block;
    font-size: 12px;
    font-weight: 600;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--warm-deep);
    margin-bottom: 1rem;
  }

  .section-title {
    font-family: 'DM Serif Display', serif;
    font-size: clamp(2rem, 4vw, 3rem);
    line-height: 1.1;
    margin-bottom: 1.25rem;
    color: var(--night);
  }

  .section-body {
    font-size: 1.05rem;
    color: var(--muted);
    line-height: 1.75;
    max-width: 620px;
  }

  /* PROBLEM SECTION */
  .problem-section { background: var(--sand); }

  .problem-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 1.5rem;
    margin-top: 3rem;
  }

  .problem-card {
    background: #fff;
    border-radius: 16px;
    padding: 1.75rem;
    border: 1px solid rgba(0,0,0,0.06);
  }

  .problem-icon {
    font-size: 2rem;
    margin-bottom: 1rem;
  }

  .problem-card h3 {
    font-family: 'DM Serif Display', serif;
    font-size: 1.2rem;
    margin-bottom: 0.6rem;
    color: var(--night);
  }

  .problem-card p {
    font-size: 0.92rem;
    color: var(--muted);
    line-height: 1.65;
  }

  /* SOLUTION */
  .solution-section { background: #fff; }

  .features-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
    margin-top: 3.5rem;
  }

  .feature {
    display: flex;
    gap: 1.25rem;
    align-items: flex-start;
  }

  .feature-dot {
    width: 44px;
    height: 44px;
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.3rem;
    flex-shrink: 0;
  }

  .dot-sky { background: #E6F4FC; }
  .dot-warm { background: #FCEEE6; }
  .dot-leaf { background: #EAF3EC; }
  .dot-sand { background: #F7F2EA; }

  .feature-text h3 {
    font-weight: 600;
    font-size: 1rem;
    margin-bottom: 0.4rem;
    color: var(--night);
  }

  .feature-text p {
    font-size: 0.9rem;
    color: var(--muted);
    line-height: 1.65;
  }

  /* HOW IT WORKS */
  .how-section { background: var(--night); }
  .how-section .section-title { color: #fff; }
  .how-section .section-body { color: rgba(255,255,255,0.5); }
  .how-section .label { color: var(--sky-mid); }

  .steps {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 1.5rem;
    margin-top: 3.5rem;
    position: relative;
  }

  .step {
    background: rgba(255,255,255,0.05);
    border: 1px solid rgba(255,255,255,0.08);
    border-radius: 16px;
    padding: 1.75rem;
  }

  .step-num {
    font-family: 'DM Serif Display', serif;
    font-size: 2.5rem;
    color: rgba(255,255,255,0.15);
    line-height: 1;
    margin-bottom: 1rem;
  }

  .step h3 {
    font-weight: 500;
    color: #fff;
    margin-bottom: 0.5rem;
    font-size: 1rem;
  }

  .step p {
    font-size: 0.88rem;
    color: rgba(255,255,255,0.45);
    line-height: 1.65;
  }

  /* WHO IT HELPS */
  .who-section { background: var(--snow); }

  .personas {
    display: flex;
    gap: 1.5rem;
    margin-top: 3rem;
    flex-wrap: wrap;
  }

  .persona {
    flex: 1;
    min-width: 200px;
    background: #fff;
    border-radius: 16px;
    padding: 2rem 1.5rem;
    border: 1px solid rgba(0,0,0,0.06);
    text-align: center;
  }

  .persona-avatar {
    width: 60px;
    height: 60px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.6rem;
    margin: 0 auto 1rem;
  }

  .persona h3 {
    font-weight: 600;
    font-size: 0.95rem;
    margin-bottom: 0.4rem;
    color: var(--night);
  }
  .persona p {
    font-size: 0.85rem;
    color: var(--muted);
    line-height: 1.6;
  }

  /* FOOTER */
  footer {
    background: var(--night);
    color: rgba(255,255,255,0.35);
    text-align: center;
    padding: 2.5rem;
    font-size: 0.85rem;
  }

  footer strong { color: rgba(255,255,255,0.7); font-weight: 500; }

  /* Responsive tweaks */
  @media (max-width: 600px) {
    .hero { padding: 3rem 1.25rem 4rem; }
    section { padding: 4rem 1.25rem; }
  }
</style>
</head>
<body>

<!-- HERO -->
<section class="hero">
  <div class="hero-bg"></div>
  <div class="orb orb1"></div>
  <div class="orb orb2"></div>
  <div class="orb orb3"></div>

  <div class="season-bar">
    <span class="chip">❄️ Winter</span>
    <span class="chip">🌱 Spring</span>
    <span class="chip">☀️ Summer</span>
    <span class="chip">🍂 Fall</span>
  </div>

  <div class="hero-content">
    <h1>Your NYC closet,<br /><em>finally intelligent</em></h1>
    <p class="hero-sub">Smart Wardrobe AI takes the daily stress out of getting dressed — using real-time weather, your personal style, and your actual closet space to outfit you perfectly, every day.</p>
    <div class="cta-group">
      <a href="#solution" class="btn-primary">See How It Works</a>
      <a href="#problem" class="btn-ghost">The Problem We Solve</a>
    </div>
  </div>

  <div class="weather-preview">
    <div class="weather-temp">48°</div>
    <div class="weather-info">
      <div class="weather-city">📍 New York City, Today</div>
      <div class="weather-desc">Partly cloudy, chilly winds</div>
      <div class="weather-outfit">Today's recommendation:</div>
      <div class="outfit-tags">
        <span class="outfit-tag">Light wool coat</span>
        <span class="outfit-tag">Dark jeans</span>
        <span class="outfit-tag">Chelsea boots</span>
      </div>
    </div>
  </div>
</section>

<!-- PROBLEM -->
<section class="problem-section" id="problem">
  <div class="container">
    <span class="label">The Challenge</span>
    <h2 class="section-title">NYC living is tight.<br/>Wardrobes make it tighter.</h2>
    <p class="section-body">New York City residents — especially families in small apartments — face a relentless cycle of seasonal clothing changes with nowhere to put it all. The city's four unpredictable seasons demand a wide variety of clothing, but the average NYC apartment offers minimal storage.</p>

    <div class="problem-grid">
      <div class="problem-card">
        <div class="problem-icon">📦</div>
        <h3>Limited Storage Space</h3>
        <p>NYC apartments average 750 sq ft. Closets are small, and seasonal storage bins quickly consume every available corner.</p>
      </div>
      <div class="problem-card">
        <div class="problem-icon">🌦️</div>
        <h3>Unpredictable Weather</h3>
        <p>New York experiences all four seasons — sometimes in one week. Residents constantly scramble to find the right outfit for today's forecast.</p>
      </div>
      <div class="problem-card">
        <div class="problem-icon">⏱️</div>
        <h3>Decision Fatigue</h3>
        <p>The average person makes 35,000 decisions per day. Choosing what to wear from a cluttered closet adds unnecessary stress every morning.</p>
      </div>
      <div class="problem-card">
        <div class="problem-icon">👕</div>
        <h3>Forgotten Clothing</h3>
        <p>Without an organized system, clothes get buried, forgotten, and re-purchased — wasting money and adding more clutter.</p>
      </div>
    </div>
  </div>
</section>

<!-- SOLUTION -->
<section class="solution-section" id="solution">
  <div class="container">
    <span class="label">The Solution</span>
    <h2 class="section-title">Smart Wardrobe AI</h2>
    <p class="section-body">An intelligent wardrobe companion that learns your style, watches the weather, and helps you organize seasonal clothing — so your mornings are effortless and your closet stays manageable.</p>

    <div class="features-grid">
      <div class="feature">
        <div class="feature-dot dot-sky">🌤️</div>
        <div class="feature-text">
          <h3>Weather-Based Daily Outfits</h3>
          <p>Syncs with NYC weather forecasts and recommends a complete outfit from your actual wardrobe — not generic suggestions.</p>
        </div>
      </div>
      <div class="feature">
        <div class="feature-dot dot-warm">🤖</div>
        <div class="feature-text">
          <h3>AI That Learns Your Style</h3>
          <p>The more you use it, the smarter it gets. Smart Wardrobe AI adapts to your preferences, favorite items, and comfort level over time.</p>
        </div>
      </div>
      <div class="feature">
        <div class="feature-dot dot-leaf">🔄</div>
        <div class="feature-text">
          <h3>Seasonal Rotation Reminders</h3>
          <p>Receive smart prompts when it's time to swap winter coats for spring layers — optimizing your closet space automatically.</p>
        </div>
      </div>
      <div class="feature">
        <div class="feature-dot dot-sand">📸</div>
        <div class="feature-text">
          <h3>Virtual Closet Inventory</h3>
          <p>Upload photos of your clothes to build a digital wardrobe. See what you own, what you wear most, and what's just taking up space.</p>
        </div>
      </div>
      <div class="feature">
        <div class="feature-dot dot-sky">📊</div>
        <div class="feature-text">
          <h3>Wear Tracking & Insights</h3>
          <p>Understand your clothing habits — which items are workhorses and which are forgotten — so you shop smarter going forward.</p>
        </div>
      </div>
      <div class="feature">
        <div class="feature-dot dot-warm">📏</div>
        <div class="feature-text">
          <h3>Space-Aware Organization</h3>
          <p>Tell the app how much storage you have and it builds a seasonal system that fits your real-world constraints.</p>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- HOW IT WORKS -->
<section class="how-section">
  <div class="container">
    <span class="label">How It Works</span>
    <h2 class="section-title">Four steps to a smarter closet</h2>

    <div class="steps">
      <div class="step">
        <div class="step-num">01</div>
        <h3>Build Your Wardrobe</h3>
        <p>Snap photos of your clothes and upload them. The AI categorizes each item by season, type, and style automatically.</p>
      </div>
      <div class="step">
        <div class="step-num">02</div>
        <h3>Share Your Space & Style</h3>
        <p>Answer a few quick questions about your closet dimensions, storage bins, and style preferences.</p>
      </div>
      <div class="step">
        <div class="step-num">03</div>
        <h3>Get Daily Recommendations</h3>
        <p>Every morning, receive a complete outfit suggestion based on today's NYC weather and your personal wardrobe.</p>
      </div>
      <div class="step">
        <div class="step-num">04</div>
        <h3>Stay Organized Year-Round</h3>
        <p>Receive seasonal rotation reminders and closet insights that keep your space clutter-free all year long.</p>
      </div>
    </div>
  </div>
</section>

<!-- WHO IT HELPS -->
<section class="who-section" id="who">
  <div class="container">
    <span class="label">Who It's For</span>
    <h2 class="section-title">Built for real New Yorkers</h2>
    <p class="section-body">Smart Wardrobe AI is designed for anyone living the NYC apartment life — where space is limited and time is precious.</p>

    <div class="personas">
      <div class="persona">
        <div class="persona-avatar" style="background:#EAF3EC;">👨‍👩‍👧</div>
        <h3>NYC Families</h3>
        <p>Managing clothing for multiple people in a small apartment — especially kids who outgrow things seasonally.</p>
      </div>
      <div class="persona">
        <div class="persona-avatar" style="background:#E6F4FC;">💼</div>
        <h3>Working Professionals</h3>
        <p>Busy schedules demand fast, confident outfit decisions. No more morning stress about what to wear.</p>
      </div>
      <div class="persona">
        <div class="persona-avatar" style="background:#FCEEE6;">🎓</div>
        <h3>Students</h3>
        <p>Living in tiny dorms or shared apartments with limited closet space and tight budgets for clothing.</p>
      </div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <strong>Smart Wardrobe AI</strong> &nbsp;·&nbsp; Built for NYC. Built for real life.<br/>
  <span style="margin-top: 0.5rem; display: block;">Created as part of the <strong>Pursuit Fellowship</strong> program · 2024</span>
</footer>

</body>
</html>

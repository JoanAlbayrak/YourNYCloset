<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Smart Wardrobe AI</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Sans:opsz,wght@9..40,300;9..40,400;9..40,500;9..40,600&display=swap');

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

:root {
  --sky-mid: #6BB8E8;
  --night: #0D1B2A;
  --sand: #F5EFE6;
  --warm: #E8956A;
  --warm-deep: #C96B3A;
  --snow: #FAFCFF;
  --muted: #6B7C8D;
  --text: #1A2733;
}

html { scroll-behavior: smooth; }

body {
  font-family: 'DM Sans', sans-serif;
  background: var(--snow);
  color: var(--text);
  overflow-x: hidden;
}

/* ── HERO ── */
.hero {
  min-height: 100vh;
  background: linear-gradient(160deg, #162436 0%, #0D1B2A 60%, #0a1520 100%);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 4rem 1.5rem 5rem;
  text-align: center;
}

.season-bar {
  display: flex;
  gap: 10px;
  margin-bottom: 2.5rem;
  flex-wrap: wrap;
  justify-content: center;
}

.chip {
  font-size: 13px;
  font-weight: 500;
  padding: 6px 16px;
  border-radius: 999px;
  border: 1px solid rgba(255,255,255,0.15);
  background: rgba(255,255,255,0.07);
  color: rgba(255,255,255,0.75);
}

.hero h1 {
  font-family: 'DM Serif Display', Georgia, serif;
  font-size: clamp(2.6rem, 7vw, 5rem);
  color: #fff;
  line-height: 1.08;
  margin-bottom: 1.25rem;
  max-width: 700px;
}

.hero h1 em {
  font-style: italic;
  color: var(--sky-mid);
}

.hero-sub {
  font-size: 1.1rem;
  color: rgba(255,255,255,0.55);
  line-height: 1.75;
  max-width: 520px;
  margin: 0 auto 2.5rem;
  font-weight: 300;
}

.cta-group {
  display: flex;
  gap: 12px;
  justify-content: center;
  flex-wrap: wrap;
  margin-bottom: 3.5rem;
}

.btn-primary {
  background: var(--warm);
  color: #fff;
  border: none;
  padding: 13px 30px;
  border-radius: 999px;
  font-size: 15px;
  font-weight: 600;
  font-family: inherit;
  cursor: pointer;
  text-decoration: none;
  display: inline-block;
  transition: background 0.2s;
}
.btn-primary:hover { background: var(--warm-deep); }

.btn-ghost {
  background: transparent;
  color: rgba(255,255,255,0.65);
  border: 1px solid rgba(255,255,255,0.2);
  padding: 13px 30px;
  border-radius: 999px;
  font-size: 15px;
  font-weight: 400;
  font-family: inherit;
  cursor: pointer;
  text-decoration: none;
  display: inline-block;
  transition: border-color 0.2s, color 0.2s;
}
.btn-ghost:hover { border-color: rgba(255,255,255,0.45); color: #fff; }

/* weather card */
.weather-card {
  background: rgba(255,255,255,0.08);
  border: 1px solid rgba(255,255,255,0.12);
  border-radius: 18px;
  padding: 1.4rem 2rem;
  display: flex;
  align-items: center;
  gap: 2rem;
  max-width: 480px;
  width: 100%;
  flex-wrap: wrap;
  justify-content: center;
}

.w-temp {
  font-family: 'DM Serif Display', Georgia, serif;
  font-size: 3.8rem;
  color: #fff;
  line-height: 1;
}

.w-info { text-align: left; }
.w-city { font-size: 12px; color: rgba(255,255,255,0.45); text-transform: uppercase; letter-spacing: 0.08em; margin-bottom: 4px; }
.w-desc { font-size: 14px; color: rgba(255,255,255,0.8); margin-bottom: 6px; }
.w-label { font-size: 12px; color: var(--sky-mid); margin-bottom: 6px; }
.w-tags { display: flex; gap: 6px; flex-wrap: wrap; }
.w-tag {
  background: rgba(107,184,232,0.15);
  color: #8ECFEF;
  border: 1px solid rgba(107,184,232,0.25);
  border-radius: 999px;
  padding: 3px 10px;
  font-size: 12px;
}

/* ── SHARED ── */
section { padding: 5.5rem 1.5rem; }
.container { max-width: 1080px; margin: 0 auto; }

.eyebrow {
  display: inline-block;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--warm-deep);
  margin-bottom: 0.9rem;
}

.s-title {
  font-family: 'DM Serif Display', Georgia, serif;
  font-size: clamp(1.8rem, 4vw, 2.8rem);
  line-height: 1.1;
  color: var(--night);
  margin-bottom: 1rem;
}

.s-body {
  font-size: 1rem;
  color: var(--muted);
  line-height: 1.75;
  max-width: 580px;
}

/* ── PROBLEM ── */
.problem-section { background: var(--sand); }

.problem-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 1.25rem;
  margin-top: 3rem;
}

.p-card {
  background: #fff;
  border-radius: 14px;
  padding: 1.6rem;
  border: 1px solid rgba(0,0,0,0.06);
}

.p-icon { font-size: 1.8rem; margin-bottom: 0.8rem; }

.p-card h3 {
  font-family: 'DM Serif Display', Georgia, serif;
  font-size: 1.1rem;
  margin-bottom: 0.5rem;
  color: var(--night);
}

.p-card p { font-size: 0.88rem; color: var(--muted); line-height: 1.65; }

/* ── SOLUTION ── */
.solution-section { background: #fff; }

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.75rem;
  margin-top: 3rem;
}

.feat { display: flex; gap: 1.1rem; align-items: flex-start; }

.feat-icon {
  width: 42px; height: 42px;
  border-radius: 10px;
  display: flex; align-items: center; justify-content: center;
  font-size: 1.2rem;
  flex-shrink: 0;
}

.ic-sky  { background: #E6F4FC; }
.ic-warm { background: #FCEEE6; }
.ic-leaf { background: #EAF3EC; }
.ic-sand { background: #F7F2EA; }

.feat h3 { font-weight: 600; font-size: 0.95rem; margin-bottom: 0.35rem; color: var(--night); }
.feat p  { font-size: 0.87rem; color: var(--muted); line-height: 1.65; }

/* ── HOW IT WORKS ── */
.how-section { background: var(--night); }
.how-section .eyebrow { color: var(--sky-mid); }
.how-section .s-title { color: #fff; }
.how-section .s-body  { color: rgba(255,255,255,0.45); }

.steps {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(210px, 1fr));
  gap: 1.25rem;
  margin-top: 3rem;
}

.step {
  background: rgba(255,255,255,0.05);
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 14px;
  padding: 1.6rem;
}

.step-num {
  font-family: 'DM Serif Display', Georgia, serif;
  font-size: 2.2rem;
  color: rgba(255,255,255,0.12);
  line-height: 1;
  margin-bottom: 0.8rem;
}

.step h3 { font-weight: 500; color: #fff; margin-bottom: 0.4rem; font-size: 0.95rem; }
.step p  { font-size: 0.85rem; color: rgba(255,255,255,0.42); line-height: 1.65; }

/* ── WHO ── */
.who-section { background: var(--snow); }

.personas {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1.25rem;
  margin-top: 3rem;
}

.persona {
  background: #fff;
  border-radius: 14px;
  padding: 2rem 1.5rem;
  border: 1px solid rgba(0,0,0,0.06);
  text-align: center;
}

.p-avatar {
  width: 56px; height: 56px;
  border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-size: 1.5rem;
  margin: 0 auto 1rem;
}

.persona h3 { font-weight: 600; font-size: 0.92rem; margin-bottom: 0.4rem; color: var(--night); }
.persona p  { font-size: 0.83rem; color: var(--muted); line-height: 1.6; }

/* ── FOOTER ── */
footer {
  background: var(--night);
  color: rgba(255,255,255,0.35);
  text-align: center;
  padding: 2.5rem 1rem;
  font-size: 0.85rem;
  line-height: 1.8;
}

footer strong { color: rgba(255,255,255,0.7); font-weight: 500; }

@media (max-width: 500px) {
  .w-info { text-align: center; }
  .w-tags { justify-content: center; }
}
</style>
</head>
<body>

<!-- HERO -->
<section class="hero">
  <div class="season-bar">
    <span class="chip">❄️ Winter</span>
    <span class="chip">🌱 Spring</span>
    <span class="chip">☀️ Summer</span>
    <span class="chip">🍂 Fall</span>
  </div>

  <h1>Your NYC closet,<br><em>finally intelligent</em></h1>

  <p class="hero-sub">Smart Wardrobe AI takes the daily stress out of getting dressed — using real-time weather, your personal style, and your actual closet space to outfit you perfectly, every day.</p>

  <div class="cta-group">
    <a href="#solution" class="btn-primary">See How It Works</a>
    <a href="#problem" class="btn-ghost">The Problem We Solve</a>
  </div>

  <div class="weather-card">
    <div class="w-temp">48°</div>
    <div class="w-info">
      <div class="w-city">📍 New York City · Today</div>
      <div class="w-desc">Partly cloudy, chilly winds</div>
      <div class="w-label">Today's AI recommendation:</div>
      <div class="w-tags">
        <span class="w-tag">Light wool coat</span>
        <span class="w-tag">Dark jeans</span>
        <span class="w-tag">Chelsea boots</span>
      </div>
    </div>
  </div>
</section>

<!-- PROBLEM -->
<section class="problem-section" id="problem">
  <div class="container">
    <span class="eyebrow">The Challenge</span>
    <h2 class="s-title">NYC living is tight.<br>Wardrobes make it tighter.</h2>
    <p class="s-body">New York City residents — especially families in small apartments — face a relentless cycle of seasonal clothing changes with nowhere to put it all. The city's four unpredictable seasons demand a wide variety of clothing, but the average NYC apartment offers minimal storage.</p>

    <div class="problem-grid">
      <div class="p-card">
        <div class="p-icon">📦</div>
        <h3>Limited Storage Space</h3>
        <p>NYC apartments average 750 sq ft. Closets are small and seasonal storage bins quickly consume every available corner.</p>
      </div>
      <div class="p-card">
        <div class="p-icon">🌦️</div>
        <h3>Unpredictable Weather</h3>
        <p>New York experiences all four seasons — sometimes in one week. Residents constantly scramble to find the right outfit for today's forecast.</p>
      </div>
      <div class="p-card">
        <div class="p-icon">⏱️</div>
        <h3>Decision Fatigue</h3>
        <p>Choosing what to wear from a cluttered closet adds unnecessary mental load and stress to every single morning.</p>
      </div>
      <div class="p-card">
        <div class="p-icon">👕</div>
        <h3>Forgotten Clothing</h3>
        <p>Without an organized system, clothes get buried, forgotten, and re-purchased — wasting money and adding more clutter.</p>
      </div>
    </div>
  </div>
</section>

<!-- SOLUTION -->
<section class="solution-section" id="solution">
  <div class="container">
    <span class="eyebrow">The Solution</span>
    <h2 class="s-title">Smart Wardrobe AI</h2>
    <p class="s-body">An intelligent wardrobe companion that learns your style, watches the weather, and helps you organize seasonal clothing — so your mornings are effortless and your closet stays manageable.</p>

    <div class="features-grid">
      <div class="feat">
        <div class="feat-icon ic-sky">🌤️</div>
        <div>
          <h3>Weather-Based Daily Outfits</h3>
          <p>Syncs with NYC weather forecasts and recommends a complete outfit from your actual wardrobe each morning.</p>
        </div>
      </div>
      <div class="feat">
        <div class="feat-icon ic-warm">🤖</div>
        <div>
          <h3>AI That Learns Your Style</h3>
          <p>The more you use it, the smarter it gets — adapting to your preferences, favorite items, and comfort level.</p>
        </div>
      </div>
      <div class="feat">
        <div class="feat-icon ic-leaf">🔄</div>
        <div>
          <h3>Seasonal Rotation Reminders</h3>
          <p>Smart prompts when it's time to swap winter coats for spring layers, optimizing closet space automatically.</p>
        </div>
      </div>
      <div class="feat">
        <div class="feat-icon ic-sand">📸</div>
        <div>
          <h3>Virtual Closet Inventory</h3>
          <p>Upload photos of your clothes to build a digital wardrobe — see what you own and what you actually wear.</p>
        </div>
      </div>
      <div class="feat">
        <div class="feat-icon ic-sky">📊</div>
        <div>
          <h3>Wear Tracking & Insights</h3>
          <p>Discover which items are workhorses and which are forgotten, so you shop smarter going forward.</p>
        </div>
      </div>
      <div class="feat">
        <div class="feat-icon ic-warm">📏</div>
        <div>
          <h3>Space-Aware Organization</h3>
          <p>Tell the app your storage limits and it builds a seasonal system that fits your real-world constraints.</p>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- HOW IT WORKS -->
<section class="how-section" id="how">
  <div class="container">
    <span class="eyebrow">How It Works</span>
    <h2 class="s-title">Four steps to a smarter closet</h2>
    <p class="s-body">Getting started takes less than 15 minutes. From there, Smart Wardrobe AI does the heavy lifting every day.</p>

    <div class="steps">
      <div class="step">
        <div class="step-num">01</div>
        <h3>Build Your Wardrobe</h3>
        <p>Snap photos of your clothes and upload them. The AI categorizes each item by season, type, and style automatically.</p>
      </div>
      <div class="step">
        <div class="step-num">02</div>
        <h3>Share Your Space & Style</h3>
        <p>Answer a few quick questions about your closet size, storage bins, and personal style preferences.</p>
      </div>
      <div class="step">
        <div class="step-num">03</div>
        <h3>Get Daily Recommendations</h3>
        <p>Every morning, receive a complete outfit based on today's NYC weather and your personal wardrobe inventory.</p>
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
    <span class="eyebrow">Who It's For</span>
    <h2 class="s-title">Built for real New Yorkers</h2>
    <p class="s-body">Smart Wardrobe AI is for anyone living the NYC apartment life — where space is limited and time is precious.</p>

    <div class="personas">
      <div class="persona">
        <div class="p-avatar" style="background:#EAF3EC;">👨‍👩‍👧</div>
        <h3>NYC Families</h3>
        <p>Managing clothing for multiple people in a small apartment, including kids who outgrow things each season.</p>
      </div>
      <div class="persona">
        <div class="p-avatar" style="background:#E6F4FC;">💼</div>
        <h3>Working Professionals</h3>
        <p>Busy schedules demand fast, confident outfit decisions. No more morning stress about what to wear.</p>
      </div>
      <div class="persona">
        <div class="p-avatar" style="background:#FCEEE6;">🎓</div>
        <h3>Students</h3>
        <p>Living in tiny dorms or shared apartments with limited closet space and tight budgets for clothing.</p>
      </div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <strong>Smart Wardrobe AI</strong> &nbsp;·&nbsp; Built for NYC. Built for real life.<br>
  Created as part of the <strong>Pursuit Fellowship</strong> program · 2024
</footer>

</body>
</html>

# SHREYAS BIDWAI — PORTFOLIO WEBSITE
# Complete Design & Build Specification
# Version 2.0 — May 2026 (HTML + CSS + Vanilla JS)

---

## 1. IDENTITY & POSITIONING

**Name:** Shreyas Bidwai
**Title:** AI Engineer
**One-liner:** I build production AI systems — RAG pipelines, LLM orchestration, and agentic workflows — that serve real users at scale.
**Target audience:** Engineering hiring managers, startup founders/CTOs, AI team leads
**Goal:** Visitor thinks "this person ships production AI, not tutorials" within 10 seconds

---

## 2. DESIGN PHILOSOPHY

Dark, minimal, engineered — like Linear, Vercel, or Raycast. NOT a creative portfolio. NOT a template. Feels like a control panel for viewing engineering work.

Technically confident, quietly impressive. No "passionate developer" language. No emojis. No generic tech imagery. Let the work speak.

---

## 3. TECH STACK

```
Structure:     Single index.html (all sections, anchor nav)
Styling:       Single style.css (CSS variables, no frameworks)
Interactivity: Single script.js (scroll animations, mobile nav, smooth scroll)
Fonts:         Google Fonts CDN — Inter + JetBrains Mono
Deployment:    Netlify (free) or GitHub Pages (free)
```

**File structure:**
```
portfolio/
├── index.html
├── style.css
├── script.js
├── assets/
│   ├── resume.pdf
│   ├── og-image.png
│   └── projects/
│       ├── video-platform-arch.svg
│       ├── rag-pipeline-arch.svg
│       └── market-agent-arch.svg
└── README.md
```

---

## 4. DESIGN SYSTEM

### 4.1 Colors (CSS Variables)
```css
:root {
  --bg-primary: #0A0A0A;
  --bg-secondary: #111111;
  --bg-tertiary: #1A1A1A;
  --text-primary: #EDEDED;
  --text-secondary: #888888;
  --text-tertiary: #555555;
  --accent: #00D4AA;
  --accent-hover: #00E8BB;
  --accent-dim: rgba(0, 212, 170, 0.08);
  --border: #1E1E1E;
  --border-hover: #333333;
  --container-max: 1100px;
  --card-radius: 12px;
  --gap: 24px;
}
```

### 4.2 Fonts
```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
```
- Headings + body: `'Inter', sans-serif`
- Code/tags/metrics: `'JetBrains Mono', monospace`

### 4.3 Type Scale
```css
.hero-heading    { font-size: clamp(2rem, 5vw, 3.5rem); font-weight: 700; }
.section-heading { font-size: clamp(1.5rem, 3vw, 2rem); font-weight: 600; }
.card-title      { font-size: 1.25rem; font-weight: 600; }
.body-text       { font-size: 1rem; line-height: 1.7; }
.small-text      { font-size: 0.875rem; color: var(--text-secondary); }
.mono-tag        { font-family: 'JetBrains Mono', monospace; font-size: 0.75rem;
                   text-transform: uppercase; letter-spacing: 0.05em; }
```

### 4.4 Animations (CSS + IntersectionObserver)
```css
.fade-in {
  opacity: 0; transform: translateY(20px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}
.fade-in.visible { opacity: 1; transform: translateY(0); }
.fade-in[data-delay="1"] { transition-delay: 0.1s; }
.fade-in[data-delay="2"] { transition-delay: 0.2s; }
.fade-in[data-delay="3"] { transition-delay: 0.3s; }
```

---

## 5. SECTIONS

### 5.1 Navbar (sticky, blur on scroll)
- Left: "SB" monogram in accent
- Right: About, Experience, Projects, Skills, Contact, Resume ↓ button
- On scroll >50px: `background: rgba(10,10,10,0.85); backdrop-filter: blur(10px);`
- Mobile: hamburger → slide-in nav links

### 5.2 Hero (min-height 90vh)
- "Hi, I'm Shreyas." (small text)
- "I build production AI systems." (big heading)
- "RAG pipelines · LLM orchestration · Agentic workflows · 500+ daily queries" (subtitle with accent dots)
- "Currently at Datagrid Solutions, building AI middleware that routes queries through intelligent multi-model orchestration."
- Two buttons: [View Projects] [Download Resume]
- Social links: GitHub, LinkedIn, Medium
- Background: subtle CSS dot grid pattern
- NO: images, 3D, particles, typing animation

### 5.3 About (two-column)
- Left: 3 paragraphs of text
- Right: 4 metrics in JetBrains Mono (500+, 30%, 90%, ₹3.5-5L) with accent-colored numbers

### 5.4 Experience (vertical timeline)
- Dot + line timeline, left-aligned
- Entry 1: Software & AI Developer — Datagrid (Jul 2025 – Present) + tech tags
- Entry 2: Data Science Intern — Bosch (Dec 2023 – Jan 2024) + tech tags

### 5.5 Projects (2-column grid, MOST IMPORTANT SECTION)
4 cards:
1. **AI Video Production Platform** — status: Personal Project. Flask, React, PostgreSQL, Celery, Redis, Claude API, Docker. Architecture: 7-table PostgreSQL schema, provider-agnostic AI service, Celery async, React Flow.
2. **Autonomous Market Intelligence Agent** — status: Agentic AI. Hermes Agent, OpenRouter, Telegram API, Linux, Cron. Impact: 30+ calls → 15/day, 24/7 systemd service.
3. **Forest Monitoring System** — status: 🏆 1st Prize. Python, U-Net, QGIS, Deep Learning. Results: 90% accuracy, 64 sq km, 800+ images, government-sponsored.
4. **Coming soon** (dashed border) — FinSight AI, Voyager AI, MedAssist AI.

### 5.6 Skills (3-column grid)
6 categories: AI & LLM Systems, LLM APIs, Backend & APIs, Databases, Infrastructure, AI-Native Tools. Each: monospace heading + dot-separated list.

### 5.7 Contact (centered)
- "Let's build something."
- "Open to AI Engineer, GenAI Engineer, and ML Engineer roles at product companies in Bangalore, Pune, Mumbai, or remote."
- Email button + social links

### 5.8 Footer
- "Built by Shreyas Bidwai · 2026"

---

## 6. script.js (complete)

```javascript
// Scroll-triggered fade-in
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      entry.target.classList.add('visible');
      observer.unobserve(entry.target);
    }
  });
}, { threshold: 0.1 });
document.querySelectorAll('.fade-in').forEach(el => observer.observe(el));

// Sticky nav
window.addEventListener('scroll', () => {
  document.getElementById('navbar').classList.toggle('scrolled', window.scrollY > 50);
});

// Mobile hamburger
const hamburger = document.querySelector('.nav-hamburger');
const navLinks = document.querySelector('.nav-links');
if (hamburger) {
  hamburger.addEventListener('click', () => navLinks.classList.toggle('open'));
  navLinks.querySelectorAll('a').forEach(link =>
    link.addEventListener('click', () => navLinks.classList.remove('open'))
  );
}

// Smooth scroll
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
  anchor.addEventListener('click', function(e) {
    e.preventDefault();
    const target = document.querySelector(this.getAttribute('href'));
    if (target) target.scrollIntoView({ behavior: 'smooth', block: 'start' });
  });
});

// Active nav highlight
const sections = document.querySelectorAll('section[id]');
window.addEventListener('scroll', () => {
  const scrollY = window.scrollY + 100;
  sections.forEach(section => {
    const top = section.offsetTop;
    const height = section.offsetHeight;
    const link = document.querySelector(`.nav-links a[href="#${section.id}"]`);
    if (link) link.classList.toggle('active', scrollY >= top && scrollY < top + height);
  });
});
```

---

## 7. SEO Meta Tags
```html
<title>Shreyas Bidwai — AI Engineer | Production RAG, LLM Orchestration</title>
<meta name="description" content="AI Engineer building production RAG pipelines, LLM orchestration, and agentic AI systems. Currently at Datagrid Solutions.">
<meta property="og:title" content="Shreyas Bidwai — AI Engineer">
<meta property="og:description" content="I build production AI systems — RAG pipelines, LLM orchestration, and agentic workflows.">
<meta property="og:image" content="assets/og-image.png">
```

---

## 8. DEPLOYMENT

**Netlify (simplest):** Push to GitHub → netlify.com → New site from Git → Deploy. No build command needed.

**GitHub Pages:** Repo named `ShreyasBidwai.github.io` → Enable Pages in Settings.

**Domain:** Buy shreyasbidwai.dev (~₹800/year) when ready, or keep .netlify.app for now.

---

## 9. CONTENT — READY TO PASTE

**Hero:** "I build production AI systems."

**Subtitle:** "RAG pipelines · LLM orchestration · Agentic workflows · 500+ daily queries"

**About:**
"I build AI systems that run in production — not notebooks that demo well.
At Datagrid Solutions, I architect RAG pipelines with FAISS vector search, design multi-model LLM orchestration across Claude, GPT-4o, and Gemini, and build FastAPI middleware serving 500+ daily queries.
Before this, I built SARIMA forecasting models at Bosch that saved ₹3.5-5 lakh annually and won 1st prize for a deep learning forest monitoring system among 150+ teams."

**Contact:** "Let's build something. Open to AI Engineer, GenAI Engineer, and ML Engineer roles at product companies in Bangalore, Pune, Mumbai, or remote."

---

## 10. PROMPT FOR CLAUDE CODE

```
Build a single-page portfolio website using plain HTML, CSS, and vanilla JavaScript.
No frameworks, no React, no Tailwind, no npm. Single index.html, style.css, script.js.

Design: Dark theme (#0A0A0A bg, #EDEDED text, #00D4AA accent).
Fonts: Inter + JetBrains Mono from Google Fonts CDN.
Aesthetic: Linear.app meets Vercel — engineered, minimal, dark, confident.

Sections (single page, smooth scroll anchor nav):
1. Sticky navbar — transparent, blurred dark bg on scroll, mobile hamburger
2. Hero — "I build production AI systems." big heading, subtitle with accent dots
   separating skills, two CTA buttons, social links. Dot grid background. 90vh.
3. About — two columns: text left, 4 metrics right (500+, 30%, 90%, ₹3.5-5L)
4. Experience — vertical timeline, 2 entries with tech tags
5. Projects — 2-col grid, 4 cards (AI Video Platform, Market Intelligence Agent,
   Forest Monitoring, Coming Soon placeholder with dashed border)
6. Skills — 3-col grid, 6 categories with monospace headings
7. Contact — centered, email button, social links
8. Footer — "Built by Shreyas Bidwai · 2026"

Animations: CSS fade-in (opacity+translateY) triggered by IntersectionObserver.
Fully responsive. No particles, no 3D, no typing animations, no Bootstrap.
```
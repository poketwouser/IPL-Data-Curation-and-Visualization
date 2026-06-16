<p align="center">
  <img src="https://img.shields.io/badge/IPL-Intelligence-f5a623?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48Y2lyY2xlIGN4PSIxMiIgY3k9IjEyIiByPSIxMCIgZmlsbD0iI2Y1YTYyMyIvPjwvc3ZnPg==&logoColor=white" alt="IPL Intelligence" />
  <br/>
  <img src="https://img.shields.io/badge/Dash-2.14+-00ADD8?style=flat-square&logo=plotly" />
  <img src="https://img.shields.io/badge/Plotly-5.18+-3F4F75?style=flat-square&logo=plotly" />
  <img src="https://img.shields.io/badge/Python-3.11-3776AB?style=flat-square&logo=python" />
  <img src="https://img.shields.io/badge/GSAP-3.12-88CE02?style=flat-square" />
  <img src="https://img.shields.io/badge/Deploy-GitHub_Pages-222222?style=flat-square&logo=github" />
  <a href="https://poketwouser.github.io/IPL-Intelligence/" target="_blank"><img src="https://img.shields.io/badge/Project_Site-GitHub_Pages-2088FF?style=flat-square&logo=github" /></a>
</p>

<h1 align="center">🏏 IPL Intelligence Platform</h1>

<p align="center">
  <strong><a href="https://poketwouser.github.io/IPL-Intelligence/">🌐 PROJECT SITE: poketwouser.github.io/IPL-Intelligence</a></strong>
  <br/>
  <sub>The interactive Dash app runs locally (see Quick Start). GitHub Pages hosts this static project page only.</sub>
</p>

<p align="center">
  <strong>Cinema-grade cricket analytics. Apple Sports × F1 aesthetics.</strong>
  <br/>
  <em>19 seasons (2008–2026 Live) · 1,235 matches · 293K+ deliveries — decoded.</em>
</p>

---

## ✨ What Is This?

IPL Intelligence is a **production-grade cricket analytics platform** built with Python, Dash, and Plotly. It transforms raw Cricsheet ball-by-ball data (2008–2026) into an immersive, cinematic sports intelligence experience.

This is not a dashboard. It's a **sports cinematography engine** — with GSAP-powered animations, glassmorphic UI, holographic player cards, scroll-triggered storytelling, and 3D tilt effects.

---

## 🧠 Problem Statement & Engineering Challenges

This vast Cricsheet IPL ball-by-ball dataset (**293,764 deliveries** across **1,235 matches** and **805 players**) contains incredible analytical potential, but standard visualization dashboards fail to capture the adrenaline-inducing, cinematic atmosphere, and storytelling inherent to T20 cricket. **The goal** was to build a highly performant, production-grade intelligence platform that marries deep statistical rigor with the premium aesthetics of modern sports broadcasting (e.g., Apple Sports, F1).

### Key Challenges & Solutions

1. **Handling Massive Data at Scale Without Crashing**
   * **Problem**: Processing 290K+ rows of delivery data across multiple interactive UI modules dynamically creates massive Memory (OOM) spikes and severe latency during route transitions.
   * **Solution**: Migrated from raw CSVs to **highly compressed Parquet files**. Data is pre-aggregated and globally cached in memory via `Flask-Caching` on application startup. This allows instantaneous querying and route-switching without triggering repeated I/O reads.

2. **Automated Asset Retrieval & Semantic Ambiguity**
   * **Problem**: Automatically sourcing player portraits across an 800+ player pool is notoriously difficult due to name abbreviations (e.g., "YS Chahal" vs "Yuzvendra Chahal") and the anti-bot protections of sports CDNs. Early iterations fetched incorrect celebrity or stock photos.
   * **Solution**: Engineered a robust, multi-stage retrieval pipeline. Player initials are semantically expanded to full names, queried against the **Wikimedia API** with a **scored Bing image-scraping fallback**, then verified with **OpenCV Haar-cascade face validation** (rejecting team photos and mismatched faces) before being persistently cached in `assets/images/players`.

3. **Achieving 60FPS Animations in a Python Framework**
   * **Problem**: Dash inherently uses React under the hood, but injecting heavy, scroll-triggered DOM animations entirely from a Python backend often results in severe stuttering and jittery component transitions.
   * **Solution**: Bypassed Dash's native callback-based animation limits by injecting **raw GSAP 3.12 (GreenSock)** and **Lenis Smooth Scroll** directly into the browser DOM (`assets/animations.js`). This offloads all cinematic scroll reveals, 3D tilts, and holographic foil calculations directly to the GPU.

4. **Dynamic Timelines & Season Handling**
   * **Problem**: Hardcoding dataset boundaries (e.g., stopping at 2024) breaks the UI when new seasons are added, leading to skewed calculations or missing dropdown options.
   * **Solution**: Architected a fully dynamic global configuration. The app dynamically polls the underlying Parquet files to detect the exact `min_season` and `max_season` (currently 2026), automatically adjusting UI labels to state `"2026 Live/Partial"` and recalculating all all-time metrics dynamically without requiring code updates.

---

## 🎯 Features

### 📊 Analytics Modules
| Module | Description |
|--------|-------------|
| **Overview** | Cinematic homepage with hero, season rewind timeline, KPI counters |
| **All-Time** | Historical leaderboard, milestone trackers, and ultimate legends |
| **Match Explorer** | Ball-by-ball scorecards, Manhattan, Worm, Fall of Wickets |
| **Head to Head** | Team rivalry analysis with margin distributions, season arcs |
| **Player Analysis** | FIFA-style profile cards, radar charts, performance meters |
| **Batter vs Bowler** | Matchup arena with outcome distributions, over-by-over profiling |
| **Team Intelligence** | Trophy cabinets, venue dominance, season performance trends |
| **Scorecard Cinema** | Immersive, full-screen playback of legendary match scorecards |
| **Analytics Lab** | Win probability curves, Impact Player scores, phase evolution |

### 🎨 Design System
- **Dark Cinema Theme** — void-to-surface gradient palette
- **Glassmorphism** — frosted-glass cards with 24px blur + saturation
- **Holographic Foil** — CSS `@property` animated gradient on player cards
- **GSAP Scroll Reveals** — directional, staggered, scale-up animations
- **Lenis Smooth Scroll** — butter-smooth inertia scrolling
- **3D Tilt** — perspective-based card interactions
- **Magnetic Buttons** — cursor-attracted micro-animations
- **Custom Cursor** — dot + trail system with hover states
- **Stadium Glow** — pulsing radial ambient light effects
- **Page Transitions** — blur + slide animation between routes

### ⚡ Impact Player Analytics (NEW)
- **Impact Score** — `avg(runs + wickets × 25)` per match appearance
- **Leaderboard** — Top 15 all-time impact players
- **Phase Strategy** — Team RPO comparison across Powerplay/Middle/Death
- **Win Probability** — Over-by-over chase success curves

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|-----------|
| **Framework** | Dash 2.14+ (multi-page architecture) |
| **Charting** | Plotly 5.18+ (dark-themed, interactive) |
| **Data** | Pandas + Parquet (compressed, fast I/O) |
| **Animations** | GSAP 3.12 + ScrollTrigger |
| **Scrolling** | Lenis smooth scroll |
| **Styling** | Custom CSS (2,500+ lines, design system v5) |
| **Server** | Flask (Dash WSGI) |
| **Caching** | Flask-Caching (SimpleCache) |
| **Deployment** | Docker / Procfile (any Python host) · GitHub Pages for the static project site |
| **Data Source** | [Cricsheet](https://cricsheet.org/) (2008–2026) |

---

## 🚀 Quick Start

```bash
# Clone
git clone https://github.com/YOUR_USERNAME/ipl-data-curation-and-visualization.git
cd ipl-data-curation-and-visualization

# Install dependencies
pip install -r requirements.txt

# Run
python app.py
```

Open **http://localhost:8050** in your browser.

---

## 📂 Project Structure

```
├── app.py                  # Main Dash application + layout
├── pages/
│   ├── overview.py         # Cinematic homepage + season rewind
│   ├── match_explorer.py   # Ball-by-ball match center
│   ├── head_to_head.py     # Team rivalry analytics
│   ├── players.py          # Player profiles + radar charts
│   ├── player_vs_player.py # Batter vs Bowler matchup arena
│   ├── teams.py            # Franchise intelligence
│   └── advanced.py         # Analytics lab + Impact Player
├── utils/
│   ├── analytics.py        # Statistical computation engine
│   ├── components.py       # UI component library (50+ components)
│   ├── constants.py        # Design tokens + team mappings
│   ├── data_loader.py      # Parquet data pipeline
│   └── player_images.py    # ESPNcricinfo image pipeline
├── assets/
│   ├── style.css           # Design system v5 (2,500+ lines)
│   ├── animations.js       # GSAP animation engine v5
│   └── particles.js        # Canvas particle system
├── data/processed/         # Parquet datasets (matches, deliveries, venues)
├── Dockerfile              # Containerization for Railway / Fly.io
├── Procfile                # gunicorn process definition (Render/Heroku-style hosts)
├── _config.yml             # Jekyll config for the GitHub Pages project site
├── .github/workflows/      # jekyll-gh-pages.yml — builds & deploys the Pages site
└── requirements.txt        # Python dependencies
```

---

## 🌍 Deployment Architecture & Challenges

Hosting a data-heavy Python Dash application poses unique infrastructural challenges. Here is a breakdown of the deployment hurdles we faced and how they were solved:

### 1. The Memory Constraint (Render & Railway)
* **The Problem:** Free-tier platforms like Render and Railway strictly cap RAM at ~500MB. Dash heavily relies on Pandas to process and filter data. Loading 290,000+ deliveries directly into memory instantly breached this threshold, triggering Out of Memory (OOM) crashes and silent deployment failures.
* **The Solution:** We bypassed heavy CSV loading by strictly utilizing tightly compressed **Parquet** binaries. This shrank the on-disk delivery dataset from **25.4 MB (CSV) to 1.27 MB (Parquet) — a ~95% reduction** — allowing the app to successfully boot on ultra-low-memory containers. (Note: We also fixed Railway's strict `$PORT` environment mapping by dynamically exposing the port in our `Dockerfile`).

## 📊 Data Pipeline

The platform uses a reproducible scraper-to-Parquet pipeline for fast startup:

1. **Ingest** — `utils/data_scraper.py` downloads and caches Cricsheet's `ipl_json.zip` (1,235 nested JSON match files)
2. **Parse & Normalize** — innings → overs → deliveries are flattened into `matches`, `deliveries`, and `impact_players` tables, with team renames resolved (e.g. *Kings XI Punjab → Punjab Kings*) and **Impact-Player substitution events** extracted from each delivery's `replacements` field
3. **Output** — Optimized Parquet files written to `data/processed/`
4. **Loading** — `utils/data_loader.py` reads Parquet once at startup, cached in-memory via `functools.lru_cache` + `Flask-Caching`

---

## 🎨 Design Philosophy

> *"Every pixel should feel like it belongs in a broadcast."*

The design draws from:
- **Apple Sports** — Clean typography, spacious layouts
- **Formula 1 App** — Dark cinema aesthetics, data-rich displays
- **FIFA Ultimate Team** — Holographic player cards with team colors
- **SofaScore** — Performance meters, form curves
- **Netflix** — Scroll-triggered content reveals

----

## 📜 License

MIT License. Data sourced from [Cricsheet](https://cricsheet.org/) under their terms.

----

<p align="center">
  <sub>Built with ❤️ and way too much cricket data.</sub>
</p>

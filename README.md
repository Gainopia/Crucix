<div align="center">

# Gainopia • Crucix

**Your own intelligence terminal. 27 sources. One command. Zero cloud.**

## [Visit The Live Site: crucix.live](https://www.crucix.live/)

[![Live Website](https://img.shields.io/badge/live-crucix.live-00d4ff?style=for-the-badge)](https://www.crucix.live/)
[![Open Demo](https://img.shields.io/badge/open-live%20dashboard-0b1220?style=for-the-badge&logo=googlechrome&logoColor=white)](https://www.crucix.live/)

[![Node.js 22+](https://img.shields.io/badge/node-22%2B-brightgreen)](#quick-start)
[![License: AGPL v3](https://img.shields.io/badge/license-AGPLv3-blue.svg)](LICENSE)
[![Dependencies](https://img.shields.io/badge/dependencies-1%20(express)-orange)](#architecture)
[![Sources](https://img.shields.io/badge/OSINT%20sources-27-cyan)](#data-sources-27)
[![Docker](https://img.shields.io/badge/docker-ready-blue?logo=docker)](#docker)

**Enter The Signal Network**

[![Signal Wire](https://img.shields.io/badge/Signal%20Wire-%40crucixmonitor-111111?style=for-the-badge&logo=x&logoColor=white)](https://x.com/crucixmonitor)
[![Ops Room](https://img.shields.io/badge/Ops%20Room-Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/ChVy7SF4)

![Crucix Dashboard](docs/dashboard.png)

<details>
<summary><b>🔍 View More Screenshots</b></summary>

| Boot Sequence | World Map |
|:---:|:---:|
| ![Boot](docs/boot.png) | ![Map](docs/map.png) |

| 3D Globe View |
|:---:|
| ![Globe](docs/globe.png) |

</details>

</div>

---

> **Live website:** [https://www.crucix.live/](https://www.crucix.live/)  
> Explore the public demo first, then clone the repo to run Crucix locally.

Crucix pulls satellite fire detection, flight tracking, radiation monitoring, satellite constellation tracking, economic indicators, live market prices, conflict data, sanctions lists, and social sentiment from **27 open-source intelligence feeds** — in parallel, every 15 minutes — and renders everything on a single self-contained Jarvis-style dashboard.

Hook it up to an LLM and it becomes a **two-way intelligence assistant** — pushing multi-tier alerts to Telegram and Discord when something meaningful changes, responding to commands like `/brief` and `/sweep` from your phone, and generating actionable trade ideas grounded in real cross-domain data. Your own private analyst that watches the world while you sleep.

No cloud. No telemetry. No subscriptions. Just `node server.mjs` and you're running.

---

## ⚠️ Token & Asset Warning

> [!WARNING]
> **Crucix has not launched any official token, coin, NFT, airdrop, presale, or other blockchain-based asset.**  
> Any digital asset using the Crucix name, logo, or branding is completely unrelated to and unauthorized by Crucix. Do not buy it, connect your wallet to claim it, or sign transactions based on third-party DMs or posts.

---

## Why This Exists

Most of the world's real-time intelligence — satellite imagery, radiation levels, conflict events, economic indicators, flight tracking, maritime activity — is publicly available. It's just scattered across dozens of government APIs, research institutions, and open data feeds that nobody has time to check individually.

Crucix brings it all into one place. Not behind a paywall, not locked in an enterprise platform, and not requiring a security clearance. Just open data, aggregated and cross-correlated locally, updated every 15 minutes.

---

## Quick Start

```bash
# 1. Clone the repo
git clone [https://github.com/calesthio/Crucix.git](https://github.com/calesthio/Crucix.git)
cd Crucix

# 2. Install dependencies (just Express)
npm install

# 3. Configure environment variables
cp .env.example .env

# 4. Start the dashboard
npm run dev
If npm run dev fails silently (exits with no output), run Node directly instead:Bashnode --trace-warnings server.mjs
This bypasses npm's script runner, which can suppress errors on certain systems (particularly PowerShell on Windows). You can also run node diag.mjs to check your Node version, test module imports, and verify port availability. See Troubleshooting for more.The dashboard opens automatically at http://localhost:3117 and immediately begins its first intelligence sweep (taking 30–60 seconds). After that, it auto-refreshes every 15 minutes via SSE (Server-Sent Events).Requirements: Node.js 22+ (uses native fetch, top-level await, ESM)Docker DeploymentBashgit clone [https://github.com/calesthio/Crucix.git](https://github.com/calesthio/Crucix.git)
cd Crucix
cp .env.example .env    # add your API keys
docker compose up -d
Dashboard available at http://localhost:3117. Sweep data persists in ./runs/ via volume mount.What You Get🎛️ Live DashboardA self-contained Jarvis-style HUD featuring:3D WebGL Globe (Globe.gl) with atmosphere glow, star field, and smooth rotation (plus a classic flat map toggle).9 Marker Types: Fire detections, air traffic, radiation sites, maritime chokepoints, SDR receivers, OSINT events, health alerts, geolocated news, and conflict events.Animated 3D Flight Corridors and region filters (World, Americas, Europe, Middle East, Asia Pacific, Africa).Live Financials & Risk Gauges: Indexes, crypto, energy, commodities via Yahoo Finance, VIX, high-yield spreads, and supply chain pressure.Real-time Feeds: Curated OSINT Telegram posts, news ticker, sweep delta change tracking, and nuclear/space watches.⚡ Performance Modes (VISUALS FULL / VISUALS LITE)The top-bar toggle adjusts rendering behavior without sacrificing data coverage or sweep frequency:VISUALS LITE: Disables heavy background overlays, scanlines, backdrop blurs, globe auto-rotation, and continuous marquee animations, converting feeds into clean scrollable lists. Automatically applied on mobile devices.🤖 Two-Way Bot IntegrationTelegram: Commands like /status, /sweep, /brief, /portfolio, /alerts, and /mute.Discord: Slash commands, rich color-coded embeds (FLASH/PRIORITY/ROUTINE), and zero-dependency webhook support.API Keys SetupCopy .env.example to .env at the root. Core economic and satellite data require three free keys:KeySourceHow to GetFRED_API_KEYFederal Reserve Economic Datafred.stlouisfed.orgFIRMS_MAP_KEYNASA FIRMS (Satellite Fires)NASA FIRMSEIA_API_KEYUS Energy Information AdminEIA Open Data(Optional keys for ACLED, AISStream, ADS-B Exchange, LLM providers, and bots are fully documented in .env.example). Crucix works with zero API keys out of the box; unconfigured sources gracefully return structured errors while the rest of the sweep completes successfully.ArchitecturePlaintextcrucix/
├── server.mjs                 # Express dev server & SSE orchestrator
├── crucix.config.mjs          # Configuration & delta thresholds
├── apis/
│   ├── briefing.mjs           # Master orchestrator (27 parallel feeds)
│   └── sources/               # 27 modular source integrations
├── dashboard/
│   └── public/jarvis.html     # Self-contained Jarvis HUD
├── lib/
│   ├── llm/                   # 8 LLM provider abstractions (pure fetch)
│   ├── delta/                 # Cross-sweep change tracking & memory
│   └── alerts/                # Telegram & Discord bot handlers
└── runs/                      # Runtime data & daily archives
Troubleshootingnpm run dev exits silently: Use node --trace-warnings server.mjs or node diag.mjs to view direct stack traces.Port 3117 in use: Kill existing background processes (taskkill /F /IM node.exe on Windows or lsof -ti:3117 | xargs kill on Unix) or change PORT in your .env.Empty panels on first load: Normal behavior while the initial 30–60 second parallel source sweep completes.Contact & ContributingContact: celesthioailabs@gmail.comIssues / Contributions: Please open a GitHub issue or pull request. Review CONTRIBUTING.md for guidelines.LicenseAGPL-3.0

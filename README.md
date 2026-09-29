# SyncFit Presentation

Academic defense and demo material for **SyncFit Edge**, built with Slidev
(TypeScript + Vue). Everything here supports the oral defense of the project.

## Purpose

Communicate the project clearly to an evaluation panel: the problem, the dual
physiology, the architecture, the two-AI routine flow, the data structures, the
impact and the references — plus interactive diagrams.

## Contents

```
syncfit-presentation/
├── slides.md               # Slidev deck (narrative + embedded diagrams)
├── public/
│   ├── flow.html           # 2D flow: two AIs (hardware -> core -> DeepSeek -> validator)
│   ├── architecture.html   # 3D interactive flow (three.js; drag/zoom)
│   └── journey.html        # User journey as 7 small "stations"
├── notes/                  # Speaker script (see notes/README.md)
├── components/             # Custom slides/diagrams (empty scaffold)
└── package.json
```

## Run

```bash
npm i
npm run dev        # opens the deck; diagrams served at /flow.html, /architecture.html, /journey.html
npm run export     # PDF export (needs a browser)
```

Open a diagram directly (no server) with e.g.:
```bash
xdg-open public/flow.html
xdg-open public/journey.html
# architecture.html needs internet (three.js CDN)
xdg-open public/architecture.html
```

## Diagrams

- **flow.html** — the two-AI pipeline: hardware → local model (assessment +
  `k_load`) → DeepSeek designs → deterministic validation → backend → UI.
- **architecture.html** — the same flow in interactive 3D (nodes, animated
  connections, orbit/zoom), including the gym-equipment input.
- **journey.html** — a **3D animated** walkthrough (Spanish) with low-poly
  characters across **9 stations**, showing **both AIs** (local `core` and
  DeepSeek) and the **data entering/leaving each stage** (inputs/outputs panel):
  1. Super admin · 2. Gym admin surveys equipment · 3. Athlete registers/onboards
  · 4. Joins the gym by code · 5. Hardware scan (raw PPG/°T/force) · 6. **IA #1
  local (core)**: DSP + RandomForest → RMSSD/fatigue/`k_load` + assessment ·
  7. **IA #2 DeepSeek**: designs the routine from assessment + profile + catalog +
  equipment · 8. Deterministic validator · 9. Trains/tracks/shares. Camera
  auto-tours the stations (drag to orbit).
  1. Super admin creates the gym admin.
  2. Gym admin creates the gym and surveys equipment.
  3. Athlete registers (cedula) and onboards.
  4. Athlete joins the gym by code.
  5. Hardware scan → local model.
  6. DeepSeek designs + deterministic validation.
  7. Trains, tracks and shares.

## Narrative outline (slides.md)

1. Problem: male-based models ignore female endocrine states.
2. Dual physiology: menstrual cycle and pregnancy by trimester.
3. Architecture: hardware, core, DeepSeek, backend, frontend.
4. Routine flow (two AIs) and 3D architecture.
5. User journey (stations).
6. Data structures and hybrid-AI rules.
7. Impact: social, cultural, economic, normative.
8. Roles and administration.
9. References (APA 7th).

## Speaker notes

Per-slide script lives in `notes/README.md`; slide-level notes are also inline in
`slides.md` as HTML comments.

## What does NOT belong here

- Production or runtime code.

## Related repositories

[`syncfit-hardware`](../syncfit-hardware) · [`syncfit-core`](../syncfit-core) ·
[`syncfit-ai-reasoning`](../syncfit-ai-reasoning) · [`syncfit-backend`](../syncfit-backend) ·
[`syncfit-frontend`](../syncfit-frontend) · [`syncfit-contracts`](../syncfit-contracts).

All code, comments, documentation and commits in this repository are written in English.

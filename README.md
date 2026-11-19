# SyncFit Presentation

**Live app:** https://syncfit.jenilarper.dev

Academic defense and demo material for **SyncFit Edge**, built with Slidev
(TypeScript + Vue). Everything here supports the oral defense of the project.

## 15-minute pitch

Open [the public SyncFit pitch on Vercel](https://syncfit-presentation-juan-5a09.vercel.app/) in your browser.
It includes five minutes on the problem and ten minutes for the live demo.

A Beamer (LaTeX) version in the SyncFit brand style, with the same script, is in
[`beamer/syncfit-pitch.pdf`](./beamer/syncfit-pitch.pdf) (see [`beamer/README.md`](./beamer/README.md)).
It has 11 slides: slides 1–5 cover the 5-minute presentation and slides 6–9 the
10-minute demo, followed by why SyncFit and questions. Present it in Adobe Acrobat
so the transitions and animations play.

## Architecture

See [`ARCHITECTURE.md`](./ARCHITECTURE.md) for the software architecture
(style, layers, patterns, deployment, hybrid AI).

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
  `k_load`) → DeepSeek (GPT-6 Luna outage backup) designs → deterministic validation → backend → UI.
- **architecture.html** — the same flow in interactive 3D (nodes, animated
  connections, orbit/zoom), including the gym-equipment input.
- **journey.html** — a **3D animated** walkthrough (Spanish) with low-poly
  characters across **9 stations**, showing **both AIs** (local `core` and
  DeepSeek (with GPT-6 Luna backup) and the **data entering/leaving each stage** (inputs/outputs panel):
  1. Super admin · 2. Gym admin surveys equipment · 3. Athlete registers/onboards
  · 4. Joins the gym by code · 5. Hardware scan (raw PPG/°T/force) · 6. **IA #1
  local (core)**: DSP + RandomForest → RMSSD/fatigue/`k_load` + assessment ·
  7. **IA #2 DeepSeek / GPT-6 Luna**: designs the routine from assessment + profile + catalog +
  equipment · 8. Deterministic validator · 9. Trains/tracks/shares. Camera
  auto-tours the stations (drag to orbit).
  1. Super admin creates the gym admin.
  2. Gym admin creates the gym and surveys equipment.
  3. Athlete registers (cedula) and onboards.
  4. Athlete joins the gym by code.
  5. Hardware scan → local model.
  6. DeepSeek (GPT-6 Luna backup) designs + deterministic validation.
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

## Handoff for the team

**Role.** Defense deck (Slidev) + interactive diagrams.

**Run.** `npm i && npm run dev`; diagrams at `/flow.html`, `/architecture.html`,
`/journey.html` (or open `public/*.html` directly; the 3D ones need internet for
the three.js CDN).

**Contents.** `slides.md` (narrative), `public/flow.html` (2D two-AI pipeline),
`public/architecture.html` (3D interactive), `public/journey.html` (3D animated,
Spanish, 9 stations with per-stage inputs/outputs), `notes/README.md` (speaker
script). User-story backlog lives as GitHub issues in this repo.

## Roadmap · Qué falta (español)

> Estado: **para la presentación final · primera versión** (aún no implementado del todo).

- `components/` vacío; falta pulir el deck y los assets.
- **Primera versión**: faltan muchos ajustes — **login con Google**, arreglar el **compartir datos**, **enlazar el hardware**, y **errores que se vayan viendo**.
- Convertir el backlog de historias de usuario (issues) en entregables.

## Conoce a Pulsi

<img src="public/pulsi.png" alt="Pulsi, la gotita guía de SyncFit Edge" width="130" align="left" style="margin-right:16px" />

**¡Hola! Soy Pulsi, tu guía en SyncFit Edge.** Acompaño a la usuaria en todo el
recorrido: me pongo feliz, cansada o alerta según su energía, su fase del ciclo y
las señales del hardware. Represento el latido del sistema y hago cercana una
tecnología que, por dentro, es muy seria.

<br clear="left" />

### El sistema en 20 segundos

SyncFit Edge es un sistema **edge-IoT + IA predictiva** que adapta el
entrenamiento femenino al **ciclo menstrual** y al **embarazo**, y previene
lesiones. Funciona con **dos IAs que trabajan en cadena**:

1. **IA local** (`syncfit-core`, determinista): toma los datos del hardware
   (PPG, temperatura dérmica, fuerza isométrica), calcula biomarcadores y
   produce el factor de carga **`k_load`**.
2. **IA de nube** (DeepSeek vía OpenCode, GPT-6 Luna ante fallos transitorios):
   **diseña la rutina** a partir de esa evaluación, el perfil, la meta y las
   **máquinas/equipo del gimnasio**.
3. Una capa **determinista valida** (patrones, seguridad, sin duplicados,
   máquinas primero) y hace **eco de `k_load`** (la IA nunca lo recalcula).

Todo se despliega en **AWS** (S3 + CloudFront, ECS + ALB) y está en línea en
**https://syncfit.jenilarper.dev**.

> ⚠️ **Primera versión.** Faltan muchos ajustes: **login con Google**, arreglar el
> **compartir datos**, **enlazar el hardware** y los **errores que se vayan viendo**.

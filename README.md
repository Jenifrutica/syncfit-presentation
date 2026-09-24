# SyncFit Presentation

Academic defense and demo material for SyncFit Edge, built with Slidev (TypeScript).

## Purpose

Communicate the project clearly to an evaluation panel: the problem, the dual physiology, the architecture, the data structures, the hybrid AI design, the impact and the references.

## What belongs here

- `slides.md` — the Slidev deck.
- `components/` — custom slides and diagrams.
- `public/` — images, architecture diagrams and demo assets.
- `notes/` — speaker notes and script.
- Reused metrics and figures produced by the other repositories.

## Narrative outline

1. Problem: male-based training models ignore female endocrine states.
2. Physiology: menstrual cycle and pregnancy by trimester.
3. Architecture: hardware, core, reasoning, backend, frontend.
4. Data structures: Ring Buffer, Segment Tree, Max-Heap, Directed State Graph.
5. Hybrid AI: deterministic `k_load` plus cloud biomechanical audit.
6. Impact: social, cultural, economic and normative.
7. References (APA 7th edition).

## What does NOT belong here

- Any production or runtime code.

## Suggested structure

```
syncfit-presentation/
├── slides.md
├── components/
├── public/
├── notes/
├── package.json
└── README.md
```

## Stack

TypeScript, Slidev, Vue.

## Tasks

> **Language: TypeScript (Slidev).**

### Requirements

- [ ] Scaffold the Slidev project.
- [ ] Write the narrative sections in `slides.md`.
- [ ] Add architecture diagrams (hardware, core, reasoning, backend, frontend).
- [ ] Add the data structures section (Ring Buffer, Segment Tree, Max-Heap, Directed State Graph).
- [ ] Add the hybrid AI section (deterministic `k_load` plus cloud audit).
- [ ] Add the impact section (social, cultural, economic, normative).
- [ ] Add the references in APA 7th edition.
- [ ] Write speaker notes and the presentation script.
- [ ] Collect demo assets produced by the other repositories.
- [ ] Rehearse and time the deck for the defense.

## Related repositories

- [`syncfit-hardware`](../syncfit-hardware)
- [`syncfit-core`](../syncfit-core)
- [`syncfit-ai-reasoning`](../syncfit-ai-reasoning)
- [`syncfit-backend`](../syncfit-backend)
- [`syncfit-frontend`](../syncfit-frontend)

All code, comments, documentation and commits in this repository are written in English.

## Context for a new session

**What it is.** Academic defense deck (Slidev, TypeScript) plus the product
backlog of user stories as GitHub **issues** in this repo.

**Layout.** `slides.md`, `components/`, `public/`, `notes/`.

**Backlog.** ~25 US (US-01..US-25). Labels: `user-story`, `epic:*`
(hardware/core/ai/backend/frontend/data/security/infra), `prio:urgente|alta|media|baja`.
Highlights: **US-21 Rutinas más personalizadas (URGENTE)**, US-22 verificar
estructuras, US-18 animaciones, US-19 frontend, US-20 backend, US-23 hardware,
US-24 AWS, US-25 PWA/notificaciones.

**Run.** `npm i && npm run dev` (Slidev). `npm run export` to PDF.

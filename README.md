# SyncFit Presentation

**Live app:** https://syncfit.jenilarper.dev

Defense and demo material for **SyncFit Edge**: the pitch slides, interactive
diagrams and the speaker script.

## Team

- Juan Esteban Cuaran
- Juan Camilo López
- Jenifer Daniela Urbano

## Present

| What | Where | Notes |
|---|---|---|
| **Pitch (Beamer PDF)** — main deck | [`beamer/syncfit-pitch.pdf`](./beamer/syncfit-pitch.pdf) | 11 slides / 24 pages. Open in Adobe Acrobat, full screen (Ctrl/Cmd+L), allow the document's JavaScript for the animations. |
| Pitch (web) | [`public/SyncFit-Pitch.html`](./public/SyncFit-Pitch.html) · [online](https://syncfit-presentation-juan-5a09.vercel.app/) | Same script, opens in any browser. |
| Live demo | https://syncfit.jenilarper.dev | Slides 6–9. |

Timing: slides 1–5 are the 5-minute presentation, slides 6–9 the 10-minute live
demo, then why SyncFit and questions. Checklist and build steps:
[`beamer/README.md`](./beamer/README.md).

### Before presenting

- Acrobat with document JavaScript allowed; start full screen on the cover.
- For the demo, three browser sessions: gym admin, athlete with the gym code,
  and superadmin in Catalogs.
- Prototype plugged in (it zeroes the force platform by itself when it connects);
  without it, the check-in's "Simulate" uses the athlete's own history or the
  values expected for her age, weight and height.

## Diagrams

Open directly in a browser (`xdg-open public/<file>`):

- `flow.html` — the two-AI pipeline: hardware → local model (`k_load`) → cloud
  AI designs the routine → deterministic validation → app.
- `architecture.html` — the same flow in interactive 3D (needs internet for three.js).
- `journey.html` — 3D walkthrough of the user journey in 9 stations.

## Contents

```
syncfit-presentation/
├── beamer/          # Main deck: syncfit-pitch.tex + brand theme, built PDF, fonts, images
├── public/          # Web pitch, diagrams and pitch images
├── notes/           # Speaker script
├── slides.md        # Earlier Slidev deck (npm i && npm run dev)
└── ARCHITECTURE.md  # Software architecture (layers, patterns, deployment, hybrid AI)
```

## Rebuild the PDF

```bash
cd beamer
xelatex syncfit-pitch.tex && xelatex syncfit-pitch.tex
```

## Meet Pulsi

<img src="public/pulsi.png" alt="Pulsi, the SyncFit Edge guide" width="110" align="left" style="margin-right:16px" />

Pulsi is the SyncFit guide: a heart-shaped drop whose face mirrors the athlete's
state (happy, tired, alert, asleep) according to her energy, her cycle phase or
pregnancy week, and the sensor readings.

<br clear="left" />

## Related repositories

[`syncfit-frontend`](https://github.com/Jenifrutica/syncfit-frontend) ·
[`syncfit-backend`](https://github.com/Jenifrutica/syncfit-backend) ·
[`syncfit-contracts`](https://github.com/Jenifrutica/syncfit-contracts) ·
[`syncfit-core`](https://github.com/Jenifrutica/syncfit-core) ·
[`syncfit-database`](https://github.com/Jenifrutica/syncfit-database) ·
[`syncfit-ai-reasoning`](https://github.com/Jenifrutica/syncfit-ai-reasoning) ·
[`syncfit-simulator`](https://github.com/Jenifrutica/syncfit-simulator) ·
[`syncfit-hardware`](https://github.com/Jenifrutica/syncfit-hardware)

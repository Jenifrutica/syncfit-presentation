# SyncFit Presentation

**Live app:** https://syncfit.jenilarper.dev

Defense and demo material for **SyncFit Edge**: a short pitch deck (the idea and
the data structures), the speaker script for the three of us, and the live demo.

## Team

- Juan Esteban Cuaran
- Juan Camilo López
- Jenifer Daniela Urbano

## Present

| What | Where | Notes |
|---|---|---|
| **Pitch (Beamer PDF)** — main deck | [`beamer/syncfit-pitch.pdf`](./beamer/syncfit-pitch.pdf) | 8 slides, one page each. Open in Adobe Acrobat, full screen (Ctrl/Cmd+L), allow the document's JavaScript for the animations. |
| **Script** | [`beamer/GUION.md`](./beamer/GUION.md) | What each of us says per slide, who drives each part of the demo, likely questions. |
| Pitch (web) | [`public/SyncFit-Pitch.html`](./public/SyncFit-Pitch.html) · [online](https://syncfit-presentation-juan-5a09.vercel.app/) | Same script, opens in any browser. |
| Live demo | https://syncfit.jenilarper.dev | Shown in the app, without slides, after slide 7. |

Order: slides 1–7 (the idea, how the backend is built and the data structures it
uses, about 4.5 minutes), then the live demo in the app, then slide 8 for
questions. Checklist and build steps: [`beamer/README.md`](./beamer/README.md).

### Before presenting

- Acrobat with document JavaScript allowed; start full screen on the cover.
- For the demo, three browser sessions: gym admin, athlete with the gym code,
  and superadmin in Catalogs.
- Prototype plugged in (it zeroes the force platform by itself when it connects);
  without it, the check-in's "Simulate" uses the athlete's own history or the
  values expected for her age, weight and height.

## Contents

```
syncfit-presentation/
├── beamer/          # Main deck: syncfit-pitch.tex + brand theme, built PDF, fonts, Pulsi, GUION.md
├── public/          # Web pitch (SyncFit-Pitch.html), its photos and Pulsi
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

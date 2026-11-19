# SyncFit Presentation

Defense and demo material for **SyncFit Edge**: the deck the team presents and
the script for each speaker. No production code lives here.

## The presentation (5 min + 10 min of live demo)

- **Deck:** [`beamer/syncfit-pitch.pdf`](./beamer/syncfit-pitch.pdf), LaTeX Beamer
  in the SyncFit brand style. Present it in Adobe Acrobat, full screen, so the
  transitions and animations play. How to build and present it:
  [`beamer/README.md`](./beamer/README.md).
- **Script:** [`beamer/GUION.md`](./beamer/GUION.md) — what Juan López, Jenifer
  Urbano and Juan Cuarán say on each slide, with times and hand-offs.
- **Web version:** [the public pitch on Vercel](https://syncfit-presentation-juan-5a09.vercel.app/),
  a single page (`public/SyncFit-Pitch.html` with `public/pitch-assets/`).

## Contents

```
beamer/                 # The deck: .tex, brand theme, fonts (OFL), Pulsi, PDF, script
public/
├── SyncFit-Pitch.html  # Web version of the pitch (Vercel)
├── pitch-assets/       # Its photos
└── pulsi.png           # Pulsi, used below
ARCHITECTURE.md         # Software architecture (layers, patterns, deployment, AI)
```

## Architecture

See [`ARCHITECTURE.md`](./ARCHITECTURE.md) for the software architecture
(style, layers, patterns, deployment, hybrid AI). The deck summarizes the
backend and its data structures in the "Cómo está construido" slides.

## Related repositories

[`syncfit-hardware`](../syncfit-hardware) · [`syncfit-core`](../syncfit-core) ·
[`syncfit-ai-reasoning`](../syncfit-ai-reasoning) · [`syncfit-backend`](../syncfit-backend) ·
[`syncfit-frontend`](../syncfit-frontend) · [`syncfit-contracts`](../syncfit-contracts).

All code, comments, documentation and commits in this repository are written in English;
the deck and the script are in Spanish, the language of the defense.

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

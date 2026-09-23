---
theme: default
title: SyncFit Edge
info: |
  Edge-IoT system and predictive biomechanical inference engine for adaptive
  female training prescription (menstrual cycle and pregnancy) and injury
  prevention.
class: text-center
highlighter: shiki
drawings:
  persist: false
mdc: true
---

# SyncFit Edge

Edge-IoT + predictive biomechanical inference for adaptive female training

<div class="pt-12 opacity-70">
Technical & methodological defense
</div>

<!--
Speaker notes: welcome, one-line pitch, and the goal of the session.
-->

---

# Problem

- Training prescription models are based almost exclusively on male cohorts.
- Female endocrine states are ignored: cycle phases and pregnancy trimesters.
- Consequences: elevated ACL/tendon risk (3-8x in the ovulatory window),
  overtraining, pelvic floor and venous-return complications.

<!--
Speaker notes: cite Hewett, Wojtys, ACOG, Sims.
-->

---

# Dual physiology

| Menstrual cycle | Pregnancy (by trimester) |
|-----------------|--------------------------|
| Menstrual / follicular / ovulatory / luteal | T1 / T2 / T3 |
| Estrogen + relaxin peaks -> ligament laxity | Hyperlaxity, displaced center of gravity |
| Luteal: higher basal temperature, lower HRV | Avoid supine decubitus >= week 16, Valsalva |

---

# Architecture

- **Hardware / firmware** (C++/ESP-IDF): ESP32, MAX30102, MLX90614, HX711.
- **Core** (Python): DSP, trained fatigue model, deterministic `k_load`.
- **Reasoning** (Python): DeepSeek biomechanical audit in strict JSON.
- **Backend** (Python/FastAPI): REST + WebSockets, mandatory data structures.
- **Frontend** (TypeScript/Next.js): real-time analytics and adaptive routine.
- **Simulator** replaces the hardware while real captures are recorded.

---

# Data structures

| Structure | Complexity | Where |
|-----------|:----------:|-------|
| Ring Buffer | O(1) | hardware (C++), core, backend |
| Segment Tree | O(log n) | backend |
| Priority Queue / Max-Heap | O(1) | backend |
| Directed State Graph | traversal | backend, core |

---

# Hybrid AI

1. **Deterministic half** (`syncfit-core`): DSP + Random Forest -> `k_load`.
2. **Generative half** (`syncfit-ai-reasoning`): DeepSeek audits and structures.

The model **never** recomputes `k_load`; a deterministic rule engine preserves it
and enforces the biomechanical blocks.

---

# Impact

- **Social:** scientific prescription for fertile and maternity stages.
- **Cultural:** removes taboos around training during the cycle and pregnancy.
- **Economic:** fewer orthopedic surgeries and postpartum dysfunctions.
- **Normative:** aligned with SDG 3 and 5 and biomedical data protection.

---

# References (APA 7th)

- Hewett, Zazulak & Myer (2007)
- Wojtys et al. (1998)
- ACOG (2020)
- Mottola et al. (2018)
- Sims & Yeager (2016)

<div class="pt-8 opacity-70">Thank you — questions</div>

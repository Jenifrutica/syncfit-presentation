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
- **Core — local AI** (Python): DSP, trained fatigue model, deterministic `k_load`.
- **Reasoning — DeepSeek** (OpenCode Go), with GPT-6 Luna on transient outages: designs the routine in strict JSON.
- **Backend** (Python/FastAPI): REST + WebSockets, mandatory data structures.
- **Frontend** (TypeScript/Next.js): real-time analytics and adaptive routine.
- **Simulator** replaces the hardware while real captures are recorded.

---

# Routine flow (two AIs)

<iframe src="/flow.html" class="w-full h-[430px] rounded-xl border border-pink-200" />

<!--
Speaker notes: hardware -> local model (assessment + k_load) -> DeepSeek designs
(GPT-6 Luna backup for transient outages; patterns, exercises, dose, rationale)
-> deterministic enforcement -> backend -> UI.
The model never recomputes k_load.
-->

---

# Architecture (3D)

<iframe src="/architecture.html" class="w-full h-[440px] rounded-xl border border-pink-200" />

<!-- Speaker notes: interactive 3D flow; drag/zoom. Hardware -> local model -> assessment -> DeepSeek (GPT-6 Luna backup) -> validator -> backend/frontend, with the gym equipment feeding the designer. -->

---

# User journey (3D · stations)

<iframe src="/journey.html" class="w-full h-[480px] rounded-xl border border-pink-200" />

<!-- Speaker notes: 9 stations - super admin; gym admin surveys equipment; athlete registers/onboards; joins by code; hardware scan; IA #1 local core (assessment + k_load); IA #2 DeepSeek with GPT-6 Luna backup; deterministic validator; trains/tracks/shares. Each station shows its input/output data. -->

---

# Data structures

| Structure | Complexity | Where |
|-----------|:----------:|-------|
| Ring Buffer | O(1) | hardware (C++), core, backend |
| Segment Tree | O(log n) | backend |
| Priority Queue / Max-Heap | O(1) | backend |
| Directed State Graph | traversal | backend, core |

---

# Hybrid AI (two AIs)

1. **Local AI** (`syncfit-core`): DSP + Random Forest → biomarkers + deterministic `k_load`.
2. **Cloud AI** (`syncfit-ai-reasoning`): **DeepSeek (GPT-6 Luna backup) designs the whole routine** from the
   assessment, the profile, the gym machines and evidence guidelines.

A deterministic layer **never designs**: it validates and repairs — pattern coverage,
no repeated pattern, compounds first, contraindications, machine-first — and **echoes
`k_load`** (the model never recomputes it).

Evidence: Schoenfeld (2017, 2021), Baz-Valle (2022), Currier (2023), Contreras (2016),
Plotkin (2023); safety from ACOG (2020), Hewett (2007), Wojtys (1998), Maniar (2022).

---

# Impact

- **Social:** scientific prescription for fertile and maternity stages.
- **Cultural:** removes taboos around training during the cycle and pregnancy.
- **Economic:** fewer orthopedic surgeries and postpartum dysfunctions.
- **Normative:** aligned with SDG 3 and 5 and biomedical data protection.

---

# Roles and administration

- **Super admin**: purely administrative — users/profiles CRUD (activate,
  deactivate, reset password, change role, delete). Cannot create gyms/machines.
- **Gym admin**: creates gyms and registers **equipment** (machines and free
  equipment: dumbbells, barbell, Smith, benches), each with photo and weight factor.
- **Athlete**: joins a gym by code; routines are filtered by the gym's equipment.

---

# References (APA 7th)

- Hewett, Zazulak & Myer (2007)
- Wojtys et al. (1998)
- ACOG (2020)
- Mottola et al. (2018)
- Sims & Yeager (2016)

<div class="pt-8 opacity-70">Thank you — questions</div>

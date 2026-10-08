# Speaker notes & script

Script for the oral defense. Times assume a ~10-minute talk. Slide-level notes
are also inline in `slides.md` as HTML comments.

## 1 · Title (~20 s)
One line: "SyncFit Edge is an edge-IoT + predictive biomechanical system that
adapts female strength training to the menstrual cycle and pregnancy, and
prevents injury."

## 2 · Problem (~50 s)
Training models are built on male cohorts; female endocrine states are ignored.
In the ovulatory window, ligament laxity raises ACL/tendon risk (3–8×); late
luteal raises basal temperature and lowers HRV → overtraining. Cite Hewett
(2007), Wojtys (1998), ACOG (2020), Sims (2016).

## 3 · Dual physiology (~50 s)
Walk the table: cycle phases vs trimesters; what changes (laxity, temperature,
HRV, supine/Valsalva constraints) and why prescription must adapt.

## 4 · Architecture (~50 s)
Hardware/firmware → core (DSP + RF/XGBoost, deterministic `k_load`) → DeepSeek
(GPT-6 Luna backup on transient failures) → backend (FastAPI, data structures) → frontend. The simulator
replaces hardware until the device is built.

## 5 · Routine flow (two AIs) — `flow.html` (~60 s)
"The local model synthesizes the hardware into an assessment; DeepSeek (GPT-6 Luna
backup on transient failures) designs the routine from that data, the profile, the goal and the gym's equipment; a
deterministic layer validates and repairs — it never invents `k_load`."

## 6 · Architecture (3D) — `architecture.html` (~40 s)
Drag to orbit. Point out the equipment input feeding the designer.

## 7 · User journey (stations) — `journey.html` (~70 s)
Seven stations: super admin creates the gym admin; the gym admin surveys
equipment; the athlete registers (cedula) and onboards; joins by code; hardware
scan → local model; DeepSeek / GPT-6 Luna designs + validation; she trains, tracks and shares.

## 8 · Data structures & hybrid AI (~60 s)
Ring Buffer (fixed 100 Hz stream), Segment Tree (range queries), Max-Heap
(alerts), Directed State Graph (phases/trimesters), plus hashmaps/sets in the
routine engine. `k_load` is deterministic; the generative model only reasons on top of it.

## 9 · Impact (~40 s)
Social, cultural, economic, normative (SDG 3 & 5; biomedical data protection).

## 10 · Roles & administration (~30 s)
Super admin (administrative CRUD) vs gym admin (gyms + equipment) vs athlete.

## 11 · References & questions (~30 s)
APA 7th list; invite questions.

# SyncFit Edge — Software Architecture

This document describes the **software architecture** of SyncFit Edge: its
architectural style, layers, patterns, deployment topology and the hybrid-AI
design. It complements the visual diagrams in `public/` (2D flow, 3D
architecture, 3D user journey).

## Style in one line

**Modular monolith + shared libraries**, built with a **layered architecture**,
a **stage-by-stage pipeline (orchestration)** and a **contract-first** design,
with a **hybrid (deterministic + generative) AI** guarded by deterministic
validation. It is **not** a microservices architecture.

## Why not microservices

Only **two executables** are deployed — the backend (one FastAPI app) and the
frontend (Next.js) — plus PostgreSQL. `contracts`, `core`, `ai-reasoning`,
`simulator` and `database` are **libraries** installed into the backend, not
independently running services. There is no API gateway, service mesh or message
broker. The backend is internally modular, so it could be split later
(natural seams: `capture/telemetry` and `reasoning`), but today it is a single
deployable unit.

## Layered architecture (backend)

```
Presentation      app/api/* , app/ws/*         routers, request validation, auth
Application       app/services/*               use cases, system rules
Integration       syncfit-core / syncfit-ai / syncfit-simulator   ports & adapters
Data              syncfit-database             models, sessions, Unit of Work
Contracts         syncfit-contracts            shared models / validation
```

Each layer only depends on the layer below it. `syncfit-contracts` is the
**single source of truth** for every payload crossing a boundary: Pydantic
(`extra="forbid"`), Zod and JSON Schema enforce the same shapes.

## Pipeline / orchestration (routine)

```
hardware (or simulator)
   → syncfit-core (IA #1, deterministic): DSP + RandomForest/XGBoost → k_load
   → PhysiologicalAssessment
   → DeepSeek (IA #2, OpenCode Go): designs the routine (patterns, dose, rationale)
   → GPT-6 Luna (Responses API) on transient provider/network failures
   → deterministic routine if both generative calls fail
   → deterministic enforcement: patterns, safety, equipment order, k_load echo
   → persistence → REST/WebSocket → frontend
```

The backend orchestrates the stages. The generative stage may vary the *how*; the
deterministic stage guarantees the *what*.

## Software patterns used

- **Repository + Unit of Work** — `syncfit-database` with `Database.session_scope()`
  (commit/rollback per unit of work).
- **Ports & Adapters (hexagonal, partial)** — `ReasoningClient` protocol with
  `FakeClient` / `OpenCodeGoClient` adapters (dependency inversion); `core`'s
  `contracts_adapter` decouples it from the contract package.
- **Facade** — `SyncFitEngine` (core) and the `services/*` functions expose a
  simple API over complex internals.
- **Strategy / Policy** — routine engine selectable
  (`BACKEND_ROUTINE_ENGINE=ai|deterministic`) and model backend
  (`RandomForest|XGBoost`).
- **Catalog / Registry** — exercises, machines, supplements and symptoms as
  data-driven catalogs with loaders.
- **Contract-first / shared schema** — interfaces defined once and reused.

## Hybrid AI architecture

- **Deterministic half** (`syncfit-core`): DSP + trained ML → central fatigue and
  `k_load`. Never hallucinated; runs offline.
- **Generative half** (`syncfit-ai-reasoning`): DeepSeek reasons from the
  assessment, profile, goal, catalog and gym equipment to design the routine;
  GPT-6 Luna is attempted on transient DeepSeek/provider failures.
- **Deterministic guardrails** (`enforce_prescription`): normalize ids, exclude
  contraindications, no duplicate pattern, required-pattern coverage, compounds
  first, equipment filters, and a literal echo of `k_load`.

This is the *LLM-as-reasoner with deterministic enforcement* pattern.

## Deployment topology

```
[Sensor / Simulator]  ⇄  HTTP/WebSocket
        │
   [Backend · FastAPI] ──── [PostgreSQL]
        │  REST + WebSocket
   [Frontend · Next.js]
```

Client–server, REST + WebSocket, stateless backend that scales horizontally.
`syncfit-infra` (Docker/AWS) is currently scaffolding.

## Data structures (mandatory + extended)

- **Mandatory:** Ring Buffer (100 Hz stream), Time-Series Segment Tree (range
  queries), Priority Queue / Max-Heap (alerts), Directed State Graph
  (phases/trimesters).
- **Extended in the routine engine:** hash maps (`exercise_id → gym station`),
  sets (preferred/available equipment, movement families), grouping
  `defaultdict`, LRU cache (reasoning results).

## Repository responsibilities

| Repo | Architectural role |
|---|---|
| `syncfit-contracts` | Shared interfaces (schemas, models, catalogs). |
| `syncfit-core` | Local AI library (DSP + ML + `k_load` + state graph). |
| `syncfit-ai-reasoning` | Cloud AI library (DeepSeek client, planner, enforcement). |
| `syncfit-simulator` | Hardware substitute library (telemetry, replay, harness). |
| `syncfit-database` | Persistence library (models, sessions, reconciliation). |
| `syncfit-backend` | Application executable (orchestration + API). |
| `syncfit-frontend` | Presentation executable (Next.js UI). |
| `syncfit-hardware` | Embedded firmware (edge). |
| `syncfit-infra` | Deployment & operations (Docker/AWS). |
| `syncfit-presentation` | Defense deck and diagrams. |

## Cross-cutting concerns

- **Security / roles:** JWT auth; `ATHLETE`, `GYM_ADMIN`, `SUPER_ADMIN`
  (administrative only, role change/delete require the admin password).
- **i18n:** EN / ES / ZH across backend and frontend.
- **Safety:** impact/supine rules, symptom-driven contraindications.
- **Data:** Postgres (prod) / SQLite (dev); additive schema reconciliation.

## Visual summary

The Beamer deck (`beamer/syncfit-pitch.pdf`) shows the two-AI pipeline ("Dos IAs
y un guardián"), the backend layers and the data structures used in the live
flow ("Cómo está construido" and "Estructuras de datos").

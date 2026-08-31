# ARCHITECTURE.md: iSimulator Target Architecture

**Version:** 0.3.0
**Status:** Active
**Last Updated:** 2026-08-31
**Authority:** ISIM-CR-01, ISIM-CR-02 (openspec/changes/)

---

## 1. Definition

iSimulator is a semantic execution environment for representing, simulating, experimenting with, predicting the behavior of, and interacting with contextualized digital twins (iTwins).

The primary conceptual chain:

```
Real / Intended World
        |
        v
   Contextualized iTwin
        |
        v
   Executable Model
        |
        v
   Simulation Runtime
        |
   +----+----+
   v    v    v
Scenario Forecast Optimization
   |    |    |
   +----+----+
        v
   Decision Support
        |
        v
   Interactive Experience
        |
        v
   Human / AI Interaction
```

**Governing principle:** the visualization layer, analytics layer, and LLM consume and operate upon the simulation contract; they do not redefine the semantic or simulation model.

## 2. Target Logical Architecture

```
+--------------------------------------------------------------+
|                     INTERACTION LAYER                        |
|   Human UI        Natural Language       External Apps       |
+---------------------------+----------------------------------+
                            v
+--------------------------------------------------------------+
|                    INTERACTION SERVICES                      |
|   Twin Explorer | Scenario Builder | Controls | AI Tool API  |
+---------------------------+----------------------------------+
                            v
+--------------------------------------------------------------+
|                    ANALYTICAL SERVICES                       |
|  Forecast | Prediction | Optimization | Sensitivity | Report |
+---------------------------+----------------------------------+
                            v
+--------------------------------------------------------------+
|                    EXPERIMENT SERVICES                       |
|  Scenario | Experiment | Replication | Comparison | Results  |
+---------------------------+----------------------------------+
                            v
+--------------------------------------------------------------+
|                    SIMULATION RUNTIME                        |
|  Clock | Events | State | Process | Resources | Controls     |
|  Scheduler | Rules | Policies | Metrics | Observers          |
+---------------------------+----------------------------------+
                            v
+--------------------------------------------------------------+
|                    EXECUTABLE iTWIN                          |
|  Entity | State | Behavior | Process | Resource | Event      |
|  Capability | Function | Service | Policy | Rule | Metric    |
+---------------------------+----------------------------------+
                            v
+--------------------------------------------------------------+
|                    SEMANTIC FOUNDATION                       |
|  WSF | OpenDEAM | iSimulator Catalogs | Standards Alignment  |
+--------------------------------------------------------------+
```

## 3. The Five Models (ISIM-CR-01 section 5)

The word "model" is never ambiguous in iSimulator. Five models are explicitly separated:

| Model | Question | Contents |
|-------|----------|----------|
| Semantic Model | What something is | Entity, Role, Capability, Function, Resource, Service, Process, Information, Relationship |
| State Model | What the twin is like now | State Variable, State Value, State Transition, Condition, Observation, Measurement, Timestamp |
| Behavior Model | How the twin behaves | Event, Activity, Process, Transition, Rule, Policy, Constraint, Resource Consumption |
| Simulation Model | How behavior becomes executable | Simulation Clock, Event Queue, Scheduler, Execution Context, Resource Allocation, State Update, Metric Collection, Randomness |
| Scenario Model | How "what if" is asked | Baseline, Initial State, Parameter Overrides, Control Changes, Events, Policies, Constraints, Horizon, Random Seed |

An iTwin describes what the entity is. The **iTwin Execution Model** describes how that representation becomes executable. Loading an iTwin produces an executable simulation context without changing the semantic identity of the iTwin.

## 3a. Framework Positioning (ISIM-CR-02)

iSimulator is an integration and semantic orchestration framework: Semantic Framework + Simulation Framework + Interaction Framework, with integration adapters to external engines (DES, ABM, FMI, renderers, analytics). iSimulator owns models, composition, contracts, and provenance; it adopts proven open-source engines rather than recreating them (ADR-0002: adopt before build, Integration Decision Records, permissive license policy).

Three-level engine architecture:

```
Level 1: Native Enterprise Primitives (Process, Queue, Resource, Activity, Event, Policy, Capacity)
            |
            v
Level 2: iSimulator Execution Abstraction (engine-neutral execution model)
            |
            v
Level 3: External Execution Engines via Simulation Adapters (SimPy, Mesa, FMI, ...)
```

## 4. Engine Abstraction

iSimulator is not a wrapper around one simulation engine. The simulation-engine abstraction supports: Discrete Event, Continuous, Discrete Time, Agent Based, System Dynamics, Hybrid, Co-Simulation.

- First reference execution mode: **Discrete Event Simulation** (natural fit for enterprise processes, queues, resources, events, capacity).
- **SimPy is a candidate reference engine, not "the iSimulator engine"** (ISIM-CR-02). Selection of the reference engine is by Integration Decision Record after integration testing; the enterprise architect never needs to know which engine is underneath.
- The adapter contract (load, compile, initialize, run, pause, resume, step, observe, terminate, result) is the anti-lock-in mechanism; engine results are normalized into the iSimulator result model.

## 5. Epistemic Separation (Observation Model)

Model Value, Observed Value, Simulated Value, Forecast Value, and Predicted Value are different epistemic sources, never different values of one property.

| Kind | Question |
|------|----------|
| Simulation | What happens under specified model assumptions? |
| Forecast | What is likely to happen based on observed historical behavior? |
| Prediction | What future state does the model estimate? |
| Optimization | Which controllable configuration produces the preferred outcome? |

These are separate analytical services.

## 6. Natural Language Boundary

```
User -> Local LLM -> Context Builder -> Tool Selection -> Typed iSimulator API -> Simulation Runtime
```

The LLM never manipulates simulation internals directly. Initial tool contract: inspect_twin, inspect_entity, inspect_process, get_state, get_metric, create_scenario, modify_parameter, modify_control, run_simulation, pause_simulation, resume_simulation, compare_scenarios, forecast, predict, optimize, explain_result, generate_report.

LLM providers sit behind an adapter architecture (Ollama, llama.cpp, vLLM); no specific model is mandated. The LLM receives context from the iTwin itself; embeddings are an auxiliary retrieval mechanism only.

## 7. Control Model

Every UI control maps to an explicit model element: Control Variable, Allowed Range, Current Value, Scenario Override, Simulation Effect, Observed Outcome. Controls carry: identifier, semantic target, current value, allowed range, unit, default, scenario value, validation rule. No hard-coded demo sliders.

## 8. Provenance

Every simulation result identifies: iTwin version, executable model version, scenario version, parameter set, simulation engine and version, random seed, data snapshot, simulation start and end. Results are reproducible by construction.

## 9. Golden Path

**OTCHERE Order-to-Cash / Fulfillment** is the canonical architectural acceptance example:

Order -> Validation -> Credit -> Inventory -> Fulfillment -> Shipment -> Invoice -> Payment

Each stage carries: Resource, Capacity, Processing Time, Queue, Policy, Rule, Failure Rate, SLA, Cost. Acceptance progression: Observe, Manipulate, Simulate, Compare, Explain, Forecast, Optimize, Report.

## 9a. Progressive Complexity (ISIM-CR-02 section 10)

Adoption path: Level 0 Primitive; Level 1 Process; Level 2 Resource; Level 3 Flow; Level 4 Policy; Level 5 Scenario; Level 6 Experiment; Level 7 Prediction; Level 8 Optimization; Level 9 Autonomous. A valid simulation is constructible from simple primitives with no engine knowledge, then progressively elaborated. Entry points: Visual Builder, Natural Language, Programmatic API, Imported Model.

## 10. Repository Responsibilities and Boundary Rule

| Repository | Responsibility |
|------------|----------------|
| itwin-spec | Semantic + executable iTwin specification |
| itwin-enterprise | Organization specialization |
| itwin-catalogs | Reusable model/catalog assets |
| isimulator-core | Simulation execution |
| examples | Canonical executable examples (golden path) |
| wsf-alignment | Semantic grounding |
| opendeam-alignment | Enterprise model alignment |
| standards-alignment | External standards mapping |
| docs | Architecture and conceptual documentation |
| openspec | Change/specification lifecycle |

Future repositories (isimulator-studio, isimulator-api, isimulator-ai, isimulator-analytics, isimulator-connectors) are **not created until their boundaries are established by subsequent CRs**. First prove the domain boundaries; then crystallize them into repositories.

## 11. Technology Baseline (reference, not mandate)

Runtime: Python, FastAPI, Pydantic, SimPy. Data: SQLite, DuckDB, Parquet, PostgreSQL. Analytics: NumPy, pandas, SciPy, statsmodels, scikit-learn. Optimization: SciPy Optimize, Optuna, OR-Tools. UI (CR-06): React, TypeScript, React Flow, ECharts/Plotly, WebSocket. Local AI (CR-08): Ollama, llama.cpp, Qwen-family evaluation.

Recorded as ADR candidates; not irrevocable architecture.

## 12. Non-Goals (ISIM-CR-01)

No simulation engine implementation, no UI, no final LLM selection, no production data synchronization, no 3D visualization mandate, no optimization algorithms, no single simulation paradigm, no enterprise-only limitation. This architecture establishes the contracts that permit those capabilities later.

# PLAN.md: iSimulator Program Plan

**Version:** 0.3.0
**Status:** Active
**Last Updated:** 2026-08-31
**Authority:** ISIM-CR-01 (architecture), ISIM-CR-02 (reusable simulation framework)

---

## 1. Program Board

**GitHub Project:** [iSimulator (org project #1)](https://github.com/orgs/isimulator/projects/1)

All 11 organization repositories are linked to this single board. Work is tracked as epic issues in the owning repository, surfaced on the board with these fields:

| Field | Options |
|-------|---------|
| Status | Todo, In Progress, Done (GitHub default) |
| Item Type | Epic, Story, Task, Decision, Spike |
| Priority | P0, P1, P2, P3 |
| Phase | Phase 0 Foundation Hardening; Phase 1 Executable iTwin Model; Phase 2 Simulation Kernel; Phase 3 Scenario & Experiment; Phase 4 Twin Studio; Phase 5 Forecast & Analytics; Phase 6 Local AI Interaction; Phase 7 Synchronization; Phase 8 Autonomous Loop |
| Milestone | Repo-level milestones |

## 2. Phasing (ISIM-CR-01 section 24)

Phasing is CR-driven. Each phase ends when its CR acceptance criteria are met against the golden path.

| Phase | CR | Goal |
|-------|-----|------|
| Phase 0 Foundation Hardening | ISIM-CR-01 | Coherent target architecture: ARCHITECTURE.md, five-model separation, repo responsibilities, ADR structure |
| Phase 1 Executable iTwin Model | ISIM-CR-02 | Reusable Simulation Framework: primitive library, composition model, declarative simulation spec, adapter contract, progressive complexity |
| Phase 2 Simulation Kernel | ISIM-CR-03 | Reference Engine Integration: engine landscape assessment, IDRs, first adapter proven against the golden path |
| Phase 3 Scenario & Experiment | ISIM-CR-04 | Scenario Experiment Framework: replications, parameter sweeps, comparison, provenance |
| Phase 4 Twin Studio | ISIM-CR-06 | Simulation Builder / Studio: composition canvas, not just visualization; Runtime API (ISIM-CR-05) precedes it |
| Phase 5 Forecast & Analytics | ISIM-CR-07 | Analytics, Forecasting, Optimization as integrated external capabilities |
| Phase 6 Local AI Interaction | ISIM-CR-08 | LLM generates and manipulates primitives/scenarios, never opaque simulation code |
| Phase 7 Synchronization | ISIM-CR-10 | Operational Twin Synchronization (CR-09 Visualization Engine Integrations slots before it) |
| Phase 8 Autonomous Loop | ISIM-CR-11 | Observe-Understand-Simulate-Predict-Evaluate-Decide-Act closed loop |

## 3. Epic Map (board items)

| Epic | Location | Phase | Priority |
|------|----------|-------|----------|
| ISIM-CR-01: Interactive Semantic Simulation Architecture (Decision) | openspec#2 | Phase 0 | P0 |
| Requirements pipeline and v0.2.0 delta process | openspec#1 | Phase 0 | P0 |
| Governance and decision pipeline | docs#1 | Phase 0 | P0 |
| ISO/IEC 30173 terminology map | standards-alignment#1 | Phase 0 | P2 |
| ISIM-CR-02: Executable iTwin Model | itwin-spec#2 | Phase 1 | P0 |
| iTwin metamodel v0.1.0 | itwin-spec#1 | Phase 1 | P0 |
| Organization iTwin specification v0.1.0 | itwin-enterprise#1 | Phase 1 | P1 |
| Seed reusable catalogs | itwin-catalogs#1 | Phase 1 | P1 |
| WSF mapping v0.1.0 | wsf-alignment#1 | Phase 1 | P1 |
| OpenDEAM mapping v0.1.0 | opendeam-alignment#1 | Phase 1 | P1 |
| First worked Organization iTwin (OTCHERE golden path) | examples#1 | Phase 1 | P2 |
| ISIM-CR-03: Simulation Execution Model | isimulator-core#2 | Phase 2 | P1 |
| Execution semantics ADR + runtime skeleton | isimulator-core#1 | Phase 2 | P2 |
| ISIM-CR-04: Scenario Experiment Engine | isimulator-core#3 | Phase 3 | P1 |
| ISIM-CR-05..CR-10 roadmap tracker | docs#2 | Phase 4 | P2 |

CR-05 through CR-11 are tracked in one roadmap epic until their repository boundaries are earned (ARCHITECTURE.md section 10). ISIM-CR-09 (Visualization Engine Integrations) was added by the authoritative CR-02.

## 4. Current Milestone: v0.2.0 Specifications

Defined in: openspec, itwin-spec, docs, itwin-enterprise, itwin-catalogs.

Exit criteria:

1. ADR-0001 (iTwin metamodel serialization) resolved: JSON + JSON Schema + Pydantic, JSON-LD projection additive. ADR-0002 (technology integration policy) resolved: adopt before build, Integration Decision Records, permissive license policy.
2. openspec change-delta workflow demonstrated end-to-end: ISIM-CR-01 lands as changes/ISIM-CR-01.
3. itwin-spec v0.1.0 covers: Entity anchor, semantics, behavior, operations, control, temporal stipulations, execution-model boundary.
4. Organization iTwin spec v0.1.0 drafted against OpenDEAM catalogs.
5. Editorial pass complete: Design Specification tone, dash rules, glossary conformance.

## 5. Key Open Decisions (tracked as ADRs)

| Decision | Where | Blocking |
|----------|-------|----------|
| ADR-0001: iTwin metamodel serialization (CR-01 recommends JSON + JSON Schema + Pydantic) | docs/adr/0001 | itwin-spec v0.1.0, catalogs, examples |
| Simulation engine abstraction contract | isimulator-core (CR-03 ADR) | runtime skeleton |
| OpenDEAM direct reuse vs mapping | itwin-enterprise (future ADR) | Organization iTwin spec |
| LLM provider adapter contract | future (CR-08) | local AI interaction |
| AAS / ISO 23247 interoperability strategy | standards-alignment (future ADR) | industrial asset twins |

## 6. Working Agreements

1. Epic checklist items convert to child issues (Item Type: Task or Story) when work starts; epics stay high-level.
2. CRs are the unit of architectural change; each CR lands in openspec/changes/ before implementation.
3. Decisions are ADR-first: an ADR issue (Item Type: Decision) precedes dependent specification work.
4. Normative documents follow the docs rules: Design Specification tone; no en/em dashes; semantic versioning with CHANGELOG.
5. Repository boundaries are earned, not anticipated: new repos are created only when a CR establishes their contract.
6. Board hygiene: closing an issue moves its item to Done; new requirements enter via openspec changes before becoming work items.

---

**Document Owner:** iSimulator project
**Related Documents:** ARCHITECTURE.md, DESIGN.md, ORG.md, glossary.md, openspec/specs/isimulator/spec.md, openspec/changes/ISIM-CR-01

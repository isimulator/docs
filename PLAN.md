# PLAN.md: iSimulator Program Plan

**Version:** 0.1.0
**Status:** Active
**Last Updated:** 2026-08-31

---

## 1. Program Board

**GitHub Project:** [iSimulator (org project #1)](https://github.com/orgs/isimulator/projects/1)

All 11 organization repositories are linked to this single board. Work is tracked as epic issues in the owning repository, surfaced on the board with these fields:

| Field | Options |
|-------|---------|
| Status | Todo, In Progress, Done (GitHub default) |
| Item Type | Epic, Story, Task, Decision, Spike |
| Priority | P0, P1, P2, P3 |
| Phase | P1 Specifications, P2 Enterprise Twinning, P3 Alignments, P4 Runtime, P5 Examples & Accessibility |
| Milestone | Repo-level milestones (currently: v0.2.0 Specifications) |

## 2. Phasing

Phases derive from DESIGN.md section 7 (open questions) and ORG.md section 7 (immediate next steps). Order is dependency-driven: specifications precede enterprise twinning, twinning precedes alignments, alignments inform the runtime, the runtime enables examples.

| Phase | Goal | Epic issues |
|-------|------|-------------|
| P1 Specifications | Requirements pipeline, iTwin metamodel v0.1.0, governance/decision pipeline | openspec#1, itwin-spec#1, docs#1 |
| P2 Enterprise Twinning | Organization iTwin spec v0.1.0, seed catalogs | itwin-enterprise#1, itwin-catalogs#1 |
| P3 Alignments | WSF, OpenDEAM, ISO/IEC 30173 mappings | wsf-alignment#1, opendeam-alignment#1, standards-alignment#1 |
| P4 Runtime | Execution semantics ADR, runtime skeleton | isimulator-core#1 |
| P5 Examples & Accessibility | First worked Organization iTwin, non-technical walkthrough | examples#1 |

## 3. Current Milestone: v0.2.0 Specifications

Defined in: openspec, itwin-spec, docs, itwin-enterprise, itwin-catalogs.

Exit criteria:

1. ADR-0001 (iTwin metamodel serialization) resolved and recorded in docs/adr/.
2. openspec change-delta workflow demonstrated end-to-end on one real change.
3. itwin-spec v0.1.0 covers: Entity anchor, semantics, behavior, operations, control, temporal stipulations.
4. Organization iTwin spec v0.1.0 drafted against OpenDEAM catalogs.
5. Editorial pass complete: Design Specification tone, dash rules, glossary conformance.

## 4. Key Open Decisions (tracked as ADRs)

| Decision | Where | Blocking |
|----------|-------|----------|
| ADR-0001: iTwin metamodel serialization format | docs/adr/0001 | itwin-spec v0.1.0, catalogs, examples |
| Simulation execution semantics | isimulator-core (future ADR) | runtime skeleton |
| OpenDEAM direct reuse vs mapping | itwin-enterprise (future ADR) | Organization iTwin spec |
| AAS / ISO 23247 interoperability strategy | standards-alignment (future ADR) | industrial asset twins (post-v0.2.0) |

## 5. Working Agreements

1. Epic checklist items convert to child issues (Item Type: Task or Story) when work starts; epics stay high-level.
2. Decisions are ADR-first: an ADR issue (Item Type: Decision) precedes dependent specification work.
3. Normative documents follow the docs rules: Design Specification tone; no en/em dashes; semantic versioning with CHANGELOG.
4. Board hygiene: closing an issue moves its item to Done; new requirements enter via openspec changes before becoming work items.

---

**Document Owner:** iSimulator project
**Related Documents:** DESIGN.md, ORG.md, glossary.md, openspec/specs/isimulator/spec.md

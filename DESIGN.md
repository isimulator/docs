# DESIGN.md: iSimulator & iTwin

**Version:** 0.1.0  
**Status:** Draft  
**Last Updated:** 2026-08-31  
**Evolvable:** Yes: versioned; changes tracked via CHANGELOG and OpenSpec deltas

---

## 1. Purpose of this Document

This DESIGN.md defines the conceptual and structural design that informs:

- Creation of the GitHub organization
- Repository layout and responsibilities
- The native concept **iTwin**
- Focus on **enterprise architecture twinning** of organization functions and their operations
- How the work relates to formal Digital Twin standards (especially ISO/IEC 30173) and open foundations (WSF, OpenDEAM)

It is intentionally high-level and evolvable. Detailed requirements live in OpenSpec-style specifications; detailed architecture decisions live in ADRs.

---

## 2. Core Concepts

### 2.1 iTwin (Native Term)

**iTwin** is the name we use for our view of a digital twin.

An iTwin is:

> A digital representation of a concrete entity (physical, logical, or organizational) that captures its semantics, behavior, operations, control models, temporal stipulations, and operational environment, and that can be simulated while remaining faithful to that context.

Key characteristics of an iTwin:

- **Entity-centric**: anchored in a real or planned entity
- **Semantically rich**: carries domain meaning, not only state variables
- **Operationally oriented**: models functions, operations, and control
- **Temporally aware**: supports lifecycle, validity, scenarios, and time-dependent rules
- **Simulatable**: can be executed within iSimulator under defined scenarios
- **Inspectable and accessible**: intended for use by digital architects and domain experts

iTwin is our specialization of the broader “digital twin” concept. We acknowledge and align with ISO/IEC 30173 terminology while using “iTwin” consistently for models produced or consumed by this project.

### 2.2 Organization iTwin / Enterprise iTwin

A primary focus area is the **Organization iTwin** (also called Enterprise iTwin):

> An iTwin that represents an organization (or a significant organizational unit / digital business ecosystem) by twinning its functions, operations, capabilities, governance, and lifecycle.

This draws heavily on:

- **OpenDEAM**: for enterprise architecture layers, catalogs (capabilities, actors, processes, etc.), lifecycle states, and governance loops
- **WSF**: for foundational entity, relationship, time, policy, and assertion semantics

### 2.3 iSimulator

**iSimulator** is the practical engine and platform that:

- Hosts and executes iTwins
- Allows configuration of scenarios, control inputs, and temporal constraints
- Supports iterative contextualization of problem spaces
- Remains accessible to non-technical domain participants once the iTwin exists

---

## 3. Relationship to Formal Standards (ISO/IEC 30173 and related)

ISO/IEC 30173:2023 (*Digital twin: Concepts and terminology*) establishes shared vocabulary and high-level concepts for digital twins, including:

- Definitions and related concepts
- Digital twin system context
- Life cycle process for digital twin
- Types of digital twin
- Stakeholders and functional views

**Our stance:**

- We **align terminology** with ISO/IEC 30173 where it is clear and useful.
- We **do not claim** that iTwin or iSimulator is itself an ISO/IEC standard.
- We treat ISO/IEC 30173 as a **complementary terminology and conceptual reference**.
- For manufacturing/industrial asset twins we remain aware of ISO 23247 and IEC 63278 (AAS) and may provide mappings later.
- Our differentiation lies in:
  - Semantic fidelity and operational/behavioral modelling
  - Organization and enterprise-function twinning
  - Accessibility for digital architects and domain experts
  - Executable specifications grounded in WSF + OpenDEAM

All public documentation SHOULD reference ISO/IEC 30173 when introducing the broader digital-twin concept, then introduce iTwin as our specialized, executable view.

---

## 4. Foundational Sources in the Design

| Source | Role in Design |
|--------|----------------|
| **World Semantic Foundation (WSF)** | Generic semantic backbone: Entity, Relationship, Time, Validity, Policy, Process, Organisation, Assertion, Provenance, etc. |
| **OpenDEAM (TechNeHub Labs)** | Enterprise architecture layer: architecture layers, catalogs, lifecycle (Baseline/Current/Target/Transition/Scenario), governance loop |
| **ISO/IEC 30173** | Shared terminology and high-level digital twin concepts |
| **iSimulator design principles** | Entity-first, semantic fidelity, accessibility, utilitarian, contextual, extensible |

---

## 5. Design Implications for the Organization and Repositories

### 5.1 Organization Purpose

The GitHub organization exists to:

1. Host evolving, versioned specifications for iTwins
2. Focus first on **Organization iTwins** (enterprise functions and operations)
3. Provide clear alignment artifacts to WSF, OpenDEAM, and ISO/IEC 30173
4. Keep the work open, evolvable, and usable by architects and domain experts

### 5.2 Key Repositories (Design Intent)

| Repository | Primary Responsibility |
|------------|------------------------|
| `itwin-spec` | Core executable specification language / metamodel for iTwins |
| `itwin-enterprise` | Specifications, catalogs, and patterns for Organization / Enterprise iTwins |
| `isimulator-core` | Runtime engine that executes iTwins |
| `wsf-alignment` | Mappings and adapters to WSF concepts |
| `opendeam-alignment` | Mappings and adapters to OpenDEAM layers and catalogs |
| `standards-alignment` | Explicit mappings and notes relative to ISO/IEC 30173 (and later AAS / ISO 23247) |
| `openspec` / specs | Requirements and change tracking in OpenSpec style |
| `docs` | DESIGN.md, ADRs, vision, glossary |
| `examples` | Concrete worked Organization iTwin examples |

### 5.3 Versioning & Evolution

- All normative documents and specifications SHALL carry a semantic version.
- Changes to requirements SHOULD follow OpenSpec delta conventions (ADDED / MODIFIED / REMOVED).
- DESIGN.md itself is versioned; major conceptual shifts require a major version bump and an ADR.

---

## 6. High-Level Design Principles (Summary)

1. **Entity-first**: iTwins start from concrete entities.
2. **Semantic fidelity**: meaning is preserved, not stripped away.
3. **Operational & control focus**: functions, operations, and control models are first-class.
4. **Temporal awareness**: lifecycle, validity, scenarios, and time rules matter.
5. **Accessible**: usable by digital architects and domain experts.
6. **Grounded**: builds on WSF + OpenDEAM; aligns with ISO/IEC 30173 terminology.
7. **Evolvable**: specifications and design documents are versioned and change-tracked.
8. **Complementary**: does not replace formal Digital Twin standards; fills gaps they leave open.

---

## 7. Open Questions / Future Evolution (v0.1.0)

- Exact formal metamodel for an iTwin (JSON Schema / TTL / Pydantic / etc.)
- Degree of direct reuse vs. mapping of OpenDEAM catalogs
- Interoperability strategy with AAS (IEC 63278) for industrial assets
- Simulation execution semantics (discrete-event, continuous, hybrid, agent-based, etc.)
- Tooling for non-technical users to configure and run Organization iTwins

These will be resolved through subsequent versions of this DESIGN.md, ADRs, and OpenSpec requirements.

---

**Document Owner:** iSimulator project  
**Related Documents:** ORG.md, openspec/specs/isimulator/spec.md, README.md  
**Status:** Living design draft

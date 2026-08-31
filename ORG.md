# GitHub Organization Specification: iSimulator / iTwin

**Version:** 0.1.0  
**Status:** Draft  
**Last Updated:** 2026-08-31  
**Evolvable:** Yes: changes tracked via version bumps and CHANGELOG

---

## 1. Purpose

This document specifies the intended GitHub organization structure, naming, governance, and repository layout for the **iSimulator** platform and its native digital-twin concept **iTwin**.

The organization exists to host:

- Executable specifications and models for entity-centric digital twins
- Focus on **enterprise architecture twinning** of organization functions and their operations
- Supporting tooling, catalogs, and simulation runtime foundations
- Alignment with open semantic foundations (WSF) and enterprise architecture models (OpenDEAM)
- Complementary positioning relative to formal Digital Twin standards (ISO/IEC 30173 and related)

---

## 2. Recommended Organization Name

**Primary recommendation:** `iSimulator` or `iTwin-Foundation`

| Candidate | Pros | Cons |
|-----------|------|------|
| `iSimulator` | Direct match to product name | May feel tool-centric |
| `iTwin-Foundation` | Emphasizes the twin concept and open foundation | Slightly longer |
| `iTwin-Labs` | Lightweight, experimental feel | Less formal |

**Decision (v0.1.0):** Prefer **`iSimulator`** as the GitHub organization name.  
Use **`iTwin`** consistently as the native term for digital twins within all repositories and documentation.

---

## 3. Core Naming Conventions

| Concept | Native Term | Notes |
|---------|-------------|-------|
| Digital Twin (general) | **iTwin** | Our view / specialization of digital twin concepts |
| Simulation platform | **iSimulator** | The engine and platform |
| Organizational / enterprise twin | **Organization iTwin** or **Enterprise iTwin** | Focus area for executable specifications |
| Entity being twinned | **Entity** (aligned with WSF) | Concrete real-world or logical entity |

All public-facing language SHOULD prefer “iTwin” over generic “digital twin” when referring to models produced or consumed by this organization.

---

## 4. Intended Repository Structure

```
iSimulator/                          # GitHub Organization
├── .github/                         # Org-level profiles, templates, CODEOWNERS
├── README.md                        # Org landing (points to vision)
├── org-spec/                        # This document and evolution history
│
├── isimulator-core/                 # Core simulation engine (runtime)
├── itwin-spec/                      # Executable specifications for iTwins
├── itwin-enterprise/                # Enterprise architecture twinning (org functions & operations)
├── itwin-catalogs/                  # Reusable catalogs (capabilities, processes, etc.)
├── wsf-alignment/                   # Mappings and adapters to World Semantic Foundation
├── opendeam-alignment/              # Mappings and adapters to OpenDEAM
├── standards-alignment/             # Alignment notes to ISO/IEC 30173 and related
│
├── openspec/                        # OpenSpec-style requirements and change tracking
├── docs/                            # Design docs, ADRs, vision
└── examples/                        # Worked examples of Organization iTwins
```

Repositories may be private or public according to maturity. Core specifications SHOULD become public as they stabilize.

---

## 5. Governance Principles

- **Versioned & evolvable**: Every normative document carries a semantic version and CHANGELOG.
- **Spec-first**: Executable specifications and requirements precede implementation where practical.
- **Open foundations**: Explicit alignment with WSF (semantic backbone) and OpenDEAM (enterprise architecture layer).
- **Standards-aware**: Acknowledge and map to ISO/IEC 30173 (Digital twin: Concepts and terminology) and related formal standards without claiming to replace them.
- **Accessible**: Documentation and models remain usable by digital architects and domain experts, not only software engineers.
- **Apache-2.0 preferred** for public repositories unless a stronger reason exists.

---

## 6. Document Evolution

This ORG.md document is itself versioned:

- **Major** version: structural change to organization or naming philosophy
- **Minor** version: addition of repositories, governance rules, or alignment statements
- **Patch** version: clarifications and editorial improvements

All changes SHOULD be recorded in a CHANGELOG.md colocated with this file.

---

## 7. Immediate Next Steps (v0.1.0)

1. Create the GitHub organization under the chosen name.
2. Seed the following repositories:
   - `itwin-spec`
   - `itwin-enterprise`
   - `openspec` (or embed openspec structure inside a meta-repo)
   - `docs`
3. Place this ORG.md, DESIGN.md, and the initial requirements specification into the appropriate repositories.
4. Establish CODEOWNERS and basic branch protection for specification repositories.

---

**Document Owner:** iSimulator project  
**Status:** Living draft: subject to refinement as the organization is stood up.

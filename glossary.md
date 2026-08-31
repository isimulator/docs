# Glossary: iSimulator / iTwin

**Version:** 0.1.0
**Status:** Draft
**Last Updated:** 2026-08-31

---

Canonical terms for all iSimulator organization repositories. Public-facing language prefers **iTwin** over generic "digital twin" for models produced or consumed by this organization.

| Term | Definition |
|------|------------|
| **iTwin** | This project's native, executable specialization of the digital twin concept: a digital representation of a concrete entity capturing its semantics, behavior, operations, control models, temporal stipulations, and operational environment, simulatable within iSimulator. |
| **iSimulator** | The simulation engine and platform that hosts and executes iTwins under configured scenarios. |
| **Organization iTwin** (Enterprise iTwin) | An iTwin representing an organization or significant organizational unit, twinning its functions, operations, capabilities, governance, and lifecycle. |
| **Entity** | A concrete real-world or logical entity that an iTwin represents (aligned with WSF). |
| **Scenario** | A configured set of initial conditions, external events, and control inputs executed against an iTwin. |
| **WSF** | [World Semantic Foundation](https://github.com/World-Semantic-Foundation): generic semantic backbone (Entity, Relationship, Time, Policy, Assertion, Provenance, ...). |
| **OpenDEAM** | [Open Digital Enterprise Architecture Model](https://github.com/technehub-labs), TechNeHub Labs: enterprise architecture layers, catalogs, lifecycle states, governance loop. |
| **ISO/IEC 30173** | Digital twin: Concepts and terminology. Terminology reference; iSimulator aligns with it and does not claim to replace it. |
| **OpenSpec delta** | Change convention for requirements: ADDED / MODIFIED / REMOVED sections with full scenario text. |

## Terminology Rules

1. "iTwin" for models produced or consumed by this project; "digital twin" only when introducing the broader concept alongside an ISO/IEC 30173 reference.
2. En dashes and em dashes are not used in normative documents; use colons or semicolons.
3. Normative documents use Design Specification tone: declarative statements of what the system does, not proposals.

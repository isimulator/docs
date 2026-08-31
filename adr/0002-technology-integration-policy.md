# ADR-0002: Technology Integration Policy (Adopt Before Build)

**Version:** 0.1.0
**Status:** Accepted
**Last Updated:** 2026-08-31
**Authority:** ISIM-CR-02 sections 1-3, 20-21

---

## Context

iSimulator is an integration and semantic orchestration framework, not a new simulation-engine, rendering-engine, or domain-specialist platform. iSimulator owns the iTwin model, enterprise simulation primitives, composition, scenario and control semantics, experiment definition, result/provenance semantics, integration contracts, and interaction/tool contracts. It does not own proprietary DES/ABM engines, renderers, ML frameworks, LLMs, or specialized industrial models.

## Decision

1. **Adopt before build.** For every substantial technical capability, iSimulator first identifies suitable open-source or open-standard implementations before implementing equivalent functionality.
2. **Integration Decision Records (IDRs).** Every external engine or framework candidate is assessed by an ISIM-ADR recording: capability, candidate, license, role (Embedded / Adapter / Service / Optional), fit, integration cost, lock-in, decision (Adopt / Integrate / Reference / Reject), rationale. Informal technology choices are not permitted.
3. **Evaluation criteria:** functional fit, semantic fit, adapter-ability, license, commercial safety, extensibility, maturity, community, performance, reproducibility, deployment options, data exchange, lock-in.
4. **License policy.** Preferred: MIT, Apache-2.0, BSD-2/3-Clause. Conditional: MPL/EPL and permissive weak-copyleft, standards with compatible implementation licenses. Avoid as embedded core dependencies: GPL/AGPL, proprietary SDKs, restrictive source-available licenses. Rationale: iSimulator's role as an easily reusable enterprise framework makes permissive licensing strategically preferable.
5. **Adapters are the anti-lock-in mechanism.** Every external capability sits behind an adapter contract; "adopt" names the best current candidate implementation, never a conceptual dependency.

## Consequences

- SimPy is a candidate reference DES engine, not "the iSimulator engine" (IDR to follow integration testing).
- OpenModelica: reference/integration candidate only; OSMC licensing (GPL/OSMC-PL variants) fails the preferred license policy.
- FMI 3.0: strong standards integration candidate; specification code is BSD-2-Clause.
- Initial matrix (ISIM-CR-02 section 20) stands as provisional positions; each entry converts to an IDR after integration testing.

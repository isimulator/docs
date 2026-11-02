# ADR-0003 / IDR-0001: SimPy as First Reference Simulation Engine

**Status:** Accepted
**Date:** 2026-09-02
**Authority:** ISIM-CR-03 (proposal merged as openspec PR #6); ADR-0002 (technology integration policy)

---

## Context

ISIM-CR-02 established the engine-adapter contract as the anti-lock-in
mechanism: external engines plug in exclusively through
`itwin-spec/contracts/engine-adapter.md`, selection binds by declared
capability, never by engine name. ISIM-CR-03 requires the first Integration
Decision Record for the candidate reference Discrete Event Simulation
engine.

## Decision

**Adopt SimPy 4.x as the first reference DES engine** (IDR-0001).

Assessment per the ADR-0002 evaluation model:

| Criterion | Assessment |
|-----------|------------|
| Functional fit | High: processes, resources with capacity, queues, timeouts, event scheduling map one-to-one onto the enterprise primitives of the CR-02 library |
| Semantic fit | High: activity -> process, resource -> Resource with capacity, arrival -> timeout loop; no iTwin concept needs distortion |
| Integration | High: pure-Python library, no native code, wraps cleanly behind AdapterBase |
| License | MIT (permissive; compatible with the org Apache-2.0 policy) |
| Commercial use | Permitted without restriction |
| Extensibility | Custom resource types and listeners supported |
| Maturity | Established (2002+), stable 4.x API, widely cited in DES literature |
| Community | Standard Python DES library; substantial adoption in education and research |
| Performance | Sufficient for enterprise-scale golden path (72k arrivals over 30-day horizon replay in seconds) |
| Reproducibility | Achievable: SimPy 4 has no built-in RNG; all randomness routes through a seeded numpy RandomState, making replay deterministic (proved by tests/test_replay_determinism.py) |
| Deployment | Pure Python; local, containerized, and cloud without change |
| Data exchange | Clean: adapter normalizes results to the R09 JSON contract |
| Lock-in | Low: the adapter boundary isolates iSimulator from SimPy; a second engine (Mesa, FMI) plugs in by writing a second adapter against the same contract |

## Evidence

The implementation (ISIM-CR-03 PR-2, `isimulator-core`) replays the OTCHERE
golden path end-to-end through `SimPyAdapter`:

- all 10 contract operations present (pause/resume/step flagged
  optional-with-capability for SimPy v1);
- all 6 declared metrics populated in the normalized R09 result;
- deterministic replay proven (identical seed, identical metrics);
- the SimPy import is confined to `isimulator_core/adapter/simpy_adapter.py`
  and asserted by CI.

The first replay surfaced two model findings, resolved within the CR-03
PR set: the OTCHERE capacities were bottleneck-saturated at 36 orders/hour
(calibration applied), and arrival rates could not bind to parameters
(control targets are the binding mechanism in the 0.1.0 schema; parameter
indirection recorded as a schema gap for a future CR).

## Consequences

- SimPy is a reference adapter, not the iSimulator engine: no iTwin
  document references it, and the enterprise architect never needs to know
  it is underneath.
- `simpy>=4.0,<5.0` is pinned in `isimulator-core`.
- Determinism discipline: no engine-level randomness bypasses the seeded
  RandomState.
- Replacement or additional engines are evaluated by new IDRs under the
  same policy.

# ADR-0001: iTwin Metamodel Serialization Format

**Version:** 0.1.0
**Status:** Accepted
**Last Updated:** 2026-08-31
**Decides:** DESIGN.md v0.1.0 section 7 open question; recommended by ISIM-CR-01 section on Phase 1

---

## Context

An iTwin must be machine-readable (tooling, validation, CI), human-readable (digital architects and domain experts), and semantically groundable (WSF and OpenDEAM mapping, downstream RDF/OWL). DESIGN.md v0.1.0 section 7 left the serialization format open. ISIM-CR-01 recommended JSON + JSON Schema + Pydantic with semantic identifiers capable of later mapping into RDF/JSON-LD.

## Options Considered

| Option | Strengths | Weaknesses |
|--------|-----------|------------|
| A. JSON + JSON Schema + Pydantic | Readable, validated, typed in the reference runtime, cheap tooling, versionable in git | Semantics are conventional, not formally entailed |
| B. RDF/Turtle + SHACL | Formal semantics, inference, direct WSF grounding | High authoring cost for domain experts; weaker fit for interactive tooling and the Studio |
| C. Pydantic-only (code as schema) | Single source in the runtime | Not a portable specification; locks the metamodel to Python |

## Decision

**Option A: JSON documents, constrained by JSON Schema, mirrored by Pydantic models in the reference runtime.**

1. The iTwin document format is JSON. Every iTwin is a JSON document valid against the published JSON Schema for its spec version.
2. JSON Schema is the normative constraint language. Pydantic models in isimulator-core are generated from or verified against the same schema; schema wins on conflict.
3. Every semantic element carries a stable semantic identifier (`id`) and an optional `concept` field naming its WSF/OpenDEAM concept. This keeps RDF/JSON-LD mapping possible without requiring RDF authoring.
4. JSON-LD context documents MAY be published later so that an iTwin document is also valid JSON-LD. This is an additive mapping, never a rewrite of the base format.
5. SHACL or OWL validation, when needed, operates on the JSON-LD projection, not on the authoring format.

## Consequences

### Positive

- Non-programmers can read and diff iTwin documents; validators run in CI.
- The reference runtime (Python, FastAPI, Pydantic) consumes the schema directly.
- The format serves Phases 1-5 without change; semantic web grounding remains available through projection.

### Negative / Risks

- Formal inference requires the JSON-LD projection; the base JSON format carries no entailment.
- Dual maintenance risk between JSON Schema and Pydantic models; mitigated by a conformance test that loads every schema example through both validators.

### Follow-ups

- Conformance levels for iTwin documents are defined in ISIM-CR-02.
- The JSON-LD context publication is scheduled with wsf-alignment v0.1.0 work.

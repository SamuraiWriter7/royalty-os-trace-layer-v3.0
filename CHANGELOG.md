# Changelog

All notable changes to this project will be documented in this file.

This repository follows a lightweight versioning model during the early specification phase.

---

## [v0.1.0-candidate] - 2026-05-27

### Added

Initial repository structure for **Royalty OS Trace Layer v3.0**.

This candidate release introduces the first working specification set for recording authorized AI usage, trace evidence, attribution signals, and allocation-trigger candidates.

#### Core Schemas

- Added `schemas/royalty-trace-event-v3.0.schema.json`
  - Defines the core Royalty Trace Event object.
  - Supports AI retrieval, usage type, permission status, verification signals, attribution scores, privacy controls, and evidence references.
  - Includes support for:
    - direct quote
    - concept reference
    - structural influence
    - outlier origin detection
    - allocation readiness

- Added `schemas/royalty-allocation-trigger-v3.0.schema.json`
  - Defines the bridge object between Trace Layer and downstream Allocation Layer.
  - Supports allocation candidates, review status, decision context, privacy controls, and evidence references.
  - Clarifies that allocation triggers do not execute payment directly.

#### Examples

- Added `examples/trace-event.structural-influence.example.json`
  - Demonstrates a trace event where an AI system structurally reuses a framework, architecture, or conceptual pattern.

- Added `examples/trace-event.concept-reference.example.json`
  - Demonstrates a trace event where an AI system references an original concept, coined term, or theoretical idea without direct quotation.

- Added `examples/trace-event.direct-quote.example.json`
  - Demonstrates a trace event where an AI system directly quotes a registered source fragment.

- Added `examples/trace-event.outlier-origin.example.json`
  - Demonstrates a trace event where an AI system references a statistically distinctive origin signal or highly original concept.

- Added `examples/allocation-trigger.example.json`
  - Demonstrates an allocation trigger generated from multiple trace events.
  - Shows how structural influence and outlier origin traces can become allocation-review candidates.

#### Documentation

- Added `README.md`
  - Defines the purpose, architecture, schemas, examples, repository structure, validation workflow, privacy principles, and future extensions.

- Added `docs/architecture-overview.md`
  - Explains the overall architecture of Royalty OS Trace Layer v3.0.
  - Covers the relationship between Embedding Layer, Logging Layer, Verification Layer, Trace Event, Allocation Trigger, and Allocation Layer.

- Added `docs/relationship-to-allocation-layer.md`
  - Clarifies the separation between Trace Layer and Allocation Layer.
  - Defines the role of allocation readiness and allocation triggers.
  - Emphasizes that trace evidence should not directly execute payment.

- Added `docs/outlier-origin-detection.md`
  - Defines Outlier Origin Detection as a high-priority evidence mechanism.
  - Explains how distinctive concepts, frameworks, and structures may be detected as origin-like signals.
  - Clarifies that outlier detection is not final ownership proof.

- Added `docs/privacy-and-compliance-notes.md`
  - Provides privacy-aware design notes.
  - Covers data minimization, purpose limitation, prompt handling, identity handling, evidence bundles, provider-side logging, access control, redaction, aggregation, and compliance-oriented design.

#### Validation

- Added `.github/workflows/validate-schemas.yml`
  - Validates the Trace Event schema against four trace examples.
  - Validates the Allocation Trigger schema against the allocation trigger example.
  - Uses Python 3.12 and `jsonschema`.

### Core Concepts Introduced

- Permission-aware AI usage tracing
- Royalty Trace Event
- Allocation Trigger
- Allocation readiness
- Direct quote trace
- Concept reference trace
- Structural influence trace
- Outlier origin trace
- C2PA-inspired provenance metadata
- Watermark-aware verification
- RAG retrieval logging
- Multi-signal verification
- Privacy-aware trace records
- Evidence bundle references
- Review before allocation
- Trace-to-allocation separation

### Design Principles

This release establishes the following core principles:

```text
Trace = evidence
Review = judgment
Allocation = distribution

No allocation without trace.
No trace without permission.
No permission without machine-readable structure.
Make AI usage traceable without making people traceable.
Notes

This is an early draft candidate.

The repository is intended for specification design, prototyping, interoperability discussion, and future implementation experiments.

It should not be treated as:

legal advice
a final technical standard
a complete implementation
a payment system
a copyright enforcement system
an automatic attribution engine
Status
Specification: Royalty OS Trace Layer v3.0
Repository stage: v0.1.0 candidate
Status: Draft

# Changelog

All notable changes to this project will be documented in this file.

This repository follows a lightweight versioning model during the early specification phase.

---

## [v0.1.2-candidate] - 2026-05-27

### Added

#### C2PA Extension Support

* Added `docs/relationship-to-c2pa.md`

  * Explains how Royalty OS Trace Layer v3.0 relates to C2PA-style provenance systems.
  * Clarifies that Royalty OS Trace does not replace C2PA.
  * Defines the core distinction:

    * C2PA-style provenance = where the content came from
    * Royalty OS Trace = how AI used the content
  * Positions C2PA-style provenance as a verification signal for Royalty Trace Events.
  * Explains how C2PA-style manifests, watermarking, retrieval logs, fragment hashes, semantic similarity, and outlier detection may work together as multi-signal trace evidence.

* Added `schemas/royalty-c2pa-extension-v3.0.schema.json`

  * Defines a lightweight Royalty OS metadata extension for C2PA-style manifests.
  * Adds machine-readable fields for:

    * Royalty OS content ID
    * permission scope
    * preferred usage
    * attribution request
    * trace priority
    * trace policy
    * evidence references
    * allocation trigger permission flags
  * Designed as a complementary layer, not a replacement for C2PA.

* Added `examples/royalty-c2pa-extension.example.json`

  * Demonstrates how Royalty OS metadata may be attached to or associated with a C2PA-style provenance record.
  * Shows content identity, permission scope, trace priority, preferred AI usage, evidence bundle references, and trace policy settings.
  * Includes `trace_policy` fields such as:

    * `trace_enabled`
    * `outlier_origin_tracking`
    * `allocation_trigger_allowed`
    * `review_required_before_allocation`
    * `privacy_mode`

### Updated

* Updated `.github/workflows/validate-schemas.yml`

  * Added validation for `schemas/royalty-c2pa-extension-v3.0.schema.json`.
  * Added validation for `examples/royalty-c2pa-extension.example.json`.
  * The validation workflow now checks:

    * five Royalty Trace Event examples
    * one Royalty Allocation Trigger example
    * one Royalty C2PA Extension example

* Updated `README.md`

  * Added C2PA Extension to Design Goals.
  * Added Royalty OS C2PA Extension metadata to the Embedding Layer.
  * Added Royalty OS C2PA Extension detection to the Verification Layer.
  * Updated Core Schemas from two schemas to three schemas.
  * Added a new `Royalty C2PA Extension` schema description.
  * Added a new `C2PA Extension` section.
  * Updated Repository Structure.
  * Updated Start Here.
  * Updated Key Documents.
  * Updated Examples.
  * Updated schema validation targets.
  * Updated Relationship to C2PA-style Provenance.
  * Updated Current Status to `v0.1.2 candidate`.
  * Added C2PA-related future implementation components.

### Core Concepts Added

* Royalty OS C2PA Extension
* C2PA-style provenance bridge
* content provenance vs AI usage trace distinction
* Royalty OS metadata for C2PA-style manifests
* permission metadata for provenance records
* trace-priority metadata
* preferred AI usage metadata
* attribution request metadata
* C2PA-style manifest as verification signal
* soft binding to external provenance records
* lightweight provenance-to-trace bridge
* content identity to AI usage traceability connection

### Design Clarification

This release clarifies the relationship between provenance and traceability:

```text
C2PA-style provenance = where the content came from
Royalty OS Trace = how AI used the content
```

It also preserves the core Royalty OS principle:

```text
Provenance identifies.
Trace records.
Review judges.
Allocation distributes.
```

### Notes

This release does not claim C2PA adoption, C2PA compliance, or formal standardization.

The C2PA Extension schema is an experimental interoperability layer intended to explore how Royalty OS metadata may complement provenance records in AI-era usage tracing.

The extension should be treated as:

* experimental
* lightweight
* complementary
* non-authoritative
* review-oriented

It should not be treated as:

* a replacement for C2PA
* a final standard
* a legal license
* an automatic allocation mechanism
* proof of ownership by itself

---

## [v0.1.1] - 2026-05-27

### Added

#### note/RAG Experiment Line

* Added `docs/note-rag-experiment-notes.md`

  * Describes an experimental workflow for connecting note-style publishing, RAG retrieval, Royalty Trace Events, and Allocation Trigger candidates.
  * Defines a lightweight article-level metadata block for early social proof experiments.
  * Clarifies that the experiment does not claim external platform adoption or production integration.
  * Positions the note/RAG workflow as a prototype for AI-era traceability.

* Added `examples/trace-event.note-rag-reference.example.json`

  * Demonstrates a trace event where a note-style article is retrieved in a RAG-like environment.
  * Represents concept reference and outlier-origin-style influence without direct quotation.
  * Uses privacy-conscious trace settings such as `hash_only`, no raw prompt storage, and anonymized session identifiers.
  * Marks the event as an allocation trigger candidate, not an automatic payment event.

### Updated

* Updated `.github/workflows/validate-schemas.yml`

  * Added `examples/trace-event.note-rag-reference.example.json` to the Trace Event validation set.
  * The validation workflow now checks five Trace Event examples and one Allocation Trigger example.

* Updated `README.md`

  * Added the note/RAG experiment to Design Goals.
  * Added note/RAG experimental records to the Logging Layer description.
  * Added `note/RAG-style reference experiment` to the Royalty Trace Event description.
  * Added a new `note/RAG Experiment` section.
  * Updated Repository Structure.
  * Updated Start Here.
  * Updated Key Documents.
  * Updated Examples.
  * Updated schema validation targets.
  * Updated current status to `v0.1.1 candidate`.
  * Added note/RAG-related future extensions.

* Updated `CITATION.cff`

  * Updated version to `0.1.1-candidate`.
  * Added note/RAG-related keywords and abstract language.

### Core Concepts Added

* note/RAG-style social proof experiment
* article-level Royalty OS Metadata block
* machine-readable metadata for public articles
* simulated or observed RAG retrieval tracing
* note-style article as traceable AI reference source
* concept reference without direct quotation
* privacy-aware note/RAG trace event
* social proof before formal platform integration
* traceable public knowledge article
* experimental route toward C2PA-style extension

### Notes

This release extends the initial Trace Layer specification with a concrete social proof path.

The note/RAG experiment is intentionally lightweight.
It can be tested without requiring direct platform integration.

The purpose is to demonstrate that public articles can be represented as machine-readable trace sources in AI retrieval environments.

This release does not claim that note, AI providers, or any external platform currently implements this specification.

---

## [v0.1.0] - 2026-05-27

### Added

Initial repository structure for **Royalty OS Trace Layer v3.0**.

This release introduces the first working specification set for recording authorized AI usage, trace evidence, attribution signals, and allocation-trigger candidates.

#### Core Schemas

* Added `schemas/royalty-trace-event-v3.0.schema.json`

  * Defines the core Royalty Trace Event object.
  * Supports AI retrieval, usage type, permission status, verification signals, attribution scores, privacy controls, and evidence references.
  * Includes support for:

    * direct quote
    * concept reference
    * structural influence
    * outlier origin detection
    * allocation readiness

* Added `schemas/royalty-allocation-trigger-v3.0.schema.json`

  * Defines the bridge object between Trace Layer and downstream Allocation Layer.
  * Supports allocation candidates, review status, decision context, privacy controls, and evidence references.
  * Clarifies that allocation triggers do not execute payment directly.

#### Examples

* Added `examples/trace-event.structural-influence.example.json`

  * Demonstrates a trace event where an AI system structurally reuses a framework, architecture, or conceptual pattern.

* Added `examples/trace-event.concept-reference.example.json`

  * Demonstrates a trace event where an AI system references an original concept, coined term, or theoretical idea without direct quotation.

* Added `examples/trace-event.direct-quote.example.json`

  * Demonstrates a trace event where an AI system directly quotes a registered source fragment.

* Added `examples/trace-event.outlier-origin.example.json`

  * Demonstrates a trace event where an AI system references a statistically distinctive origin signal or highly original concept.

* Added `examples/allocation-trigger.example.json`

  * Demonstrates an allocation trigger generated from multiple trace events.
  * Shows how structural influence and outlier origin traces can become allocation-review candidates.

#### Documentation

* Added `README.md`

  * Defines the purpose, architecture, schemas, examples, repository structure, validation workflow, privacy principles, and future extensions.

* Added `docs/architecture-overview.md`

  * Explains the overall architecture of Royalty OS Trace Layer v3.0.
  * Covers the relationship between Embedding Layer, Logging Layer, Verification Layer, Trace Event, Allocation Trigger, and Allocation Layer.

* Added `docs/relationship-to-allocation-layer.md`

  * Clarifies the separation between Trace Layer and Allocation Layer.
  * Defines the role of allocation readiness and allocation triggers.
  * Emphasizes that trace evidence should not directly execute payment.

* Added `docs/outlier-origin-detection.md`

  * Defines Outlier Origin Detection as a high-priority evidence mechanism.
  * Explains how distinctive concepts, frameworks, and structures may be detected as origin-like signals.
  * Clarifies that outlier detection is not final ownership proof.

* Added `docs/privacy-and-compliance-notes.md`

  * Provides privacy-aware design notes.
  * Covers data minimization, purpose limitation, prompt handling, identity handling, evidence bundles, provider-side logging, access control, redaction, aggregation, and compliance-oriented design.

#### Validation

* Added `.github/workflows/validate-schemas.yml`

  * Validates the Trace Event schema against four trace examples.
  * Validates the Allocation Trigger schema against the allocation trigger example.
  * Uses Python 3.12 and `jsonschema`.

### Core Concepts Introduced

* Permission-aware AI usage tracing
* Royalty Trace Event
* Allocation Trigger
* Allocation readiness
* Direct quote trace
* Concept reference trace
* Structural influence trace
* Outlier origin trace
* C2PA-inspired provenance metadata
* Watermark-aware verification
* RAG retrieval logging
* Multi-signal verification
* Privacy-aware trace records
* Evidence bundle references
* Review before allocation
* Trace-to-allocation separation

### Design Principles

This release establishes the following core principles:

```text
Trace = evidence
Review = judgment
Allocation = distribution
```

```text
No allocation without trace.
No trace without permission.
No permission without machine-readable structure.
```

```text
Make AI usage traceable without making people traceable.
```

### Notes

This is an early draft release.

The repository is intended for specification design, prototyping, interoperability discussion, and future implementation experiments.

It should not be treated as:

* legal advice
* a final technical standard
* a complete implementation
* a payment system
* a copyright enforcement system
* an automatic attribution engine

### Status

```text
Specification: Royalty OS Trace Layer v3.0
Repository stage: v0.1.0
Status: Draft
```


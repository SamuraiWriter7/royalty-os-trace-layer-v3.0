# Royalty OS Trace Layer v3.0

A machine-readable trace layer for recording authorized AI usage, retrieval events, provenance signals, attribution evidence, and allocation-trigger candidates.

This repository defines the **Trace Layer** of Royalty OS v3.0.

The Trace Layer is designed to record how AI systems access, retrieve, reference, quote, summarize, transform, or structurally depend on creative and knowledge-based content.

Its purpose is not to directly decide payment, ownership, or legal liability.  
Its purpose is to provide a reliable evidence layer that can connect to review and downstream allocation systems.

---

## Core Concept

Royalty OS v3.0 is based on three major layers:

```text
Permission Layer
  ↓
Trace Layer
  ↓
Allocation Layer
```

This repository focuses on the middle layer:

```text
Trace Layer = evidence infrastructure for AI-era value circulation
```

The Trace Layer aims to move AI-based content use from:

```text
AI reference as invisible extraction
```

toward:

```text
AI reference as traceable value circulation
```

---

## Design Goals

Royalty OS Trace Layer v3.0 is designed to support:

- Machine-readable recording of AI retrieval and reference events
- Permission-aware usage evidence
- RAG retrieval logging
- Direct quote tracing
- Concept-level reference tracing
- Structure-level influence tracing
- Outlier origin detection
- C2PA-inspired provenance metadata
- Watermark-aware verification signals
- Privacy-aware trace records
- Allocation-readiness status
- Allocation Trigger generation
- Human or multi-party review before final distribution
- note/RAG-style social proof experiments
- Interoperability with future Royalty OS, RSL, C2PA, RAG, and AI audit ecosystems

---

## Non-Goals

This repository does **not** attempt to:

- Prove legal authorship by itself
- Automatically determine payment
- Replace copyright law
- Replace licensing contracts
- Replace platform policies
- Decide disputes without review
- Claim perfect attribution accuracy
- Require all AI systems to use one centralized registry
- Store unnecessary user identity or raw prompts
- Claim that any external platform currently implements this specification

The Trace Layer provides evidence.

```text
Trace = evidence
Review = judgment
Allocation = distribution
```

---

## Architecture Overview

Royalty OS Trace Layer v3.0 consists of three internal sublayers:

```text
Embedding Layer
  ↓
Logging Layer
  ↓
Verification Layer
```

### 1. Embedding Layer

The Embedding Layer attaches machine-readable identifiers, permission metadata, or provenance signals to participating content.

Possible mechanisms include:

- Text watermarking
- Media watermarking
- C2PA-style manifest metadata
- Royalty OS content identifiers
- Soft binding to external manifests or registries
- Article-level metadata blocks for early experiments

Example metadata:

```yaml
royalty:
  os_id: "royalty-os:example:content:001"
  permission_scope: "allow_reference"
  version: "3.0"
  trace_priority: "high"
```

The Embedding Layer should be opt-in where possible.

---

### 2. Logging Layer

The Logging Layer records what happened when an AI system retrieved, referenced, quoted, or structurally used content.

Typical logging sources include:

- RAG retrieval logs
- AI search logs
- Agent memory logs
- Training data audits
- Evaluation runs
- Manual audits
- Third-party reports
- Simulated note/RAG experiment records

The core object of this layer is the **Royalty Trace Event**.

---

### 3. Verification Layer

The Verification Layer checks whether a trace event is supported by evidence.

Possible verification signals include:

- Watermark detection
- C2PA-style manifest detection
- Soft binding resolution
- Retrieval log confirmation
- Fragment hash comparison
- Semantic similarity analysis
- Structure similarity analysis
- Outlier origin detection
- Manual review
- Third-party attestation

The goal is not perfect certainty.

The goal is structured, reviewable evidence.

---

## Main Flow

The high-level flow is:

```text
Content with Royalty OS metadata
  ↓
AI retrieval or reference
  ↓
Royalty Trace Event
  ↓
Verification
  ↓
Attribution scoring
  ↓
Allocation readiness status
  ↓
Allocation Trigger
  ↓
Human or multi-party review
  ↓
Allocation Layer
```

A simplified version:

```text
Evidence first.
Review second.
Distribution third.
```

---

## Core Schemas

This repository currently defines two core schemas.

```text
schemas/royalty-trace-event-v3.0.schema.json
schemas/royalty-allocation-trigger-v3.0.schema.json
```

### Royalty Trace Event

A **Royalty Trace Event** records one meaningful instance of AI usage.

It may describe:

- Direct quote
- Factual grounding
- Concept reference
- Structural influence
- Style reference
- Summary
- Translation
- Paraphrase
- Training signal
- Evaluation reference
- note/RAG-style reference experiment

Schema:

```text
schemas/royalty-trace-event-v3.0.schema.json
```

### Royalty Allocation Trigger

A **Royalty Allocation Trigger** is generated when one or more Trace Events become strong enough to justify downstream allocation review.

It does not execute payment.

It says:

```text
These trace events may deserve allocation review.
```

Schema:

```text
schemas/royalty-allocation-trigger-v3.0.schema.json
```

---

## Example Trace Event

```json
{
  "schema_version": "3.0",
  "trace_id": "trace_2026_05_royalty_os_structural_0001",
  "content_os_id": "royalty-os:jp:example:trace-layer-001",
  "timestamp": "2026-05-27T10:30:00+09:00",
  "actor": {
    "ai_model_id": "example-rag-agent-v1",
    "provider_id": "example-provider",
    "deployment_context": "rag",
    "system_role": "generator"
  },
  "retrieval": {
    "retrieval_score": 0.92,
    "retrieval_granularity": "structure",
    "retrieval_method": "hybrid_search"
  },
  "usage": {
    "usage_type": "structural_influence",
    "citation_visible_to_user": false,
    "human_visible_use": true
  },
  "permission": {
    "permission_scope": "allow_reference",
    "permission_status": "valid"
  },
  "verification": {
    "watermark_detected": true,
    "c2pa_manifest_detected": true,
    "soft_binding_resolved": true,
    "retrieval_log_confirmed": true,
    "outlier_origin_detected": true,
    "verification_confidence": 0.89
  },
  "attribution": {
    "influence_estimate": 0.76,
    "origin_score": 0.94,
    "attribution_confidence": 0.82,
    "allocation_readiness": "trigger_candidate",
    "attribution_method": "hybrid"
  }
}
```

---

## Trace Granularity

Trace events may be recorded at different levels of granularity.

```text
token
sentence
paragraph
section
document
concept
structure
dataset
unknown
```

Direct quotation often occurs at sentence or paragraph level.

Conceptual influence may occur at concept level.

Structural influence may occur at structure level.

This allows the Trace Layer to record both visible and non-visible forms of AI usage.

---

## Usage Types

The current schema supports the following usage types:

```text
direct_quote
factual_grounding
concept_reference
structural_influence
style_reference
summary
translation
paraphrase
training_signal
evaluation_reference
other
```

This distinction is important because AI systems do not only quote text.

They may also reuse:

- Concepts
- Frameworks
- Classifications
- Structural patterns
- Original terminology
- Reasoning architectures

Royalty OS v3.0 is especially concerned with concept-level and structure-level traces.

---

## Outlier Origin Detection

Outlier Origin Detection is one of the distinctive features of Royalty OS Trace Layer v3.0.

It identifies unusually original concepts, structures, or frameworks that may function as origin points for later AI-generated outputs.

Examples include:

- Newly coined terms
- Original theoretical structures
- Unique combinations of fields
- High-density conceptual architectures
- Rare structural patterns

Outlier detection does not automatically prove ownership.

It marks the trace as high-priority evidence.

```text
Outlier detection = high-priority evidence
Outlier detection ≠ final ownership proof
```

See:

```text
docs/outlier-origin-detection.md
```

---

## note/RAG Experiment

This repository includes an experimental note/RAG workflow.

The experiment explores whether a public article with machine-readable metadata can be represented as a traceable AI reference event.

The minimal flow is:

```text
note-style article
  ↓
Royalty OS Metadata block
  ↓
RAG retrieval or AI reference
  ↓
Royalty Trace Event
  ↓
Allocation Trigger candidate
```

This is not a claim that note or any external platform currently implements this specification.

It is a social proof and prototyping model for AI-era traceability.

Relevant files:

```text
docs/note-rag-experiment-notes.md
examples/trace-event.note-rag-reference.example.json
```

Example metadata block:

```yaml
Royalty OS Metadata:
  os_id: "royalty-os:jp:samuraiwriter7:example-article-001"
  title: "Example Article Title"
  author_id: "royalty-os:creator:jp:samuraiwriter7"
  permission_scope: "allow_reference"
  preferred_usage:
    - concept_reference
    - structural_influence
    - factual_grounding
  attribution_request: "cite_origin_when_possible"
  trace_priority: "high"
  version: "1.0"
  related_repository: "SamuraiWriter7/royalty-os-trace-layer-v3.0"
```

The purpose is to show that AI reference activity can be:

```text
visible
structured
privacy-aware
reviewable
allocation-ready
```

---

## Allocation Readiness

The Trace Layer does not distribute value directly.

Instead, it assigns an `allocation_readiness` status.

```text
not_ready
review_required
trigger_candidate
ready
```

Meaning:

| Status | Meaning |
|---|---|
| `not_ready` | Evidence is weak, incomplete, or unsuitable |
| `review_required` | Human or multi-party review is needed |
| `trigger_candidate` | The trace may justify an allocation trigger |
| `ready` | The trace is structured enough for downstream allocation processing |

The Allocation Layer should treat these values as signals, not final commands.

---

## Allocation Trigger

An Allocation Trigger is the bridge between Trace evidence and Allocation review.

Example:

```json
{
  "schema_version": "3.0",
  "trigger_id": "allocation_trigger_2026_05_royalty_os_0001",
  "trigger_type": "aggregated_trace_events",
  "source_trace_events": [
    {
      "trace_id": "trace_2026_05_royalty_os_structural_0001",
      "content_os_id": "royalty-os:jp:example:trace-layer-001",
      "usage_type": "structural_influence",
      "allocation_readiness": "trigger_candidate",
      "influence_estimate": 0.76,
      "origin_score": 0.94,
      "verification_confidence": 0.89
    }
  ],
  "allocation_candidate": {
    "candidate_id": "allocation_candidate_2026_05_royalty_os_0001",
    "recipient_os_id": "royalty-os:creator:jp:example",
    "content_os_id": "royalty-os:jp:example:trace-layer-001",
    "allocation_basis": "structural_influence",
    "candidate_score": 0.91,
    "recommended_action": "request_review",
    "suggested_allocation_band": "medium"
  }
}
```

The trigger does not execute payment.

It signals that review may be justified.

---

## Repository Structure

```text
royalty-os-trace-layer-v3.0/
  README.md
  LICENSE
  CITATION.cff
  CHANGELOG.md

  schemas/
    royalty-trace-event-v3.0.schema.json
    royalty-allocation-trigger-v3.0.schema.json

  examples/
    trace-event.structural-influence.example.json
    trace-event.concept-reference.example.json
    trace-event.direct-quote.example.json
    trace-event.outlier-origin.example.json
    trace-event.note-rag-reference.example.json
    allocation-trigger.example.json

  docs/
    architecture-overview.md
    relationship-to-allocation-layer.md
    outlier-origin-detection.md
    privacy-and-compliance-notes.md
    note-rag-experiment-notes.md

  .github/
    workflows/
      validate-schemas.yml
```

---

## Start Here

Recommended reading order:

1. `README.md`
2. `docs/architecture-overview.md`
3. `schemas/royalty-trace-event-v3.0.schema.json`
4. `examples/trace-event.structural-influence.example.json`
5. `examples/trace-event.concept-reference.example.json`
6. `examples/trace-event.direct-quote.example.json`
7. `examples/trace-event.outlier-origin.example.json`
8. `docs/note-rag-experiment-notes.md`
9. `examples/trace-event.note-rag-reference.example.json`
10. `schemas/royalty-allocation-trigger-v3.0.schema.json`
11. `examples/allocation-trigger.example.json`
12. `docs/relationship-to-allocation-layer.md`
13. `docs/outlier-origin-detection.md`
14. `docs/privacy-and-compliance-notes.md`

---

## Key Documents

| Document | Purpose |
|---|---|
| `docs/architecture-overview.md` | Explains the full Trace Layer architecture |
| `docs/relationship-to-allocation-layer.md` | Explains how Trace connects to Allocation without directly distributing value |
| `docs/outlier-origin-detection.md` | Defines the v3.0 origin-detection concept |
| `docs/privacy-and-compliance-notes.md` | Provides privacy and compliance design notes |
| `docs/note-rag-experiment-notes.md` | Describes an experimental note/RAG workflow for social proof and trace validation |

---

## Examples

| Example | Purpose |
|---|---|
| `trace-event.structural-influence.example.json` | AI reuses a framework, architecture, or structural pattern |
| `trace-event.concept-reference.example.json` | AI references an original concept or coined term |
| `trace-event.direct-quote.example.json` | AI directly quotes a registered source fragment |
| `trace-event.outlier-origin.example.json` | AI references a statistically distinctive origin signal |
| `trace-event.note-rag-reference.example.json` | A note-style article is retrieved in a RAG-like environment and traced as a concept or structure reference |
| `allocation-trigger.example.json` | Trace events are converted into an allocation-review candidate |

---

## Schema Validation

This repository includes a GitHub Actions workflow for schema validation.

```text
.github/workflows/validate-schemas.yml
```

The workflow validates:

```text
schemas/royalty-trace-event-v3.0.schema.json
  ├─ examples/trace-event.structural-influence.example.json
  ├─ examples/trace-event.concept-reference.example.json
  ├─ examples/trace-event.direct-quote.example.json
  ├─ examples/trace-event.outlier-origin.example.json
  └─ examples/trace-event.note-rag-reference.example.json

schemas/royalty-allocation-trigger-v3.0.schema.json
  └─ examples/allocation-trigger.example.json
```

Local validation can be performed with Python and `jsonschema`.

```bash
python -m pip install jsonschema
```

The GitHub Actions workflow contains the validation script directly.

---

## Privacy Principles

Royalty OS Trace Layer v3.0 should be privacy-aware by design.

Recommended defaults:

```json
{
  "user_prompt_stored": false,
  "user_identity_stored": false,
  "anonymized_session": true,
  "raw_content_stored": false,
  "privacy_mode": "hash_only"
}
```

The design principle is:

```text
Make AI usage traceable without making people traceable.
```

The Trace Layer should record content usage evidence without becoming a surveillance layer.

See:

```text
docs/privacy-and-compliance-notes.md
```

---

## Relationship to RAG Systems

RAG systems are one of the most important target environments for this specification.

In a RAG workflow, an AI system retrieves documents or fragments before producing an answer.

Royalty OS Trace Layer v3.0 records that retrieval as a traceable event.

Example:

```text
User asks a question
  ↓
RAG system retrieves source content
  ↓
Model generates answer
  ↓
Trace event records source, usage, permission, and influence
```

This makes AI reference activity visible and auditable.

The note/RAG experiment is a lightweight social proof model for this direction.

See:

```text
docs/note-rag-experiment-notes.md
```

---

## Relationship to C2PA-style Provenance

Royalty OS Trace Layer v3.0 can work with provenance metadata systems.

C2PA-style manifests may provide:

- Content identity
- Creator or publisher metadata
- Edit history
- Manifest references
- Asset provenance
- External binding records

Royalty OS extends this idea toward AI usage traceability.

Example extension:

```yaml
royalty:
  os_id: "royalty-os:example:content:001"
  permission_scope: "allow_reference"
  version: "3.0"
  trace_priority: "high"
```

C2PA-style provenance and Royalty OS Trace are related but not identical:

```text
C2PA-style provenance = where the content came from
Royalty OS Trace = how AI used the content
```

---

## Relationship to Watermarking

Watermarking may help verify whether content was generated, transformed, or derived from a known source.

However, watermarking alone is not sufficient.

Royalty OS Trace Layer v3.0 uses multi-signal verification.

```text
Watermark
  + Manifest
  + Retrieval Log
  + Fragment Hash
  + Semantic Similarity
  + Outlier Detection
  = Stronger Trace Evidence
```

This avoids overdependence on a single fragile signal.

---

## Relationship to Review and Dispute Handling

Trace events and allocation triggers may be disputed.

Possible reasons include:

- Similar independent origins
- Prior art
- Incorrect permission status
- False positive similarity
- Incomplete retrieval logs
- Weak attribution confidence
- Multiple competing claims
- Misidentified recipient

For this reason, the architecture assumes review before final allocation.

The Trace Layer preserves evidence.  
The Allocation Layer and review systems decide how that evidence should be handled.

---

## Current Status

```text
Status: Draft
Specification version: Royalty OS Trace Layer v3.0
Repository release stage: v0.1.1 candidate
```

This repository is experimental and intended for specification design, prototyping, and interoperability discussion.

It should not be treated as:

- Legal advice
- A final technical standard
- A complete implementation
- A payment system
- A copyright enforcement system
- A claim of external platform adoption

---

## Future Extensions

Possible future schemas:

```text
schemas/royalty-c2pa-extension-v3.0.schema.json
schemas/royalty-attribution-score-v3.0.schema.json
```

Possible future examples:

```text
examples/trace-event.factual-grounding.example.json
examples/trace-event.summary.example.json
examples/trace-event.training-signal.example.json
examples/allocation-trigger.direct-quote.example.json
examples/allocation-trigger.aggregated-usage.example.json
examples/allocation-trigger.note-rag.example.json
```

Possible future documents:

```text
docs/embedding-layer.md
docs/logging-layer.md
docs/verification-layer.md
docs/relationship-to-c2pa.md
docs/relationship-to-rag-ecosystem.md
docs/relationship-to-rsl.md
docs/evidence-bundle-model.md
docs/dispute-and-review-flow.md
docs/note-metadata-block-template.md
docs/note-rag-experiment-report-template.md
```

Possible implementation components:

- RAG trace adapter
- Trace receipt generator
- Allocation trigger generator
- Evidence bundle builder
- Provider-side trace reporter
- Dashboard data model
- Privacy-preserving proof format
- Multi-provider trace aggregation prototype
- note/RAG experiment report generator

---

## Design Philosophy

Royalty OS Trace Layer v3.0 follows this principle:

```text
No allocation without trace.
No trace without permission.
No permission without machine-readable structure.
```

AI systems increasingly retrieve, summarize, transform, and recombine human knowledge.

The purpose of this repository is to define a minimal but extensible structure for recording that process.

Not every AI reference should become a payment event.  
Not every influence claim should be accepted automatically.  
But meaningful usage should not disappear without evidence.

The Trace Layer exists to preserve that evidence.

---

## License

This repository is released under the MIT License.

See:

```text
LICENSE
```

---

## Citation

If you use or reference this specification, please cite this repository.

See:

```text
CITATION.cff
```

---

## Version History

### v0.1.1-candidate

Adds the note/RAG experiment line.

Includes:

- `docs/note-rag-experiment-notes.md`
- `examples/trace-event.note-rag-reference.example.json`
- Updated schema validation workflow to include the note/RAG trace example
- Updated README sections for Repository Structure, Start Here, Key Documents, Examples, and validation targets

### v0.1.0

Initial repository structure for Royalty OS Trace Layer v3.0.

Includes:

- Royalty Trace Event schema
- Royalty Allocation Trigger schema
- Structural influence trace example
- Concept reference trace example
- Direct quote trace example
- Outlier origin trace example
- Allocation trigger example
- Architecture overview
- Relationship to Allocation Layer notes
- Outlier Origin Detection notes
- Privacy and Compliance notes
- GitHub Actions schema validation workflow

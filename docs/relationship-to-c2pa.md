# Relationship to C2PA

This document explains how Royalty OS Trace Layer v3.0 relates to C2PA-style provenance systems.

The core relationship is:

```text
C2PA-style provenance = where the content came from
Royalty OS Trace = how AI used the content
```

Royalty OS Trace Layer v3.0 is not a replacement for C2PA.

It is a complementary usage-trace layer that can work alongside provenance metadata, manifests, watermarking, retrieval logs, and allocation-review workflows.

---

## 1. Purpose

C2PA-style provenance systems are designed to help establish the origin, history, edits, and authenticity signals of digital content.

Royalty OS Trace Layer v3.0 is designed to record how AI systems retrieve, reference, quote, summarize, transform, or structurally depend on content.

These are related but distinct problems.

```text
Provenance asks:
  Where did this asset come from?

Trace asks:
  How was this asset used by an AI system?
```

Royalty OS Trace Layer v3.0 extends the conversation from content authenticity toward AI-era value circulation.

---

## 2. Layer Difference

The two systems operate at different layers.

```text
C2PA-style provenance
  ↓
Content identity and history

Royalty OS Trace
  ↓
AI usage evidence and allocation readiness
```

C2PA-style metadata may help establish that a content item is authentic or associated with a creator, publisher, or editing history.

Royalty OS Trace records events after that content is accessed or used by AI systems.

---

## 3. Complementary Roles

The relationship can be summarized as follows:

| Layer                 | Main Question                     | Example Data                                                          |
| --------------------- | --------------------------------- | --------------------------------------------------------------------- |
| C2PA-style provenance | Where did this content come from? | creator, tool, edit history, manifest, signature                      |
| Royalty OS Trace      | How did AI use this content?      | retrieval event, usage type, influence estimate, allocation readiness |
| Allocation Layer      | Should value be distributed?      | candidate score, review status, policy decision                       |

Royalty OS Trace may use C2PA-style provenance as one evidence signal, but it does not depend on C2PA alone.

---

## 4. Why C2PA Alone Is Not Enough for Royalty OS

C2PA-style provenance can help identify an asset and its history.

However, Royalty OS also needs to know what happened after AI interaction.

For example:

```text
A content item has valid provenance metadata.
An AI system retrieves it in a RAG pipeline.
The AI output uses its concept without direct quotation.
```

C2PA-style provenance may help identify the source.

But it does not automatically answer:

* Was the asset retrieved by an AI system?
* Was it used in the generated output?
* Was the use a direct quote, concept reference, or structural influence?
* Was the use permitted?
* How strong is the influence signal?
* Should the event become an allocation-review candidate?

These questions belong to the Trace Layer.

---

## 5. Why Royalty OS Trace Should Not Replace C2PA

Royalty OS Trace should not try to replace provenance standards.

Instead, it should use them where appropriate.

C2PA-style metadata can provide:

* Content identity
* Asset provenance
* Manifest references
* Creator or publisher metadata
* Edit history
* Cryptographic binding
* External manifest references
* Trust signals for verification

Royalty OS Trace can use these signals as part of its verification model.

```text
C2PA-style manifest
  ↓
Verification signal
  ↓
Royalty Trace Event
```

---

## 6. Possible Royalty OS Extension Fields

A future C2PA-style extension may include Royalty OS metadata fields.

Example:

```yaml
royalty:
  os_id: "royalty-os:example:content:001"
  permission_scope: "allow_reference"
  version: "3.0"
  trace_priority: "high"
  related_repository: "SamuraiWriter7/royalty-os-trace-layer-v3.0"
```

These fields would not replace existing provenance metadata.

They would provide additional machine-readable signals for AI usage tracing and allocation-readiness workflows.

---

## 7. Suggested Metadata Mapping

Possible mapping between C2PA-style metadata and Royalty OS Trace fields:

| C2PA-style Concept            | Royalty OS Trace Field                            |
| ----------------------------- | ------------------------------------------------- |
| asset identity                | `content_os_id`                                   |
| creator or publisher metadata | `recipient_os_id` or external registry reference  |
| manifest URI                  | `evidence.manifest_uri`                           |
| content binding               | `verification.c2pa_manifest_detected`             |
| claim signature               | `verification.verification_methods`               |
| edit history                  | evidence bundle or provenance reference           |
| external manifest store       | `evidence.manifest_uri`                           |
| asset hash                    | `retrieved_fragment_hash` or evidence bundle hash |

This mapping is illustrative and may evolve.

---

## 8. Trace Event Integration

A Royalty Trace Event may include C2PA-style verification signals.

Example:

```json
{
  "verification": {
    "watermark_detected": true,
    "c2pa_manifest_detected": true,
    "soft_binding_resolved": true,
    "retrieval_log_confirmed": true,
    "verification_confidence": 0.89,
    "verification_methods": [
      "watermark",
      "c2pa_manifest",
      "soft_binding",
      "retrieval_log",
      "fragment_hash"
    ]
  },
  "evidence": {
    "manifest_uri": "https://example.org/manifests/content-001.json"
  }
}
```

In this model, C2PA-style provenance contributes to verification confidence.

It does not decide allocation by itself.

---

## 9. Soft Binding

Royalty OS Trace Layer v3.0 may support soft binding between content and external records.

Soft binding is useful when metadata is not embedded directly in the content or when the content has been transformed, copied, or moved across systems.

Possible soft binding references include:

* External manifest URI
* Registry record
* Content OS ID
* Hash-based reference
* Evidence bundle ID
* Trace receipt bundle
* Provider-side audit record

Example:

```json
{
  "verification": {
    "soft_binding_resolved": true
  },
  "evidence": {
    "manifest_uri": "https://example.org/manifests/royalty-os-content-001.json"
  }
}
```

Soft binding is especially important for AI retrieval environments where content may be chunked, summarized, or indexed.

---

## 10. Relationship to Watermarking

C2PA-style provenance and watermarking are both useful but incomplete alone.

Royalty OS Trace Layer v3.0 assumes multi-signal verification.

```text
C2PA-style manifest
  + Watermark
  + Retrieval log
  + Fragment hash
  + Semantic similarity
  + Outlier detection
  = stronger trace evidence
```

This reduces overdependence on any single signal.

A watermark may help identify content origin or transformation history.

A manifest may help establish provenance.

A retrieval log may confirm actual AI usage.

A semantic or structural comparison may help estimate influence.

All signals together provide stronger evidence than any one signal alone.

---

## 11. Relationship to RAG Systems

C2PA-style provenance can identify content.

RAG logs can record retrieval.

Royalty OS Trace connects both.

Example flow:

```text
Content has C2PA-style provenance metadata
  ↓
Content is indexed in a RAG system
  ↓
RAG system retrieves the content
  ↓
AI output uses the content
  ↓
Royalty Trace Event is generated
  ↓
Allocation Trigger may be generated if evidence is strong
```

This is one of the main integration paths for Royalty OS Trace Layer v3.0.

---

## 12. Relationship to note/RAG Experiment

The note/RAG experiment may begin without C2PA integration.

In early experiments, a public article can include a simple metadata block:

```yaml
Royalty OS Metadata:
  os_id: "royalty-os:jp:samuraiwriter7:example-article-001"
  permission_scope: "allow_reference"
  preferred_usage:
    - concept_reference
    - structural_influence
    - factual_grounding
  trace_priority: "high"
```

This is not a full C2PA manifest.

It is a lightweight social proof mechanism.

Over time, this metadata model may evolve toward a more formal C2PA-style extension.

---

## 13. Proposed Integration Path

A practical integration path may look like this:

```text
Phase 1:
  Human-readable article metadata block

Phase 2:
  Royalty OS Trace Event examples

Phase 3:
  External manifest or registry reference

Phase 4:
  C2PA-style provenance mapping

Phase 5:
  Royalty OS extension fields

Phase 6:
  Allocation Trigger integration
```

This avoids premature standardization.

It begins with visible metadata and moves gradually toward interoperable provenance and trace infrastructure.

---

## 14. Possible Future Schema

A future schema may define Royalty OS metadata fields for C2PA-style manifests.

Possible file:

```text
schemas/royalty-c2pa-extension-v3.0.schema.json
```

Possible scope:

* `royalty.os_id`
* `royalty.permission_scope`
* `royalty.trace_priority`
* `royalty.preferred_usage`
* `royalty.attribution_request`
* `royalty.related_repository`
* `royalty.version`
* `royalty.policy_uri`

This schema should remain small and interoperable.

Its purpose should be to connect provenance metadata to usage tracing, not to overload C2PA with allocation logic.

---

## 15. Allocation Should Remain Separate

Even if C2PA-style metadata identifies the source, allocation should not be automatic.

The flow should remain:

```text
Provenance signal
  ↓
Trace Event
  ↓
Verification
  ↓
Allocation Readiness
  ↓
Allocation Trigger
  ↓
Review
  ↓
Allocation Layer
```

This preserves the core Royalty OS principle:

```text
Trace = evidence
Review = judgment
Allocation = distribution
```

C2PA-style metadata can strengthen the evidence.

It should not replace review or policy decisions.

---

## 16. Limitations and Cautions

C2PA-style provenance should be treated as an important signal, not an absolute guarantee.

Potential limitations include:

* Metadata may be stripped
* Manifest references may break
* Claims may be incomplete
* Identity assertions may require trust infrastructure
* Asset transformation may complicate binding
* Provenance does not prove meaningful AI usage
* Provenance does not prove allocation eligibility
* Valid provenance may coexist with weak usage evidence

For Royalty OS, this means provenance should be combined with retrieval and usage evidence.

---

## 17. Minimal Contract Between Layers

A minimal contract between C2PA-style provenance and Royalty OS Trace may be:

```text
C2PA-style provenance provides:
  - content identity
  - manifest reference
  - provenance assertions
  - cryptographic or trust signals

Royalty OS Trace provides:
  - AI retrieval record
  - usage type
  - permission status
  - verification confidence
  - attribution signals
  - allocation readiness
```

Together, they can support a stronger AI-era content accountability architecture.

---

## 18. Example Combined Flow

```text
Creator publishes content
  ↓
Content receives provenance metadata
  ↓
Royalty OS metadata identifies permission and trace priority
  ↓
AI system retrieves the content
  ↓
Retrieval log confirms access
  ↓
Trace Event records usage
  ↓
Verification checks manifest, watermark, log, and similarity
  ↓
Attribution estimates influence
  ↓
Allocation readiness is assigned
  ↓
Allocation Trigger may be created
  ↓
Review layer decides next action
```

This flow connects content provenance with AI usage accountability.

---

## 19. Recommended Design Principle

Royalty OS should treat C2PA-style systems as a provenance foundation, not as the entire royalty infrastructure.

Recommended principle:

```text
Use provenance to identify the source.
Use trace to record AI usage.
Use review to judge allocation.
```

This keeps each layer clear, auditable, and interoperable.

---

## 20. Summary

C2PA-style provenance and Royalty OS Trace Layer v3.0 are complementary.

C2PA-style systems help answer:

```text
Where did this content come from?
```

Royalty OS Trace helps answer:

```text
How did AI use this content?
```

Allocation systems then ask:

```text
Should value be distributed, and how?
```

Royalty OS Trace Layer v3.0 should therefore integrate with C2PA-style metadata where useful, while preserving a separate usage-trace and allocation-readiness layer.

In short:

```text
Provenance identifies.
Trace records.
Review judges.
Allocation distributes.
```

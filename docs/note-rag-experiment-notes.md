# Note RAG Experiment Notes

This document describes an experimental design for connecting note-style publishing, RAG retrieval, Royalty OS Trace Events, and Allocation Triggers.

The purpose is to explore how public articles, essays, and structured knowledge posts may become traceable in AI retrieval environments without requiring immediate platform-level integration.

This is an experimental design note.

It does not claim that note, AI providers, or any external platform currently implements this specification.

---

## 1. Purpose

Royalty OS Trace Layer v3.0 defines machine-readable trace events for AI usage.

This document applies that structure to a possible note/RAG experiment.

The core question is:

```text
Can a public article become traceable when it is retrieved, referenced, summarized, or structurally reused by an AI system?
```

The experiment focuses on a minimal flow:

```text
note article
  ↓
Royalty OS Metadata block
  ↓
RAG retrieval or AI reference
  ↓
Royalty Trace Event
  ↓
Allocation Trigger candidate
```

The goal is not automatic payment.

The goal is to test whether AI reference activity can be represented as structured evidence.

---

## 2. Why note-style Publishing Matters

note-style publishing is important because it often contains:

- First-person knowledge
- Original essays
- Creator-specific concepts
- Emerging frameworks
- Structured opinions
- Long-form thought records
- Experimental theory
- Public intellectual work

These works may be referenced by AI systems not only as direct quotations, but also as:

- Concept references
- Factual grounding
- Summary sources
- Structural influence
- Framework reuse
- Outlier origin signals

Royalty OS Trace Layer v3.0 is designed to preserve these signals.

---

## 3. Experimental Scope

This experiment does not require full platform integration.

It can begin with a lightweight metadata block placed at the end of a public article.

Example:

```yaml
Royalty OS Metadata:
  os_id: "royalty-os:jp:samuraiwriter7:example-article-001"
  title: "Example Article Title"
  permission_scope: "allow_reference"
  preferred_usage:
    - concept_reference
    - structural_influence
    - factual_grounding
  attribution_request: "cite_origin_when_possible"
  trace_priority: "high"
  related_repository: "SamuraiWriter7/royalty-os-trace-layer-v3.0"
```

This block is not a legal license by itself.

It is an experimental machine-readable signal for AI systems, RAG pipelines, search systems, and audit tools.

---

## 4. Experimental Flow

The basic experiment flow is:

```text
1. Publish an article with Royalty OS Metadata.
2. Index or retrieve the article in a RAG-like environment.
3. Record when the article is retrieved.
4. Classify how the article was used.
5. Generate a Royalty Trace Event.
6. Determine allocation_readiness.
7. Generate an Allocation Trigger if thresholds are met.
```

Expanded flow:

```text
Article publication
  ↓
Metadata detection
  ↓
RAG retrieval
  ↓
Usage classification
  ↓
Verification
  ↓
Attribution scoring
  ↓
Trace Event creation
  ↓
Allocation Trigger candidate
```

---

## 5. Article Metadata Block

A minimal article-level metadata block may include:

```yaml
Royalty OS Metadata:
  os_id: "royalty-os:jp:samuraiwriter7:royalty-os-trace-layer-v3.0"
  title: "Royalty OS Trace Layer v3.0"
  author_id: "royalty-os:creator:jp:samuraiwriter7"
  permission_scope: "allow_reference"
  preferred_usage:
    - concept_reference
    - structural_influence
    - factual_grounding
  attribution_request: "cite_origin_when_possible"
  trace_priority: "high"
  version: "3.0"
  related_repository: "SamuraiWriter7/royalty-os-trace-layer-v3.0"
```

This metadata block helps AI systems and audit tools identify:

- The content identity
- The creator or rights holder
- The intended permission scope
- The preferred attribution behavior
- The trace priority
- The related specification repository

---

## 6. Suggested Metadata Fields

| Field | Purpose |
|---|---|
| `os_id` | Unique Royalty OS content identifier |
| `title` | Human-readable article title |
| `author_id` | Creator or rights holder identifier |
| `permission_scope` | Declared usage permission |
| `preferred_usage` | Expected or permitted AI usage categories |
| `attribution_request` | Preferred attribution behavior |
| `trace_priority` | Suggested trace importance |
| `version` | Metadata or content version |
| `related_repository` | Related GitHub repository or specification |

---

## 7. Permission Scope

Possible permission scopes:

```text
allow_reference
allow_summary
allow_quote
allow_rag
allow_indexing
restricted
deny
unknown
```

For early experiments, recommended default:

```text
allow_reference
```

This means:

```text
The article may be referenced by AI systems,
but meaningful usage should be traceable and attribution should be preferred where possible.
```

---

## 8. Preferred Usage

The article may declare preferred usage categories.

Example:

```yaml
preferred_usage:
  - concept_reference
  - structural_influence
  - factual_grounding
```

These values may map to the `usage_type` field in the Royalty Trace Event schema.

Possible mappings:

| Metadata Usage | Trace Event `usage_type` |
|---|---|
| `concept_reference` | `concept_reference` |
| `structural_influence` | `structural_influence` |
| `factual_grounding` | `factual_grounding` |
| `direct_quote` | `direct_quote` |
| `summary` | `summary` |

---

## 9. RAG Retrieval Scenario

A RAG system retrieves an article containing Royalty OS Metadata.

Example scenario:

```text
User asks a question about AI-era creator compensation.
The RAG system retrieves a note article about Royalty OS.
The AI answer does not quote the article directly.
However, it uses the article's conceptual structure.
```

This may generate:

```json
{
  "usage_type": "structural_influence",
  "retrieval_granularity": "structure",
  "allocation_readiness": "trigger_candidate"
}
```

---

## 10. Trace Event Generation

When an article is retrieved or referenced, a trace event may be generated.

Relevant schema:

```text
schemas/royalty-trace-event-v3.0.schema.json
```

Possible trace event type:

```text
trace-event.note-rag-reference.example.json
```

The event should record:

- Article OS ID
- Retrieval score
- Retrieval granularity
- Usage type
- Permission status
- Verification confidence
- Influence estimate
- Origin score
- Allocation readiness
- Privacy mode

---

## 11. Example Trace Interpretation

If an article is directly quoted:

```text
usage_type = direct_quote
allocation_readiness = ready
```

If an article is used as factual grounding:

```text
usage_type = factual_grounding
allocation_readiness = review_required
```

If an original concept is referenced:

```text
usage_type = concept_reference
allocation_readiness = trigger_candidate
```

If a framework or architecture is structurally reused:

```text
usage_type = structural_influence
allocation_readiness = trigger_candidate
```

If the article contains a highly distinctive concept:

```text
outlier_origin_detected = true
origin_score = high
allocation_readiness = trigger_candidate
```

---

## 12. Allocation Trigger Scenario

If one or more trace events become strong enough, an Allocation Trigger may be generated.

Relevant schema:

```text
schemas/royalty-allocation-trigger-v3.0.schema.json
```

Example flow:

```text
note article retrieved repeatedly
  ↓
concept_reference and structural_influence detected
  ↓
origin_score and verification_confidence exceed threshold
  ↓
allocation_readiness becomes trigger_candidate
  ↓
Allocation Trigger is generated
  ↓
human or multi-party review begins
```

The Allocation Trigger does not execute payment.

It only signals that allocation review may be justified.

---

## 13. Experimental Thresholds

A simple experimental threshold model may use:

```json
{
  "minimum_retrieval_score": 0.75,
  "minimum_influence_estimate": 0.70,
  "minimum_origin_score": 0.85,
  "minimum_verification_confidence": 0.80
}
```

Suggested interpretation:

| Signal | Meaning |
|---|---|
| High retrieval score | The article was strongly relevant to the query |
| High influence estimate | The article likely influenced the output |
| High origin score | The article contains distinctive origin-like concepts |
| High verification confidence | Evidence is strong enough for review |

These thresholds are experimental.

They should not be treated as universal constants.

---

## 14. Outlier Origin in note Articles

note-style articles may contain original concepts before those concepts become common.

Outlier Origin Detection is useful when an article includes:

- A coined term
- A new framework
- A unique classification
- A distinctive theory
- A rare conceptual combination
- A specific architecture diagram or structure
- A repeated phrase that later appears in AI-generated explanations

Example:

```text
A creator introduces a new AI governance framework.
Later, AI systems explain similar concepts using the same structure,
but without direct quotation.
```

This may justify an outlier-origin trace candidate.

---

## 15. Privacy Considerations

The experiment should avoid storing raw user prompts.

Recommended privacy settings:

```json
{
  "user_prompt_stored": false,
  "user_identity_stored": false,
  "anonymized_session": true,
  "raw_content_stored": false,
  "privacy_mode": "hash_only"
}
```

The experiment should trace article usage, not end-user behavior.

Core principle:

```text
Trace the work.
Protect the person.
```

---

## 16. What This Experiment Can Prove

This experiment can help demonstrate:

- Public articles can include machine-readable usage metadata.
- AI/RAG retrieval can be represented as structured trace events.
- Concept references can be separated from direct quotes.
- Structural influence can be represented as a reviewable signal.
- Outlier origin detection can identify high-priority origin candidates.
- Trace events can generate allocation-review candidates.
- Privacy-aware trace logging is possible without storing raw prompts.

---

## 17. What This Experiment Cannot Prove

This experiment cannot prove by itself:

- Legal authorship
- Copyright infringement
- Final allocation eligibility
- Platform adoption
- AI provider compliance
- Guaranteed attribution
- Guaranteed payment
- Universal standardization

It is a prototype design for traceability, not a complete legal or economic system.

---

## 18. Minimal Prototype

A minimal prototype may include:

```text
1. Article metadata block
2. Manual or scripted retrieval simulation
3. Trace Event JSON generation
4. Allocation Trigger JSON generation
5. Schema validation
6. Human-readable experiment report
```

No platform integration is required at the first stage.

The prototype can be run manually using example articles and simulated RAG retrieval logs.

---

## 19. Possible File Additions

Future files may include:

```text
examples/trace-event.note-rag-reference.example.json
examples/allocation-trigger.note-rag.example.json
docs/note-metadata-block-template.md
docs/note-rag-experiment-report-template.md
```

These files would make the experiment more concrete.

---

## 20. Suggested Experiment Steps

Recommended sequence:

```text
1. Select one public article.
2. Add a Royalty OS Metadata block.
3. Define the article's content_os_id.
4. Simulate or record a RAG retrieval event.
5. Classify the usage type.
6. Generate a Royalty Trace Event.
7. Validate it against the schema.
8. If thresholds are met, generate an Allocation Trigger.
9. Validate the Allocation Trigger.
10. Write a short experiment report.
```

---

## 21. Example Article Metadata Template

```yaml
Royalty OS Metadata:
  os_id: "royalty-os:jp:samuraiwriter7:article-001"
  title: "ARTICLE_TITLE"
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

---

## 22. Example Experiment Record

A simple experiment record may look like:

```yaml
experiment_id: "note-rag-experiment-001"
article_os_id: "royalty-os:jp:samuraiwriter7:article-001"
article_platform: "note"
retrieval_context: "simulated_rag"
usage_type: "concept_reference"
retrieval_score: 0.88
influence_estimate: 0.72
origin_score: 0.91
verification_confidence: 0.84
allocation_readiness: "trigger_candidate"
result: "allocation_trigger_candidate_generated"
```

This record can later be converted into a formal Trace Event.

---

## 23. Relationship to C2PA Extension

This note experiment can later support a C2PA-style extension.

The relationship is:

```text
note metadata block
  ↓
experimental content identity
  ↓
Royalty OS Trace Event
  ↓
evidence of usage trace need
  ↓
future C2PA-style metadata extension
```

C2PA-style metadata can help identify content provenance.

Royalty OS Trace Events help record AI usage after retrieval or reference.

They are related but not identical.

```text
C2PA-style provenance = where the content came from
Royalty OS Trace = how AI used the content
```

---

## 24. Relationship to Social Proof

The note/RAG experiment creates social proof.

It can show that:

```text
AI reference activity can be described.
AI reference activity can be structured.
AI reference activity can be validated.
AI reference activity can become reviewable.
```

This is useful before attempting broader standardization.

A small working experiment is stronger than a large abstract proposal.

---

## 25. Recommended Output

The experiment should produce:

```text
1. Article with Royalty OS Metadata
2. Trace Event JSON
3. Allocation Trigger JSON
4. Validation result
5. Short experiment report
```

This package becomes a minimal proof-of-concept.

---

## 26. Design Principle

The note/RAG experiment follows this principle:

```text
Start with visible metadata.
Convert retrieval into trace.
Convert trace into reviewable evidence.
Do not jump directly to payment.
```

This protects the credibility of Royalty OS.

---

## 27. Summary

The note/RAG experiment is the first social proof layer for Royalty OS Trace Layer v3.0.

It does not require full platform adoption.

It begins with:

```text
public article
  + machine-readable metadata
  + simulated or observed retrieval
  + trace event
  + allocation trigger candidate
```

Its purpose is to show that AI-era content usage can be made visible, structured, privacy-aware, and reviewable.

In short:

```text
Publish the idea.
Mark the origin.
Trace the reference.
Review before allocation.
```

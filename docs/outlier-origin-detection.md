# Outlier Origin Detection

This document explains the concept of **Outlier Origin Detection** in Royalty OS Trace Layer v3.0.

Outlier Origin Detection is a mechanism for identifying unusually original concepts, frameworks, structures, or semantic patterns that may act as origin points for later AI-generated outputs.

It is one of the distinctive features of Royalty OS Trace Layer v3.0.

---

## 1. Purpose

AI systems do not only quote text.

They may also absorb, reuse, summarize, transform, or structurally imitate:

- Concepts
- Terms
- Frameworks
- Classifications
- Argument structures
- Design patterns
- Philosophical models
- System architectures

Traditional citation systems are relatively good at handling direct quotes.

They are much weaker at handling cases where an AI system does not quote a source but still depends on a distinctive conceptual structure.

Outlier Origin Detection addresses this gap.

Its purpose is to identify cases where a source appears to function as a meaningful origin signal even when no direct quotation is present.

---

## 2. Core Idea

The core idea is:

```text
Some ideas are not merely similar.
They are structurally distinctive.

An outlier origin is a concept, structure, or framework that differs significantly from common language patterns or ordinary topic-level similarity.

Examples may include:

Newly coined terms
Unique theoretical frameworks
Rare conceptual combinations
Original system architectures
High-density explanatory models
Unusual classification structures
Repeatedly reused but rarely attributed conceptual patterns

In Royalty OS, these are treated as high-priority trace candidates.

3. Why It Matters

AI systems often flatten originality.

A distinctive concept may enter an AI system through retrieval, summarization, or training-like exposure.
Later, the AI may produce outputs that reflect the concept without quoting the original source.

In such cases, normal citation detection may fail.

For example:

Source:
  A creator proposes an original framework.

AI output:
  The framework is reproduced as a general explanation,
  but the creator is not quoted or cited.

This is not a direct quote.

But it may still be meaningful usage.

Outlier Origin Detection helps make this kind of usage visible.

4. What Outlier Origin Detection Is Not

Outlier Origin Detection does not automatically prove:

Legal authorship
Copyright infringement
Exclusive ownership
Final attribution
Final allocation eligibility
Intentional copying
Direct causal influence

It is not a legal judgment.

It is an evidence signal.

Outlier detection = high-priority evidence
Outlier detection ≠ final ownership proof

This distinction is critical.

5. Position in the Trace Layer

Outlier Origin Detection belongs mainly to the Verification Layer and Attribution signal layer.

Embedding Layer
  ↓
Logging Layer
  ↓
Verification Layer
      └─ Outlier Origin Detection
  ↓
Attribution
  ↓
Allocation Readiness

It helps determine whether a trace event should receive higher review priority.

6. Relationship to Trace Events

In the Royalty Trace Event schema, the relevant field is:

{
  "verification": {
    "outlier_origin_detected": true
  }
}

Additional supporting fields include:

{
  "attribution": {
    "origin_score": 0.97,
    "influence_estimate": 0.73,
    "attribution_confidence": 0.81,
    "allocation_readiness": "trigger_candidate"
  }
}

A high origin_score suggests that the referenced content may contain a distinctive origin signal.

A high influence_estimate suggests that the signal may have meaningfully affected the output or system behavior.

7. Example

Example file:

examples/trace-event.outlier-origin.example.json

Conceptual summary:

An AI system retrieves a source containing a distinctive concept.
The generated output does not quote the source.
However, semantic and structural analysis suggest that the output depends on the source concept.
The source is detected as an outlier origin.
The trace event becomes a trigger candidate for allocation review.

This is one of the key cases Royalty OS v3.0 is designed to handle.

8. Detection Signals

Outlier Origin Detection may use multiple signals.

Possible signals include:

Term rarity
Concept rarity
Structural uniqueness
Semantic distance from common corpora
Low frequency in public datasets
High similarity to a registered source
Repeated appearance across AI outputs after source exposure
Unusual combination of domains
Distinctive naming patterns
Distinctive explanatory architecture
Structure fingerprint similarity
Retrieval log confirmation

No single signal is sufficient by itself.

The system should prefer multi-signal detection.

Rarity
  + Structure
  + Retrieval Log
  + Semantic Similarity
  + Source Registration
  = Stronger Outlier Origin Evidence
9. Suggested Scoring Model

A simple experimental model may combine several scores.

origin_score =
  term_rarity_score
  + structure_uniqueness_score
  + semantic_specificity_score
  + retrieval_confirmation_score
  + prior_registration_score

Normalized form:

origin_score = weighted_sum(signals) between 0.0 and 1.0

Example weights:

{
  "term_rarity_score": 0.20,
  "structure_uniqueness_score": 0.25,
  "semantic_specificity_score": 0.20,
  "retrieval_confirmation_score": 0.20,
  "prior_registration_score": 0.15
}

These weights are experimental.

They should be treated as policy-specific and implementation-dependent.

10. Suggested Thresholds

Example threshold model:

{
  "outlier_candidate": 0.70,
  "high_priority_origin": 0.85,
  "allocation_trigger_candidate": 0.90
}

Suggested interpretation:

Score Range	Interpretation
0.00 - 0.49	Weak or ordinary signal
0.50 - 0.69	Possible conceptual similarity
0.70 - 0.84	Outlier candidate
0.85 - 0.94	High-priority origin signal
0.95 - 1.00	Strong outlier origin signal

These thresholds should not be universal.

Different domains may require different thresholds.

11. Domain Sensitivity

Outlier detection must be domain-aware.

A phrase that appears rare in one domain may be common in another.

For example:

"trace"

may be ordinary in software engineering.

But a phrase like:

"AI reference as value circulation"

may be more distinctive in a royalty-oriented AI infrastructure context.

Therefore, outlier detection should consider:

Domain
Language
Publication context
Time period
Prior art
Corpus coverage
Cultural and regional context
12. Time Sensitivity

Outlier origin detection should account for time.

A concept may be original at one point and common later.

Therefore, the system should record:

First known registration time
First indexed appearance
First retrieved use
First observed AI output reuse
Later diffusion patterns

A useful model is:

Origin time
  ↓
Early diffusion
  ↓
Repeated AI reference
  ↓
Normalization into common language

Once a concept becomes common, its outlier score may decay.

This does not erase the origin signal.
It means the system should distinguish between origin detection and later common reuse.

13. Relationship to Structural Influence

Outlier Origin Detection often overlaps with Structural Influence.

However, they are not identical.

Concept	Meaning
structural_influence	The output reuses a framework, architecture, or pattern
outlier_origin	The source appears unusually distinctive and origin-like

A trace event may involve both:

{
  "usage": {
    "usage_type": "structural_influence"
  },
  "verification": {
    "outlier_origin_detected": true
  },
  "attribution": {
    "origin_score": 0.94
  }
}

This is a strong review candidate.

14. Relationship to Concept Reference

Outlier Origin Detection may also apply to concept references.

Example:

A model uses a coined term or original concept introduced by a specific source.
The term is not quoted as text, but the concept is clearly reused.

This may produce:

{
  "usage": {
    "usage_type": "concept_reference"
  },
  "verification": {
    "outlier_origin_detected": true
  }
}

This is especially important for philosophical, theoretical, and system-design content.

15. Relationship to Allocation

Outlier Origin Detection does not directly allocate value.

It may affect:

Review priority
Allocation readiness
Candidate score
Suggested allocation basis
Dispute review priority

Typical flow:

Outlier Origin Detection
  ↓
High origin_score
  ↓
allocation_readiness = trigger_candidate
  ↓
Allocation Trigger
  ↓
Review Gate
  ↓
Allocation Layer

The Allocation Layer should treat outlier origin as a strong signal, not a final command.

16. False Positives

False positives are possible.

A system may incorrectly detect an outlier origin when:

Similar ideas emerged independently
The concept existed in prior art
The source is not the true origin
The corpus is incomplete
The term appears rare only because of limited indexing
The structure is generic but appears unique due to poor comparison data

Therefore, outlier detection must be reviewable.

Recommended safeguards:

Prior art search
Multi-source comparison
Human or multi-party review
Dispute handling
Confidence scoring
Evidence bundle preservation
Time-based source comparison
17. False Negatives

False negatives are also possible.

A system may fail to detect an outlier origin when:

The concept has been heavily paraphrased
The source language has been translated
The structure has been abstracted
The AI output uses only part of the framework
The concept has already diffused widely
The source was not indexed
The watermark or manifest is unavailable

For this reason, the system should not rely only on exact text matching.

It should combine semantic, structural, temporal, and retrieval-based evidence.

18. Evidence Bundle

When an outlier origin signal is detected, the system should preserve an evidence bundle.

Possible contents:

Source content hash
Retrieved fragment hash
Output fragment hash
Retrieval log reference
Manifest URI
Timestamp
Model/provider ID
Similarity report
Structure fingerprint report
Outlier score components
Prior art comparison result
Review notes

The evidence bundle allows later review without exposing unnecessary raw private data.

19. Privacy Considerations

Outlier detection should not require storing raw user prompts.

Recommended privacy practices:

Use anonymized session IDs
Store hashes instead of raw content where possible
Avoid storing direct user identity
Separate creator identity from end-user identity
Preserve only evidence needed for review
Support redaction and aggregation
Allow provider-side logs to remain local where appropriate

The goal is origin traceability, not user surveillance.

20. Implementation Notes

A prototype implementation may include:

1. Register source content or concept metadata.
2. Compute semantic and structural fingerprints.
3. Monitor RAG retrieval or AI reference events.
4. Compare retrieved and generated structures.
5. Estimate rarity and origin-likeness.
6. Assign origin_score.
7. Set outlier_origin_detected when threshold is reached.
8. Create or update a Royalty Trace Event.
9. Generate Allocation Trigger if readiness conditions are met.

This can begin as an offline audit tool before becoming a real-time trace system.

21. Minimal Algorithm Sketch

Pseudo-flow:

input:
  source_record
  retrieved_fragment
  generated_output
  retrieval_log
  reference_corpus

steps:
  compute semantic_similarity
  compute structure_similarity
  compute term_rarity
  compute concept_rarity
  compute retrieval_confirmation
  compute prior_registration_signal
  combine signals into origin_score

if origin_score >= threshold:
  outlier_origin_detected = true
else:
  outlier_origin_detected = false

The result should be stored as part of a trace event.

22. Example Signal Object

Possible future extension:

{
  "outlier_origin": {
    "detected": true,
    "origin_score": 0.97,
    "term_rarity_score": 0.92,
    "structure_uniqueness_score": 0.95,
    "semantic_specificity_score": 0.88,
    "retrieval_confirmation_score": 0.91,
    "prior_registration_score": 0.96,
    "review_priority": "high"
  }
}

This object is not currently required in the core schema, but may be added in a future extension.

23. Recommended Review Priority

Suggested review priority mapping:

Condition	Review Priority
Low origin score, no retrieval confirmation	Low
Moderate origin score, weak evidence	Medium
High origin score, retrieval confirmed	High
High origin score, structural influence detected	Very high
High origin score, repeated AI reuse observed	Critical

This helps review teams focus on the strongest cases.

24. Design Principle

Outlier Origin Detection follows this principle:

Original structures should not vanish into statistical averages.

AI systems tend to compress, generalize, and normalize human knowledge.

Royalty OS Trace Layer v3.0 exists to preserve meaningful origin signals before they disappear into generic AI outputs.

25. Summary

Outlier Origin Detection is a high-priority evidence mechanism for identifying distinctive concepts and structures that may function as origin points in AI-generated outputs.

It does not prove ownership by itself.

It does not allocate value by itself.

It does not replace review.

But it helps the Trace Layer recognize something that ordinary citation systems often miss:

Not all influence appears as quotation.
Some influence appears as structure.
Some structure begins as an outlier.

Royalty OS Trace Layer v3.0 preserves that signal.

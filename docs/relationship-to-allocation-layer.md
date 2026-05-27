# Relationship to Allocation Layer

This document explains how Royalty OS Trace Layer v3.0 connects to the downstream Allocation Layer.

The core principle is simple:

```text
Trace does not allocate.
Trace produces evidence.
Allocation reviews and distributes value.
1. Purpose of This Document

Royalty OS v3.0 separates evidence generation from value distribution.

This separation is essential because AI usage can be complex, probabilistic, and disputable.

The Trace Layer records:

What was retrieved
How it was used
Whether the use was permitted
How strong the evidence is
Whether the event may be ready for allocation review

The Allocation Layer decides:

Whether the evidence is sufficient
Whether review is required
Whether a dispute exists
Whether value should be distributed
How much value should be allocated
Who should receive the allocation
2. Layer Separation

Royalty OS v3.0 is organized as:

Permission Layer
  ↓
Trace Layer
  ↓
Allocation Layer

The Trace Layer sits between permission and allocation.

Permission = Can this content be used?
Trace = Was this content used, and how?
Allocation = Should value be distributed, and to whom?

This separation prevents premature or automatic payment decisions based only on weak signals.

3. Why Trace Must Not Directly Allocate

Trace evidence can be strong, but it is not always final.

AI systems may:

Retrieve a source without using it meaningfully
Use a source indirectly
Paraphrase or summarize a concept
Reuse a structure without direct quotation
Combine multiple sources
Produce outputs influenced by both explicit retrieval and latent model knowledge
Generate false-positive similarity matches

For this reason, Trace Layer outputs should not immediately become payment events.

Instead, they should become allocation candidates.

Trace Event
  ↓
Verification
  ↓
Attribution Signal
  ↓
Allocation Readiness
  ↓
Allocation Trigger
  ↓
Allocation Review
4. Core Objects

The connection between Trace Layer and Allocation Layer is mainly handled by two objects.

Royalty Trace Event
Royalty Allocation Trigger
Royalty Trace Event

Defined by:

schemas/royalty-trace-event-v3.0.schema.json

A Trace Event records one meaningful AI usage event.

It may describe:

Direct quote
Factual grounding
Concept reference
Structural influence
Style reference
Summary
Translation
Paraphrase
Training signal
Evaluation reference
Royalty Allocation Trigger

Defined by:

schemas/royalty-allocation-trigger-v3.0.schema.json

An Allocation Trigger is created when one or more Trace Events become strong enough to justify downstream allocation review.

It does not execute payment.

It says:

These trace events may deserve allocation review.
5. Allocation Readiness

Each Trace Event may include an allocation_readiness field.

Possible values:

not_ready
review_required
trigger_candidate
ready
Meaning
Status	Meaning	Allocation Layer Action
not_ready	Evidence is incomplete or weak	Do not trigger allocation
review_required	Evidence may matter but needs review	Send to review queue
trigger_candidate	Evidence is strong enough to create a trigger candidate	Generate or aggregate trigger
ready	Evidence is structured and highly credible	Prepare for allocation review

The Allocation Layer should treat these values as signals, not final commands.

6. Allocation Trigger Flow

A typical flow looks like this:

Trace Event
  ↓
verification_confidence
  ↓
influence_estimate
  ↓
origin_score
  ↓
allocation_readiness
  ↓
Allocation Trigger
  ↓
Review Gate
  ↓
Allocation Decision

The Allocation Trigger acts as a bridge between evidence and decision.

7. Trigger Conditions

An Allocation Trigger may be generated when one or more conditions are met.

Possible conditions include:

Valid permission
High verification confidence
High influence estimate
High origin score
Direct quote with visible output
Repeated references over time
Aggregated usage above threshold
Outlier origin detection
Structural influence detection
Manual review request
Dispute review request

Example threshold model:

{
  "minimum_influence_estimate": 0.7,
  "minimum_origin_score": 0.9,
  "minimum_verification_confidence": 0.85,
  "minimum_candidate_score": 0.9
}

These thresholds are policy-dependent and should not be treated as universal constants.

8. Allocation Candidate

An Allocation Trigger contains an allocation_candidate object.

This object identifies:

Candidate ID
Recipient OS ID
Content OS ID
Allocation basis
Candidate score
Recommended action
Suggested allocation band

Example:

{
  "candidate_id": "allocation_candidate_2026_05_royalty_os_0001",
  "recipient_os_id": "royalty-os:creator:jp:example",
  "content_os_id": "royalty-os:jp:example:content-001",
  "allocation_basis": "outlier_origin",
  "candidate_score": 0.91,
  "recommended_action": "request_review",
  "suggested_allocation_band": "medium"
}

This is not a final payment instruction.

It is a structured recommendation for the Allocation Layer.

9. Recommended Actions

The Allocation Trigger schema supports the following recommended actions:

no_action
request_review
prepare_allocation
hold_for_dispute_check
aggregate_until_threshold
manual_decision_required
Meaning
Action	Meaning
no_action	No downstream allocation action is recommended
request_review	Send the candidate to human or multi-party review
prepare_allocation	Prepare allocation workflow after review requirements are satisfied
hold_for_dispute_check	Pause until dispute or conflict checks are complete
aggregate_until_threshold	Continue accumulating trace events before review
manual_decision_required	Requires explicit human decision
10. Direct Quote vs Structural Influence

Different usage types should be handled differently.

Direct Quote

Direct quote events are often easier to verify.

They may have:

Clear retrieved fragment
Clear output fragment
Visible citation
High fragment hash confidence
High verification confidence

A direct quote may move toward ready more quickly.

direct_quote
  → strong fragment evidence
  → allocation_readiness = ready
Structural Influence

Structural influence is more complex.

It may involve:

Framework reuse
Classification pattern reuse
Conceptual architecture reuse
Similar reasoning structure
No direct quotation

Structural influence should usually require review.

structural_influence
  → high influence signal
  → review required
  → allocation_readiness = trigger_candidate

This is where the Allocation Layer must be careful.

The signal may be important, but it should not bypass judgment.

11. Outlier Origin and Allocation

Outlier Origin Detection identifies highly distinctive concepts or structures.

Examples:

Newly coined terms
Original theoretical models
Rare conceptual combinations
Unique architecture patterns
High-density structural proposals

Outlier origin signals are important because AI systems may absorb original ideas without quoting them.

However, outlier detection does not automatically prove ownership.

It should be treated as:

High-priority evidence, not final judgment.

A typical flow:

Outlier Origin Trace
  ↓
High origin_score
  ↓
High verification_confidence
  ↓
Allocation Trigger
  ↓
Human or multi-party review
  ↓
Allocation decision
12. Review Gate

The Allocation Layer should include a review gate.

The review gate may check:

Evidence completeness
Permission validity
Attribution confidence
Dispute status
Prior claims
Overlapping sources
Similar independent origins
Policy thresholds
Jurisdiction-specific rules

Possible review outcomes:

approved_for_allocation_review
blocked
rejected
superseded
requires_more_evidence
held_for_dispute_check

The review gate protects the system from false positives and premature distribution.

13. Dispute Handling

Some allocation candidates may be disputed.

Disputes may arise when:

Multiple creators claim the same concept
Similar structures emerged independently
Permission status is unclear
The trace event is incomplete
The attribution score is contested
The source was referenced but not meaningfully used

In these cases, the Allocation Layer should not proceed automatically.

Recommended behavior:

Allocation Trigger
  ↓
Dispute Check
  ↓
Hold / Review / Reject / Supersede

The Trace Layer should preserve evidence so that disputes can be reviewed later.

14. Aggregated Allocation

Some usage events may be too small to allocate individually.

In these cases, trace events can be aggregated.

Examples:

Many low-level factual references
Repeated RAG retrievals
Small concept references across multiple sessions
Long-term influence signals
Periodic settlement candidates

Flow:

Small Trace Events
  ↓
Aggregation
  ↓
Threshold Check
  ↓
Allocation Trigger
  ↓
Review

This avoids both extremes:

Ignoring small usage completely
Overloading the system with tiny payment events
15. Automation Level

The Allocation Trigger includes an automation_level.

Possible values:

none
assistive
semi_automated
automated_with_review
fully_automated

For early Royalty OS v3.0 implementations, recommended default:

assistive

Meaning:

The system may recommend actions, but humans or authorized review systems make final decisions.

This is especially important for:

Structural influence
Concept reference
Outlier origin
Disputed claims
Aggregated usage
16. Policy Dependency

Allocation decisions depend on policy.

Different ecosystems may use different rules:

Publisher-specific rules
Platform-specific rules
Creator-defined licenses
RSL-style licensing systems
Academic citation policies
Collective management rules
Jurisdiction-specific legal requirements
Experimental research policies

The Trace Layer should remain policy-aware but not policy-locked.

This is why the Allocation Trigger includes:

allocation_policy_id

The same trace evidence may lead to different allocation outcomes under different policies.

17. Privacy Requirements

The Allocation Layer should not require unnecessary private data.

Allocation Triggers should preferably exclude:

Raw user prompts
Direct user identity
Raw private content
Sensitive session details

Recommended privacy mode:

hash_only

or:

aggregated

The goal is to allocate value based on content usage evidence without turning allocation into surveillance.

18. Example Trace-to-Allocation Path

Example path for structural influence:

1. AI retrieves a registered framework.
2. The generated output reuses the architecture without direct quotation.
3. A Trace Event is recorded.
4. Verification confirms retrieval log, semantic similarity, and structure-level influence.
5. attribution.origin_score is high.
6. allocation_readiness becomes trigger_candidate.
7. Allocation Trigger is generated.
8. Review gate checks dispute status and evidence quality.
9. Allocation Layer decides whether and how to distribute value.

Example path for direct quote:

1. AI retrieves a registered sentence.
2. The sentence appears in user-facing output.
3. A Trace Event is recorded.
4. Fragment hash and citation evidence are strong.
5. allocation_readiness becomes ready.
6. Allocation Trigger may recommend prepare_allocation.
7. Review or policy engine confirms whether payment or attribution action is required.
19. What the Allocation Layer Should Receive

The Allocation Layer should receive structured data, not vague claims.

Minimum recommended input:

trigger_id
source_trace_events
recipient_os_id
content_os_id
allocation_basis
candidate_score
recommended_action
review_status
decision_context
evidence bundle reference

This makes downstream processing auditable.

20. What the Allocation Layer Should Not Assume

The Allocation Layer should not assume:

Every trace event deserves payment
Every similarity match proves influence
Every outlier is original
Every citation is allocation-worthy
Every high score is legally valid
Every AI output can be attributed to a single source
Every creator claim is automatically correct

Allocation should be evidence-informed, not evidence-blind.

21. Minimal Contract Between Layers

The minimal contract between Trace Layer and Allocation Layer is:

Trace Layer promises:
  - structured evidence
  - explicit confidence scores
  - permission status
  - usage type
  - privacy controls
  - evidence references

Allocation Layer promises:
  - review before final distribution
  - dispute awareness
  - policy-based decision-making
  - auditable allocation logic
  - no automatic payment from weak trace signals

This contract keeps the system credible.

22. Summary

The Trace Layer and Allocation Layer are closely connected but must remain separate.

Trace Layer:
  records evidence

Allocation Trigger:
  signals review readiness

Allocation Layer:
  decides distribution

The purpose of this architecture is not to monetize every AI reference.

The purpose is to ensure that meaningful AI usage can become visible, reviewable, and fairly handled.

Royalty OS v3.0 depends on this separation.

Without Trace, allocation is blind.
Without Review, allocation is reckless.
Without Allocation, trace has no value circulation.

Together, they form the beginning of a sustainable AI-era royalty infrastructure.

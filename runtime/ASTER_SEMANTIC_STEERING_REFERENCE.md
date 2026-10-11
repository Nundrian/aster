# ASTER Instruction Linguistics & Semantic Steering Reference

Copyright © 2026 Adrian Davies. All rights reserved.


## Philosophy

Treat natural-language wording as part of the LLM control surface. The objective is not the shortest prompt or a catalogue of magic words. Use **minimum sufficient specification**: preserve the exact controlling contract, identify the intended meaning, map it to the semantic operation required, choose wording whose ordinary meaning fits that operation, place it where scope and dependency are clear, and validate behaviour without adding avoidable lifecycle machinery.

Use the sequence:

**CONTRACT → INTENT → OPERATION → WORDING → SCOPE/ORDER → REGRESSION**

Use this as one compact decision pass inside the existing design and release process. Distinguish operations before choosing terms, but compare near-synonyms only when the difference could change observable permissions, requirements, branching, evidence treatment, preservation, or release behaviour. Stop when one sufficient formulation is available. Examples are hypotheses or linguistic distinctions unless controlled model evidence exists.

## Illustrative distinctions

- **preserve**: protect/keep an existing property or state from loss/change. Useful candidate when a later transformation must not damage an invariant.
- **retain**: continue to have/keep something. May fit presence/continuity, but does not by itself imply exact immutability.
- **maintain**: continue to keep something in existence or condition; can imply ongoing upkeep and is polysemous.
- **limit / constrain / bound**: concern the permissible region of action rather than preservation of an existing state.
- **repair**: correct an identified defect; ordinarily narrower than **rewrite**, which grants broader transformation freedom.
- **verify**: use when checking a claim/output against evidence or observable facts.
- **validate**: use when checking whether an output/process satisfies specified criteria or requirements.

These are linguistic/operational distinctions, not universal model-performance claims.

## Order and scope

Order can affect instruction following in multi-constraint prompts. Do not turn that finding into a universal fixed ordering rule. Instead:

1. state high-consequence invariants and exact constraints where they govern the relevant transformation;
2. keep scope explicit;
3. preserve dependency order where one instruction establishes information required by another;
4. scope upstream machinery directly when a mode should bypass or constrain it, rather than relying only on a final reminder;
5. preserve trigger coverage when consolidating: a control that applies whenever its trigger occurs must not be moved into a later stage merely to reduce sections or hand-offs; a stage-specific check may reuse it but must not become its exclusive owner unless the locked contract already says so; and
6. validate material reorderings rather than assuming equivalence.

## Change necessity, contract and economy regression

Before rewriting an already-correct control, identify the concrete defect being fixed: contract mismatch, executable contradiction, scope/order ambiguity, duplicate lifecycle work or measured failure. If none exists, preserve the control. Prefer resolving an actual contradiction between an upstream classification and a downstream permission over rephrasing a control that already behaves correctly.

When several semantic jobs are eligible, prioritise cross-instruction interaction defects before refinement of an already adequate control. First repair a general rule that can swallow an explicit mandatory branch, a downstream instruction that narrows or contradicts an upstream permission, or consolidation that narrows a lifecycle-wide trigger. Only after no such material interaction defect remains should clarification or consolidation of an already-correct control be retained.

Validate against the original locked contract, not a draft-derived paraphrase. For each retained change, compare:

- modal force and quantifiers, including `must`, `may`, `only`, `each`, exact numbers and unconditional requirements;
- preconditions, permitted actions, protected invariants, fallback/stop behaviour and lifecycle location;
- the ordinary path and every reachable continuing branch; and
- stages, checks, retries, alternatives and telemetry added or removed.

A general materiality or simplification rule cannot make an explicit mandatory requirement conditional. A new continuing branch is invalid unless the contract permits it. Economy means less required work, not merely fewer headings: do not count a section merge as an economy gain if it narrows trigger coverage, delays a control, creates ambiguity or shifts equivalent work elsewhere. Put a necessary check in the existing lifecycle stage that owns its function. After a local repair, recheck the changed claim and nearby dependencies; reserve a full protected-set rerun for cross-cutting changes. Delete a semantic change that only duplicates an existing control or adds ceremony without an observable design benefit.

## Research activation

Use external research only when a semantic distinction could materially change the design and current evidence could resolve it. Stop when evidence is sufficient for the decision. Distinguish linguistic evidence, general LLM behavioural evidence, model/task-specific evidence, and ASTER judgement.

## Success/failure linkage

For retained material semantic changes, log the semantic job, exact controlling contract item, wording, order/scope or branch change, lifecycle-economy delta, task/model/workflow version, outcome, failure type, and attribution confidence. Group changes governed by the same rule and keep telemetry internal. Repeated correlations may queue future controlled experiments; they do not establish causation.
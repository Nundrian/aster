# ASTER Volatile Source Discovery Reference

Copyright © 2026 Adrian Davies. All rights reserved.

## Purpose and routing

Load this reference only when all are true:

1. current product, platform, model, or control behaviour materially affects correctness;
2. the exact product surface and control semantics are locked;
3. the best eligible evidence is missing or too indirect to entail the operational claim.

Do not load it for stable product-agnostic tasks, for generic prompt-engineering research, or after direct sufficient evidence has already resolved the claim.

This reference improves source discovery. It does not change task authority, permit cross-surface substitution, or weaken a strict fail-closed requirement.

## Required inputs

Carry in only:

- the exact operational claim that must be verified;
- vendor/product, surface, feature/mode, and material role/plan/workspace/platform conditions;
- the semantic distinction that controls the task, such as `restrict` versus `prioritise`, `read` versus `write`, or `available` versus `enabled`;
- official sources already inspected and the precise support still missing;
- a task-proportionate time/tool/context boundary for discovery.

## Evidence trace

Maintain a compact internal record. Use observable source and search metadata, not hidden chain-of-thought.

```text
locked claim:
locked surface:
exact semantic distinction:
search intent(s):
sources inspected: [title, URL/stable pointer, date/version when visible]
source directness: DIRECT | PARTIAL | INDIRECT | INELIGIBLE
eligibility: ELIGIBLE | INELIGIBLE [short reason]
entailment: SUPPORTS | CONTRADICTS | INSUFFICIENT
environment observation: AVAILABLE | UNAVAILABLE | NOT_CHECKED | NOT_OBSERVABLE
evidence state: VERIFIED_AVAILABLE | VERIFIED_UNAVAILABLE |
                ENVIRONMENT_UNAVAILABLE | UNRESOLVED
controlling source or unresolved reason:
```

The trace belongs in the judgement/audit record unless the task requests it. Do not put it inside the finished user-facing artifact.

## Directness ladder

Classify a source against the locked claim, not against the general topic.

- `DIRECT` — current official documentation for the locked surface explicitly describes the exact feature/control and semantic behaviour used by the workflow. For a claim about a specific feature/mode lifecycle, generic product or workspace-admin controls are not `DIRECT` merely because they are in the same product family.
- `PARTIAL` — current official same-surface documentation describes the feature but omits one material semantic, role, plan, or environment condition.
- `INDIRECT` — generic or adjacent official material, release notes without controlling detail, another feature/surface, a search snippet, or a page that is topically relevant but does not address the exact claim.
- `INELIGIBLE` — wrong surface, stale/superseded, unofficial when official authority is required, deployment mismatch, or otherwise excluded by ASTER's eligibility gate.

Authority does not compensate for indirectness. A generic official page can be a strong discovery lead and still be insufficient evidence for the claim. Do not turn an adjacent generic/admin control into a blocking prerequisite when direct same-feature guidance already establishes the required lifecycle boundary, unless the task requires independent enforcement or direct eligible evidence shows the extra control is necessary.

## Targeted discovery procedure

1. **Translate the evidence gap into search intent.** Combine the exact product, surface, feature/control name or likely current equivalent, and missing semantic term. Include official-provider scope. Search for the missing proposition, not merely the product name.
2. **Prefer feature/control documentation.** Look first for the official Help/Product page on a user-facing surface, the official developer/API page on an API/SDK surface, or the official admin page for an admin control. Open the underlying page; snippets and result titles are leads only.
3. **Test entailment immediately.** Ask whether the opened source supports or contradicts the exact operational claim, including its surface and semantic distinction. Record `INSUFFICIENT` when it does not.
4. **Reformulate around the missing semantic.** If a source is partial or indirect, narrow the next search to the unresolved term, control label, feature section, plan/role condition, or documented synonym. Follow relevant official navigation or links when they plausibly lead to the controlling page.
5. **Do not broaden indiscriminately.** Do not accumulate generic product pages, adjacent APIs, unofficial summaries, or repeated sources merely to increase source count. Cross-surface material may help identify terminology but remains ineligible for the locked claim.
6. **Recheck freshness and supersession.** Prefer the current controlling page. Use release notes or archived material only to resolve chronology or identify a successor; they do not override a current direct page without explicit supersession evidence.
7. **Stop on sufficiency.** End discovery as soon as a state below is justified. No minimum search count applies.

## Evidence-state transitions

Set exactly one state for the claim. Keep the locked claim atomic enough for one state to classify it truthfully. If documented product capability and actual-environment availability both matter, record the documentary claim and the environment observation separately; if the locked claim explicitly combines them, an unobserved required environment condition leaves that combined claim `UNRESOLVED`. Do not reuse the evidence-state labels inside a generated workflow with a different scope.

### `VERIFIED_AVAILABLE`

Use only when direct current authoritative same-surface evidence supports the exact control semantics. If execution depends on plan, role, workspace policy, account, or platform, separately verify the actual environment before relying on the control.

### `VERIFIED_UNAVAILABLE`

Use only when direct current authoritative same-surface evidence explicitly establishes non-availability or incompatibility for the locked conditions. Omission, silence, an empty search result, or only finding generic pages is not negative evidence.

### `ENVIRONMENT_UNAVAILABLE`

Use when authoritative evidence supports the capability generally but an observable check shows that the actual account, plan, role, workspace, policy, platform, or exposed controls do not provide or enable it. Record the environment observation separately from the product claim.

### `UNRESOLVED`

Use when direct evidence remains missing, indirect, inaccessible, ambiguous, stale, or conflicting when the declared discovery boundary is reached. Record what was searched and the exact missing support.

A strict task may fail closed on `UNRESOLVED`. The user-facing statement must be “the required control could not be verified,” not “the control does not exist” or “the product does not support it.”

## Environment check

Documentation of availability is not proof of enablement. When the workflow will instruct an operator to use a control:

1. verify that the active surface matches the documented surface;
2. inspect the control in the actual account/workspace when access permits;
3. record material plan, role, policy, or platform conditions;
4. use `ENVIRONMENT_UNAVAILABLE` if the documented control is absent, disabled, or unusable there;
5. use `UNRESOLVED` when the environment cannot be observed and that prevents the required conclusion. If the evidence record is scoped only to documented product capability, it may remain `VERIFIED_AVAILABLE`, but the separate operational decision must still fail closed when the required environment check is unresolved. Never leave a combined capability-plus-environment claim as `VERIFIED_AVAILABLE` when its required environment condition was not observed.

Do not infer environment unavailability from a documentation search miss.

## Source-memory use

A maintained source ledger may suggest official pages, feature names, prior queries, and supersession links. Treat every ledger entry as a discovery lead:

- live-verify volatile claims before use;
- preserve provider, product/surface, feature/control, proposition, official pointer, review date, and supersession status;
- never store hidden test answers, judge rubrics, or case-specific expected outputs in runtime memory;
- deactivate or mark stale entries rather than letting old and current pages compete as equal evidence.

Provider-specific pages do not belong in ASTER Core.

## Retrieval residual and evaluation

If targeted intent still fails to return a plausible direct official source, do not disguise that as a judgement conclusion. Record separately:

- discovery intent issued;
- official results returned or not returned;
- whether a known direct source was retrievable by an exact-title/URL route when such a route is available;
- source directness and entailment;
- final evidence state.

Repeated failure at discovery while eligibility and entailment behave correctly is evidence of a retriever/search-tool bottleneck. Repeated discovery followed by premature stopping is evidence of a workflow bottleneck. Preserve both possibilities until a test distinguishes them.
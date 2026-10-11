# ASTER v1.0 — Runtime Guide

Copyright © 2026 Adrian Davies. All rights reserved.

ASTER is a file-based research-and-judgement workflow for creating or improving prompts and AI workflows. Its purpose is to protect the original task, decide which design questions actually matter, use research selectively, make the smallest justified change, and check the finished result against the original contract.

## Runtime files

| File | Role | When to read |
|---|---|---|
| `00_READ_FIRST.md` | Package router | Always first |
| `ASTER_CORE_WORKFLOW.md` | Core methodology and authority | Always |
| `ASTER_WORKFLOW_DESIGN_RESEARCH_REFERENCE.md` | Workflow-design evidence | Only after the Core research gate activates for a material design decision |
| `ASTER_SEMANTIC_STEERING_REFERENCE.md` | Semantic steering companion | Only when wording, scope or order is materially consequential |
| `ASTER_VOLATILE_SOURCE_DISCOVERY_REFERENCE.md` | Volatile product/source discovery specialist | Only when the Core reaches the unresolved volatile-product route |

The optional files are not separate mandatory stages and do not override the Core. More than one optional route may activate if the Core independently establishes more than one material need.

## The ordinary run

1. Upload the ASTER ZIP and the prompt, workflow or other task material you want to work on.
2. Tell the AI to read `00_READ_FIRST.md` first and follow its directions.
3. Tell ASTER what you want to achieve.
4. ASTER locks the task before research can influence the design.
5. If no material research question exists, ASTER proceeds without opening optional research references.
6. If a material question exists, ASTER opens only the reference or evidence relevant to that decision.
7. ASTER designs or repairs the smallest sufficient prompt/workflow and runs its contract and release checks.

A short instruction is enough:

> Read `00_READ_FIRST.md` first and follow its directions. Use ASTER on the prompt or workflow I have supplied. I want to achieve [describe what you want]. Preserve anything that already works. Ask me if anything materially important is missing.

## What the optional routes are for

### Workflow-design research

Use when evidence could change a material decision about architecture, local repair, deterministic control, context, tools, model/runtime conditions, evaluation, state/recovery, or justified complexity.

### Semantic steering

Use when wording, construction, scope, or order could change permissions, preservation, branching, evidence treatment, transformation freedom, or release behaviour.

### Volatile source discovery

Use only for unresolved, current, product-surface-specific operational claims. It is not a general web-search checklist. The Core controls when it is eligible.

## Version

ASTER v1.0 is the first finished release. The runtime package is intended to be used as supplied. Changes to the Core or its companion references should be made as a new version so the behaviour of this release remains identifiable.

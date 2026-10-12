# ASTER v1.0 — task fidelity and disciplined prompt/workflow design

**Not an ordinary prompt optimiser.** ASTER is a reusable methodology for designing, examining and repairing prompts and AI workflows **without quietly changing the task they are meant to accomplish**. It is intended to work with a capable AI assistant; ASTER itself is not a model, agent runtime or execution engine.

**Status:** The repository is public and the workflow is free to access. ASTER v1.0 is an identified release, not a claim of universally proven performance across models.

## Why ASTER exists

Capable frontier models can produce surprisingly bloated instructions: redundant prohibitions, unnecessary stages, excessive defensive wording or elaborate redesigns of something that mostly works. That can obscure the real objective, consume context and leave less capable models with work they cannot reliably execute.

ASTER starts by **locking the original task contract**: the objective, success condition, inputs, output contract, critical constraints, permissions and authority boundaries. It then asks what, if anything, actually needs improving. Research and specialist references are **conditional**, not compulsory. The smallest justified solution takes priority over adding more instructions.

### The important distinction: repetition versus anchoring

Shorter is **not** automatically better. ASTER removes repetition that merely emphasises the same point, while preserving **functional reinforcement** such as rechecking requirements at validation and restating critical invariants at stage handoffs when the receiving component cannot depend on earlier context. These repetitions have different jobs. This is the current v1.0 Core's documented behaviour, not a claim that ASTER automatically inserts an anchor in every paragraph.

Maintaining these anchors may help a model remain oriented during lengthy work or context compaction, but the extent of any improvement still needs controlled testing.

## What makes ASTER different

- **Task-fidelity lock:** Preserve the actual request rather than optimising towards a subtly different one.
- **Minimal justified intervention:** Repair what is wrong and retain what is working.
- **Controlled context:** Avoid unnecessary instructions, duplicated work and automatically loading every supporting reference.
- **Semantic steering:** Consider how wording, scope and order affect the instructions that must survive.
- **Conditional research:** Consult supporting material only when it could alter a material decision, and distinguish evidence from speculation.
- **Release checks:** Compare the final work against the *original* locked task contract, including format, permissions and required inputs.
- **Handoff reinforcement:** Repeat critical constraints where a new phase/model would otherwise risk losing them.

The framework does not guarantee superior outputs, eliminate hallucinations or replace deterministic tests. A model checking its own work is not an independent validator.

## Frontier model planning for smaller local models

One use case is preparing a complex project with a frontier model, then having a resource-constrained local LLM execute manageable portions of it.

1. Give the frontier model the overall objective, constraints, source material and realistic limits of the intended local model.
2. Ask it to apply ASTER when constructing a plan and **small, independently actionable, well-bounded prompts**.
3. For each task, specify relevant input, expected output, success criteria, dependencies and what to do on failure — **without burdening the local model with the entire original project**.
4. Review the plan for missing requirements and unsuitable dependencies, then hand the tasks to your local model and verify the results.

ASTER can assist in designing these prompts; **it does not run tasks, automatically generate Magazine cartridges or guarantee that a small model can complete every task**.

[Magazine](https://github.com/Nundrian/Magazine) is a separate project exploring bounded task execution for smaller LLMs. The two tools may be used independently, or together by choice. The public Magazine repository currently describes a development implementation rather than a production-ready release.

## Other useful applications

- Long-running AI development projects where instructions, context and requirements may drift.
- Reviewing prompts or workflows that already work in part without rewriting everything.
- Diagnosing mistakes caused by ambiguous instructions, missing handoffs, wrong tools or model limits.
- Preparing bounded research, coding, editing or inspection tasks for 7B–30B local models.
- Maintaining output schema, permissions and acceptance criteria across stages.
- Comparing alternative workflow designs with explicit evidence and evaluable success conditions.
- Refining expensive or verbose frontier-generated prompts for limited contexts.

## Download and use

The current CC BY 4.0 licensed v1.0 runtime archive is **[ASTER_v1.0_CURRENT.zip](ASTER_v1.0_CURRENT.zip)**.

1. Download the ZIP (or clone the repository).
2. Upload the archive to a model that can read the files. Alternatively supply the individual Markdown files.
3. Tell the model: **"Read `00_READ_FIRST.md` and follow its loading instructions. Apply ASTER to the supplied prompt or workflow. My objective is [your objective]. Preserve everything that already works."**
4. The router loads `ASTER_CORE_WORKFLOW.md`; supporting references are opened only when the Core's relevant gate activates.
5. Review the output against the original requirements; verify important results independently.

The runtime package includes the router, Core, runtime guide, semantic-steering reference, workflow-design research reference, volatile-source discovery reference, copyright notice, CC BY 4.0 licence notice and SHA-256 manifest. The extracted files are also provided under **[runtime/](runtime/)** for inspection and reuse.

**Current CC BY 4.0 archive SHA-256:** `d43386df9e3e7af8492e581fe0e22e0d470058bdb9ef04ccc2cb0139dfe6e888`. Its `SHA256SUMS.txt` lists the contents for independent verification. Only the copyright/licence notices were changed in the six workflow/reference files; the operational instructions are unchanged.

**Historical provenance:** The pre-licence archive SHA-256 was `1737fd314f979796b65c4e53eb999f9a4a7211981459e42ddef6b0238f4316c4`. That checksum does **not** apply to the current licensed ZIP.

## Evidence and research

ASTER emerged from iterative prompt/workflow experiments, including longer coding projects, task drift and context compactions. These observations motivate testable hypotheses, **not proven causal claims**. The project welcomes comparisons across models and conditions, including unsuccessful cases. Useful reports record the original task, model/version, prompt, token budget, compaction conditions, failure modes and externally checked outcomes.

The accompanying workflow-design reference has a research cut-off of 24 August 2026; current provider capabilities should be verified separately.

## Licence — CC BY 4.0

© 2026 Adrian Davies. ASTER is available under **[Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE.md)**. You may use, modify, copy, share and redistribute ASTER for **personal or commercial** purposes. When sharing ASTER or adaptations, credit the creator, link to the licence and indicate changes. The official [legal code](https://creativecommons.org/licenses/by/4.0/legalcode) governs. No endorsement is implied, and the material is provided without warranty.

Suggested attribution: **ASTER v1.0 by Adrian Davies — CC BY 4.0 — https://github.com/Nundrian/aster**.

## Security and integrity

The ClamAV scan recorded on 31 August 2026 reported nine scanned files and no detections for the **pre-licence archive**, not the new CC BY 4.0 ZIP. The updated release has new notices and checksums; this is not a new malware scan. Antivirus screening cannot guarantee safety.

# ASTER Workflow Design Research Reference

Copyright © 2026 Adrian Davies. All rights reserved.

**Status:** Companion research reference for ASTER v1.0  
**Research cut-off:** 24 August 2026  
**Scope:** General LLM prompt/workflow design, orchestration, evaluation, repair, context, reliability, portability, security, and efficiency.  
**Not the VSDR:** This file is deliberately separate from ASTER's Volatile Source Discovery Reference. The VSDR is for verifying volatile product/model/control facts. This reference is for evidence about *how workflows should be designed or improved*.

---

## 1. Purpose and routing

Use this reference only when a material workflow-design decision remains uncertain after the task contract and supplied evidence have been understood.

Typical triggers:
- whether a workflow should be redesigned or only locally repaired;
- whether a step should be deterministic or model-judged;
- whether architecture, prompt wording, context, tools, memory, or evaluation is the likely bottleneck;
- whether additional stages, agents, reflection, search, or context are justified;
- whether a workflow result is portable across models or configurations;
- whether evaluation evidence is strong enough to support a design change;
- whether long-horizon state, recovery, auditability, policy enforcement, or security controls are required.

Do **not** load this reference merely because workflow-design research exists. Do not allow it to replace the user's task objective or supplied evidence.

---

## 2. Evidence classes

Use the following evidence classes when interpreting research:

1. **PEER_REVIEWED_EMPIRICAL** — conference/journal study with described experiments.
2. **PRIMARY_RESEARCH_PREPRINT** — current research paper not yet peer-reviewed; useful but provisional.
3. **PRODUCTION_ENGINEERING** — first-party engineering evidence from a deployed system; strong for observed operational behaviour, weaker for universal generalisation.
4. **OFFICIAL_PRODUCT_GUIDANCE** — useful for current supported architecture or product practice; not independent evidence of superiority.
5. **BENCHMARK_OR_EVAL_DESIGN** — evidence about measurement validity, task construction, or trajectory evaluation.
6. **SYSTEMATIC_OR_SYNTHESIS** — broad evidence map; use to discover primary sources rather than as sole support for a narrow design claim.
7. **SECONDARY_DISCOVERY_ONLY** — commentary/community material; use only as a lead unless independently verified.

For every design conclusion, distinguish:
- what the source directly demonstrated;
- what is a reasonable cross-task inference;
- what remains unverified for the current task/model.

---

## 3. Core workflow-design principles

### P1. Lock the task before optimising the workflow

**Rule:** Optimisation must improve performance against the original task contract, not silently redefine the task to fit the workflow or evaluator.

**Why it matters:** Recent evaluation work shows that apparently strong systems can exploit weak or noisy evaluation conditions, while realistic deployment simulation changes observed behaviour.

**Use when:** Any redesign, automated prompt optimisation, benchmark-driven change, or judge-guided repair is proposed.

**Evidence:** Meta AIRA₂; OpenAI deployment simulation; OpenAI coding-evaluation audits; LG DEER.

---

### P2. Separate architecture optimisation from component/prompt optimisation

**Rule:** Treat these as different intervention levels:
1. workflow topology/architecture;
2. module or stage selection;
3. individual prompt/instruction optimisation;
4. context/tool/configuration optimisation.

Do not rewrite every prompt when the topology is wrong, and do not redesign the topology when one local instruction is the failure.

**Evidence:** MIT FlowBot (outer workflow vs inner call optimisation); CUHK-Shenzhen/NUS work on generation, query-conditioned workflow selection, and fixed-topology prompt optimisation; Tsinghua AgentSquare; UBC/Vector ADAS.

---

### P3. Prefer bounded/local repair when the existing architecture is substantially sound

**Rule:** Preserve validated structure and repair the smallest causal region unless evidence shows the architecture itself is the bottleneck.

**Evidence:** GRAFT locally replaces selected workflow regions rather than re-optimising the whole workflow; Sakana AI Scientist v2 explicitly notes that freer agentic search may underperform v1 when a strong template already exists; JudgeFlow targets problematic blocks rather than indiscriminately rewriting the full system.

**Caveat:** Open-ended tasks with poor starting structure may genuinely benefit from architecture search or greater autonomy.

---

### P4. Use deterministic mechanisms for deterministic work

**Rule:** Routing, iteration, scheduling, validation, arithmetic, schema enforcement, retries, state transitions, and other mechanically specified operations should normally be handled by deterministic code or explicit workflow logic. Use the model where semantic judgement, synthesis, ambiguity resolution, or generative flexibility is required.

**Evidence:** Google ADK 2.0; Sarvam Arya; Samsung Research multi-agent compiler; Microsoft Agent Workflow Optimization.

**Why:** This usually reduces variance, token cost, latency, and silent process skipping.

---

### P5. Context is a finite design resource, not a dumping ground

**Rule:** Supply the smallest sufficient high-signal context. Prefer progressive disclosure or just-in-time retrieval to permanent inclusion of all potentially relevant material.

**Evidence:** Anthropic context engineering; Sarvam Arya context separation; production systems that isolate agent-specific context.

**Failure modes:** context pollution, instruction dilution, duplicated evidence, stale material competing with current material, and token expenditure on navigation rather than task work.

---

### P6. The target model and configuration are part of the workflow conditions

**Rule:** A workflow optimised on one model, model family, reasoning mode, tool environment, or inference configuration is not automatically verified on another.

Record when material:
- exact model/version;
- reasoning/effort mode;
- tool availability and tool schema;
- context limits;
- decoding or other material inference settings;
- runtime/harness differences.

**Evidence:** EACL 2026 MePO model-portability work; Meta ARE; OpenAI third-party evaluation guidance; multiple workflow-optimisation papers reporting backbone-dependent results.

**Design consequence:** Optimise for the actual executor, not an abstract “LLM”.

---

### P7. More agents, more reflection, and more test-time compute are conditional tools, not default improvements

**Rule:** Add agents, reflection depth, parallel reasoning, or recursive loops only when they solve a measured problem.

**Evidence:** BenchAgent finds most tested multi-agent configurations do not beat a protocol-aligned single-agent anchor and are more expensive; KAIST finds rapidly diminishing returns and widening latency/resource costs with deeper dynamic reasoning; Meta ARE finds budget-scaling plateaus and no universally dominant system.

**Counter-evidence:** AgentSquare, ADAS and other search methods show multi-stage/multi-agent structures can outperform hand designs for some tasks.

**Resolution:** complexity is justified by task-conditioned evidence, not by architecture fashion.

---

### P8. Evaluate the execution path, not only the final answer

**Rule:** Final task success can conceal skipped controls, wrong ordering, accidental shortcuts, or unsafe intermediate behaviour.

**Evidence:** Agentic Success Rate research shows models can achieve apparently correct outcomes while skipping required workflow checkpoints; Microsoft trace/trajectory optimisation and LG dynamic evaluation similarly emphasise diagnostic process signals.

**Use when:** ordering, approval, policy, compliance, handoffs, or mandatory intermediate checks matter.

---

### P9. Diagnose the earliest causal failure before changing the workflow

**Rule:** Use traces/failures to localise the first block, transition, instruction, tool choice, or state error that makes recovery unlikely. Modify downstream behaviour only if it is independently defective.

**Evidence:** JudgeFlow uses block-level responsibility; Microsoft AgentRx localises first unrecoverable failures; GRAFT uses region-level execution-quality signals.

**Benefit:** reduces broad rewrites caused by symptoms rather than causes.

---

### P10. Evaluation quality is part of workflow quality

**Rule:** A workflow cannot be considered improved merely because it scores better on a weak, noisy, contaminated, underspecified, or optimisation-exposed evaluator.

Prefer:
- task-representative cases;
- held-out evaluation after optimisation;
- multiple seeds/repeats when stochasticity matters;
- exact acceptance criteria;
- trace-level diagnostics when process fidelity matters;
- regression cases for already-correct behaviour;
- human/domain review for claims an automated judge cannot reliably assess.

**Evidence:** Meta AIRA₂ evaluation-noise finding; LG DEER; OpenAI evaluation audits and third-party evaluation guidance; RLMOpt regression constraints.

---

### P11. Separate search headroom from optimisation effort

**Rule:** More optimisation budget does not guarantee useful improvement. First ask whether the current workflow has measurable headroom and whether the evaluator can distinguish better from merely different.

**Evidence:** RLMOpt reports gains driven primarily by available headroom rather than search budget and combines adaptive search with deterministic Pareto/regression controls; Meta ARE reports scaling plateaus.

**Stop condition:** terminate optimisation when material headroom is exhausted, regressions appear, evidence quality becomes limiting, or further search is dominated on cost/performance.

---

### P12. Long-horizon workflows need explicit state, recovery, and audit design

**Rule:** For multi-stage or interruptible work, define durable state, clear transitions, retry/recovery semantics, provenance, and restart behaviour rather than relying on conversational continuity alone.

**Evidence:** AgentR (August 2026 preprint) proposes persistent workflow artifacts, explicit states, retries, orphan detection and auditable token/cost records; Anthropic long-horizon context work uses structured notes/compaction; production workflow systems increasingly expose explicit state/runtime layers.

**Status:** Strong engineering rationale; AgentR itself is provisional preprint evidence.

---

### P13. Policy and safety controls may need workflow-level enforcement

**Rule:** Action-local safety checks are insufficient when compliance depends on completing a sequence, obtaining confirmation, preserving approvals, or carrying state across turns.

**Evidence:** PolicyGuide (20 August 2026 preprint) compiles policy into workflow graphs and verifies progress at turn boundaries; NUS FlowSteer shows that workflow formation/planning itself can be attacked; Anthropic containment work treats blast radius and permissions as architectural properties.

**Use when:** regulated, consequential, transactional, security-sensitive, or approval-gated work.

---

### P14. Handoffs and state boundaries should be explicit and typed where failure is costly

**Rule:** Separate stages should exchange the minimum information needed under an explicit schema/contract rather than relying on broad conversational inheritance.

**Evidence:** Sarvam Arya; Google ADK 2.0 specialized-agent context isolation; Samsung structured artifacts between stages; Yandex agent architecture separates model, prompt, tools and memory.

**Benefit:** improves testability, reduces accidental context leakage, and makes failures localisable.

---

### P15. Cost, latency, token use, and energy are design variables, not afterthoughts

**Rule:** Compare candidate workflows on useful quality **and** resource cost when the deployment setting makes cost material.

**Evidence:** KAIST HPCA 2026 resource analysis; Microsoft Agent Workflow Optimization; Google ADK 2.0; ACM power-aware workflow optimisation; Sarvam Arya.

**Do not:** choose a cheaper workflow that violates required quality, or choose a more complex workflow without measuring whether the gain justifies the cost.

---

### P16. Real-world and dynamic evaluations should complement static benchmarks

**Rule:** Static benchmarks are useful but insufficient for long-horizon, tool-using, changing, or deployment-sensitive workflows.

**Evidence:** ByteDance EdgeBench (134 real-world long-horizon tasks and ~38,000 hours of interaction); Meta ARE/Gaia2 dynamic environments; LLM-jp real-world interaction and Japanese agent benchmark work; OpenAI deployment simulation; LG dynamic benchmark research.

**Design implication:** When practical, validate in an environment that reproduces the workflow's actual tools, constraints, timing, interruptions, and failure modes.

---

## 4. Conflict map: where research should not be flattened into one rule

### C1. Strong templates vs adaptive/free-form workflows

- **Evidence for structure:** Sakana AI Scientist v1 can outperform v2 when a strong template already exists; deterministic workflow research shows reliable execution when path constraints are known.
- **Evidence for adaptation:** ADAS, AgentSquare, FlowBot, GRAFT and contextual workflow selection show that adaptive structure can improve performance where task variation or poor starting architecture creates real headroom.

**Resolution:** Preserve strong known structure; introduce adaptation only at uncertain or failure-prone regions.

### C2. Single-agent simplicity vs multi-agent specialization

- **Evidence against default multi-agent complexity:** BenchAgent, KAIST cost analysis, Meta ARE.
- **Evidence for specialized multi-agent systems:** AgentSquare, Samsung production system, scientific/domain workflows.

**Resolution:** Require a measured coordination or specialization benefit. Do not use role multiplication as a substitute for better decomposition.

### C3. More reasoning vs constrained reasoning

- **Evidence for more compute:** Some tasks improve with reflection, search, test-time scaling, or recursive optimisation.
- **Evidence against unbounded compute:** plateauing returns, rising latency/energy, and larger failure surface.

**Resolution:** make reasoning budget adaptive and stop on sufficiency/headroom rather than selecting a universally “deep” mode.

### C4. Universal prompt merits vs model-specific optimisation

- **Evidence for transferable design merits:** MePO reports interpretable prompt merits that generalize across diverse model sizes.
- **Evidence for executor dependence:** multiple studies show prompt/workflow performance changes with model backbone and runtime configuration.

**Resolution:** use general merits as priors; treat actual model/task evaluation as the release evidence.

---

## 5. Workflow design decision sequence

When ASTER is deciding whether and how to improve a workflow:

1. **Lock the task contract.**
2. **Identify the observed or plausible failure mode.**
3. **Classify the intervention level:** architecture, stage/module, prompt/instruction, context, tool, model/configuration, evaluation, or runtime/state.
4. **Check whether deterministic logic can replace unnecessary model judgement.**
5. **Check context sufficiency and pollution.**
6. **Check target-model/runtime conditions.**
7. **Choose the smallest causal change.**
8. **Define evidence that would distinguish improvement from variation.**
9. **Test changed behaviour and previously-correct behaviour.**
10. **Inspect traces when final-output scoring cannot reveal process failure.**
11. **Evaluate quality/cost trade-offs where material.**
12. **Stop when the evidence is sufficient or further optimisation lacks justified headroom.**

---

## 6. Minimal research trace for workflow-design claims

For any external research used to justify a material design change, record:

```text
Design question:
Task/workflow scope:
Target model/runtime (if material):
Intervention layer:
Source:
Source class:
Date/version:
What the source directly demonstrates:
What is being inferred for this workflow:
Known limitations / conflicting evidence:
Validation required before release:
```

Do not confuse a paper's benchmark result with proof that its architecture is optimal for the current task.

---

## 7. Geographic and organisational source map

This map is for discovery and diversity of evidence, not authority by geography.

### North America
- Stanford HAI / DSPy — multi-stage prompt/program optimisation (MIPRO).
- UBC + Vector Institute — Automated Design of Agentic Systems (ADAS).
- Microsoft Research — Agent Workflow Optimization; workflow/trace diagnostics.
- Meta AI — AIRA₂; ARE/Gaia2; agent evaluation and search architecture.
- OpenAI — deployment simulation; workflow evaluation; benchmark integrity; third-party eval guidance.
- Anthropic — context engineering; agent/workflow design; containment and long-horizon engineering.

### China / Hong Kong / Singapore
- Tsinghua University — AgentSquare; modular agent/workflow design and search.
- CUHK-Shenzhen + NUS — workflow generation, contextual selection, fixed-topology prompt optimisation.
- NUS — FlowSteer; structured workflow research and security.
- Alibaba / Tongyi / Qwen ecosystem — workflow applications, agentic research, ReAct vs heavier inference scaffolding.
- ByteDance Seed — EdgeBench and live-workflow evaluation emphasis.

### India
- Sarvam AI — Arya: controlled dynamism, graph/state separation, deterministic control plane.
- IIT Madras / AI4Bharat ecosystem — multilingual/task-specific evaluation and applied agentic workflows.

### Korea
- KAIST — system-level cost of dynamic reasoning; PolicyGuide authorship.
- Samsung Research — production multi-agent workflow with strict task scope and deterministic tooling.
- LG AI Research — dynamic evaluation; deep-research evaluation; workflow design/security guidance.
- Upstage — production workflow optimisation with accuracy/time/cost and human/automatic evaluation.

### Japan
- Sakana AI — AI Scientist v1/v2 comparison; structured template versus exploratory autonomy.
- NII / LLM-jp — Japanese agent benchmarks and real-world interaction work.

### Russia
- ITMO — FEDOT.MAS and multi-stage validation; evolving multi-agent systems; agent/AutoML research.
- Yandex — explicit separation of model, prompt, tools and memory; visual workflow/runtime products; applied research agents.
- Skoltech/AIRI/MIPT ecosystem — LLM memory, autonomous agents, RAG and agent systems research.

### Smaller / independent organisations worth retaining
- Sarvam AI
- Sakana AI
- Upstage
- Letta
- All Hands AI / OpenHands (for agent engineering rather than general prompt design)

---

## 8. High-value source registry

The registry is intentionally concise. Prefer primary pages/papers and revisit current versions when using them operationally.

| Source | Date | Class | Main contribution to this reference |
|---|---:|---|---|
| Stanford HAI — MIPRO | 2024 | PEER_REVIEWED_EMPIRICAL | Optimise instructions and demonstrations jointly across multi-stage LM programs. |
| UBC/Vector — Automated Design of Agentic Systems | 2025 | PEER_REVIEWED_EMPIRICAL | Workflow/agent architecture itself can be searched and evaluated. |
| Tsinghua — AgentSquare | 2025 | PEER_REVIEWED_EMPIRICAL | Modular Planning/Reasoning/Tool/Memory design and recombination. |
| Meta — ARE/Gaia2 | 2025 | PRIMARY_RESEARCH | Dynamic environments, efficiency trade-offs, compute plateaus. |
| Anthropic — Effective Context Engineering | 2025 | PRODUCTION_ENGINEERING | Context is finite; just-in-time retrieval and compaction. |
| Sakana — AI Scientist v2 | 2025/26 current repo | PRODUCTION_RESEARCH | Greater autonomy is not automatically better than a strong template. |
| Microsoft — Agent Workflow Optimization | Jan 2026 | PRIMARY_RESEARCH_PREPRINT | Replace recurring agent/tool sequences with deterministic meta-tools. |
| KAIST — Cost of Dynamic Reasoning | 2026 | PEER_REVIEWED_EMPIRICAL | Diminishing returns and system cost of deeper agentic reasoning. |
| EACL — MePO | 2026 | PEER_REVIEWED_EMPIRICAL | Prompt quality/portability across model scales; model-aware optimisation. |
| MIT — FlowBot | Apr 2026 | PRIMARY_RESEARCH_PREPRINT | Separate workflow topology optimisation from per-call optimisation. |
| NUS — FlowSteer | 2026 | PRIMARY_RESEARCH_PREPRINT | Workflow formation/planning is a security boundary. |
| Samsung Research — Multi-agent compiler | 2026 | PRODUCTION_ENGINEERING | Strict task scoping; deterministic work in code; LLM for judgement. |
| Sarvam AI — Arya | 2026 | PRODUCTION_ENGINEERING | Controlled dynamism; explicit graph/state/control-plane separation. |
| Meta — AIRA₂ | Apr 2026 | PRIMARY_RESEARCH | Separate throughput, evaluation-noise and operator bottlenecks. |
| LG — DEER | Jun 2026 | BENCHMARK_OR_EVAL_DESIGN | Fine-grained expert rubric plus claim/evidence verification. |
| ByteDance — EdgeBench | Jul 2026 | PRIMARY_RESEARCH | Long-horizon real-world interaction evaluation. |
| MAPRO (EACL 2026) | 2026 | PEER_REVIEWED_EMPIRICAL | Topology-aware prompt credit assignment in multi-agent prompt optimisation. |
| GRAFT | Aug 3 2026 | PRIMARY_RESEARCH_PREPRINT | Local region replacement without whole-workflow reoptimisation. |
| RLMOpt | Aug 11 2026 | PRIMARY_RESEARCH_PREPRINT | Adaptive optimisation policy plus deterministic scoring/regression harness. |
| AgentR | Aug 15 2026 | PRIMARY_RESEARCH_PREPRINT | Durable state, retry/recovery and auditable workflow execution. |
| PolicyGuide (KAIST AI) | Aug 20 2026 | PRIMARY_RESEARCH_PREPRINT | Policy compliance enforced over the whole workflow, not only actions. |

---

## 9. Sources deliberately not promoted to design rules

Do not convert the following into universal ASTER rules without task-matched validation:

- vendor benchmark claims about one proprietary platform outperforming another;
- framework marketing that declares one orchestration pattern an “industry standard”;
- community posts without primary experimental evidence;
- benchmark gains produced under a materially different tool environment or model;
- one-off production anecdotes that do not identify confounds;
- papers where the evaluator is exposed to the optimiser without a held-out or regression check;
- results from highly specialised domains when the mechanism may not generalise.

---

## 10. Current research gaps

The evidence is still weak or mixed on:

1. How much workflow optimisation transfers between frontier model families and reasoning modes.
2. When a modular workflow becomes so fragmented that coordination/context overhead exceeds the benefit.
3. How many stochastic repeats are enough for reliable workflow release decisions across task classes.
4. How to measure context compression loss before it becomes task-fidelity loss.
5. How to distinguish genuine self-improvement from optimiser overfitting to evaluator quirks.
6. How far workflow-level policy graphs generalise across domains and changing policies.
7. When automatic architecture search is worth its own compute/cost relative to expert bounded repair.
8. How best to validate long-horizon workflows whose real execution lasts hours or days.

These should remain explicit uncertainties rather than being silently converted into defaults.

---

## 11. Compact ASTER-compatible synthesis

The current international evidence converges on a practical design stance:

- start from the actual task, not a preferred architecture;
- preserve sound existing structure;
- separate architecture failures from prompt, context, tool, model, evaluation and runtime failures;
- use deterministic mechanisms for deterministic work;
- keep model context selective and purpose-specific;
- treat the target model/runtime as part of the design;
- do not add agents, stages, reflection or search unless they solve a measured problem;
- diagnose failures locally before repairing broadly;
- evaluate both result quality and required process fidelity;
- protect already-correct behaviour with regression evidence;
- treat cost/latency/energy as deployment variables when material;
- maintain explicit state/recovery for long-horizon workflows;
- enforce policy/security across the workflow when obligations are sequential;
- stop optimisation when sufficient evidence is reached or justified headroom is exhausted.

This is intentionally a research reference, not a mandatory recipe. ASTER should select only the principles that materially bear on the current design decision.

---

## 12. Primary source pointers

- Stanford HAI, MIPRO: https://hai.stanford.edu/research/optimizing-instructions-and-demonstrations-for-multi-stage-language-model-programs
- UBC/Vector, ADAS: https://proceedings.iclr.cc/paper_files/paper/2025/file/36b7acf6f6010652b3f2a433774a66fe-Paper-Conference.pdf
- Tsinghua, AgentSquare: https://proceedings.iclr.cc/paper_files/paper/2025/hash/0ae94013da7cd459402fd77874e09ee3-Abstract-Conference.html
- Meta AIRA₂: https://ai.meta.com/research/publications/aira-overcoming-bottlenecks-in-ai-research-agents/
- Meta ARE/Gaia2: https://ai.meta.com/research/publications/are-scaling-up-agent-environments-and-evaluations/
- Anthropic context engineering: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
- Google ADK 2.0: https://developers.googleblog.com/why-we-built-adk-20/
- Microsoft Agent Workflow Optimization: https://www.microsoft.com/en-us/research/publication/optimizing-agentic-workflows-using-meta-tools/
- Sarvam Arya: https://www.sarvam.ai/blogs/introducing-sarvam-arya
- Samsung production workflow: https://research.samsung.com/blog/From-Modules-to-Agents-An-Automatic-AI-Inference-Optimization-Compiler-for-5G-RAN
- KAIST dynamic-reasoning cost study: https://pure.kaist.ac.kr/en/publications/the-cost-of-dynamic-reasoning-demystifying-ai-agents-and-test-tim/
- NUS WING publications / FlowSteer: https://wing.comp.nus.edu.sg/publication/
- CUHK-Shenzhen/NUS workflow optimisation seminar: https://events.comp.nus.edu.sg/view/26427
- LG DEER: https://www.lgresearch.ai/publication/view?seq=168
- ByteDance EdgeBench: https://seed.bytedance.com/en/research
- Sakana AI Scientist v2: https://github.com/SakanaAI/AI-Scientist-v2
- ITMO multi-agent research: https://itmo.ru/ru/viewperson/1158/nikitin_nikolay_olegovich.htm
- Yandex agent architecture: https://aistudio.yandex.ru/docs/en/ai-studio/concepts/agents/index.html
- OpenAI deployment simulation: https://openai.com/index/deployment-simulation/
- OpenAI third-party evaluation guidance: https://openai.com/index/trustworthy-third-party-evaluations-foundations/
- FlowBot: https://arxiv.org/abs/2604.26258
- GRAFT: https://arxiv.org/abs/2608.02353
- RLMOpt: https://arxiv.org/abs/2608.10471
- AgentR: https://arxiv.org/abs/2608.15264
- PolicyGuide: https://arxiv.org/abs/2608.19861

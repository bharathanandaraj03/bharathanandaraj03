# Bharath Anandaraj

**I build the evaluation systems that decide whether a model ships.**

10+ years in test engineering and automation architecture; the last four designing quality
infrastructure for AI products — classifiers, LLM report generation, RAG, and agentic systems. The problem
that interests me is the one conventional QA has no answer for: how do you gate a release when the output
is a probability and a paragraph of clinical prose?

For the last four years that meant owning quality for a veterinary diagnostic AI platform — 94 production
condition classifiers and an LLM radiology report generator, validated against 300,000+ radiologist-labelled
cases. Per-condition performance is published openly at
**[vetology.net/ai-classifier-performance](https://vetology.net/ai-classifier-performance/)**: median
specificity 92.1%, sensitivity 74.1%, AUC 0.757–0.981.

---

### Systems I've designed

- **250,000-case classifier regression harness** — five anatomy and species cohorts, each model release
  compared against baseline with graded per-classifier verdicts.
- **Automated confusion-matrix pipeline** — sensitivity, specificity, PPV, NPV and prevalence per
  condition, resolving the model version from the registry and rolling image-level results up to case level
  by majority vote.
- **Rubric-scored generative evaluation** — regenerated reports scored against baseline across five clinical
  dimensions. Used to validate an LLM provider migration over 996 cases: zero accuracy and zero faithfulness
  regressions, with the sole failure mode isolated to severity ordering.
- **Agentic test-generation pipeline** — five cooperating agents (orchestrator, researcher, generator,
  validator, publisher) producing Playwright page objects, specs and fixtures under enforced patterns,
  gated by compilation, lint and PR review.
- **LLM-judge ground-truth audit** — curated labels compared against radiologist findings, catching label
  rot before it reaches a training set.
- **One-command model deployment** — a 40-step manual runbook reduced to a single audited command with
  configuration mutation, sibling-consistency rules and a generated report.

---

### What I'm building now

**[clinical-eval-gate](https://github.com/bharathanandaraj03/clinical-eval-gate)** — a release gate for
diagnostic AI, not a scoring script. Per-condition classifier metrics with calibration and per-slice
breakdowns, rubric-scored evaluation of generated reports, and a CI gate that fails the build when either
regresses against a stored baseline. Built on public chest X-ray data.

Early, and the README says so — the status checklist is honest about what runs and what doesn't yet.

---

### Evaluation stack

| Surface | What I measure with |
|---|---|
| **Classifiers** | Confusion matrix, sensitivity / specificity / PPV / NPV, prevalence, AUC, calibration (Brier, reliability curves), per-slice breakdowns |
| **Generation** | promptfoo, DeepEval, G-Eval, faithfulness, hallucination, summarisation; BLEU / BERTScore for drift, never for gating |
| **RAG** | Contextual precision, contextual recall, contextual relevancy, answer relevancy |
| **Agents** | Task completion, tool correctness, argument correctness, plan adherence, step efficiency — trajectory, not just final answer |
| **Conversational** | Knowledge retention, role adherence, conversation completeness and relevancy |
| **In CI** | pytest-native gates, stored baselines, regression tolerances, PR summary comments |

---

### How I think about evaluation

**Accuracy is a lie at low prevalence.** A condition present in 2% of studies, and a model that outputs
"absent" unconditionally, scores 98%. Any metric a constant function can win is not a metric.

**The shape of a failure carries more information than its rate.** An 88% pass rate scattered across
accuracy and faithfulness means block the release. The same 88% concentrated in one presentational
dimension means ship it with a targeted fix. Same number, opposite decisions — and an aggregate score
destroys exactly the information the decision needed.

**Evaluating an agent is not evaluating its answer.** A correct result reached through the wrong tool call,
or a plan the agent abandoned halfway, is a failure that has not surfaced yet. Trajectory metrics —
tool correctness, plan adherence, step efficiency — catch the class of bug that end-state scoring is blind
to by construction.

**Cheap deterministic checks run before expensive probabilistic ones.** A string comparison that catches an
entire class of regression costs nothing. Only what survives it is worth spending an LLM judge on.
Inverting that order is how eval bills grow without catching more.

**An LLM judge is a model, not a ruler.** Rubric scores from a language model are one model's opinion of
another's output, with their own bias and variance. Validate the judge against human experts on a stratified
subset and report agreement per dimension — or don't gate releases on it.

**Measure the programme with the same rigour you apply to the product.** This year I modelled my own
automation coverage curve and found the target was unreachable at the current test-case intake rate: the
constraint was intake policy, not automation throughput. Publishing that was worth more than hitting the
number would have been.

---

### Background

Test engineer → automation architect → engineering manager, staying hands-on throughout. Veterinary
diagnostic AI; UK retail banking, including PSD2 Strong Customer Authentication and Open Banking work whose
stress-test results went to the FCA; insurance; rail traffic management.

**Building with** — Python · Playwright · pytest · Selenium · DeepEval · promptfoo · Docker · GitHub Actions ·
Jenkins · Azure DevOps · AWS · Azure · SQL

**Domain** — DICOM · PACS · diagnostic AI · LLM and agent evaluation · regulated delivery

---

### Elsewhere

[LinkedIn](https://linkedin.com/in/bharath-anandaraj) · bharath.anandaraj03@gmail.com

Open to quality architecture and AI/ML quality roles.

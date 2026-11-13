# Developer Adoption and Repeated Usage Report

## Purpose and evidence boundaries

This report uses the participant’s actual UnvibeCode journey on the public Flask repository as its starting point. The participant confirms exploring four output areas: Business Workflow Map; Connected Code Map; Business Risk Findings; and LLM Context with context ZIP export.

The record establishes that these areas were explored. It does not preserve the Flask report files, screenshots, CLI transcript, run duration, or specific moments of confusion. Therefore, no claim below says the participant was blocked, confused, dissatisfied, or encountered a bug. Potential friction is presented as a question for usability testing. Recommendations are engineering proposals, not user quotes.

## Verified observations from the participant’s usage

| Verified observation | Evidence | What it does and does not establish |
|---|---|---|
| The participant used UnvibeCode to analyze the public Flask repository. | Direct statement from the participant. | Establishes the product and repository used; no commit/version metadata was supplied. |
| The participant explored the Business Workflow Map. | Direct statement from the participant. | Establishes use of this output; not whether it was easy to navigate or accurate. |
| The participant explored the Connected Code Map. | Direct statement from the participant. | Establishes use of this output; not whether graph search, labels, or interactions were difficult. |
| The participant reviewed Business Risk Findings. | Direct statement from the participant. | Establishes that findings were examined; not whether any finding was trusted, rejected, or hard to verify. |
| The participant used LLM Context and exported the context ZIP. | Direct statement from the participant. | Establishes an export/handoff action; not whether the ZIP was difficult to use in a particular assistant. |

The project documentation describes the intended journey: docs/QUICKSTART.md covers installation and invocation; docs/HOW_IT_WORKS.md explains the output areas; docs/OUTPUTS.md explains focused and complete context exports and advises checking assistant context limits. These are product-documentation observations, not evidence that the participant experienced friction in those steps.

## Potential usability friction to test

Each item below is a hypothesis, not a confirmed complaint or bug.

| Journey point | Testable friction hypothesis | Why it could matter | Validation method |
|---|---|---|---|
| Installation and onboarding | New users may need to move between README, quick start, and deeper docs to understand prerequisites, expected time, output location, or privacy/network behavior. | Unclear setup can prevent first value. The participant’s specific setup experience was not recorded. | Give first-time developers a clean environment and measure time/errors to first completed analysis; ask them to narrate uncertainties. |
| CLI | A repository-path command may leave users unsure about available options, run scope, and what happens after completion. | Poor discoverability can make a successful first run hard to repeat. No CLI confusion was reported. | Ask participants to start a review using only help; observe lookups, retries, and successful completion. |
| Progress and feedback | During a long review, users may want stage, elapsed time, remaining work, and a clear explanation when only some outputs are ready. | Uncertainty during waits can cause abandonment. The Flask run’s progress display and duration are not available. | Record a real run and ask users to predict what is happening and what to do at each stage. |
| Workflow navigation | Users may need a more direct route from a business workflow step to its implementation and related risk evidence. | Reconstructing the evidence trail can increase time to understand behavior. No navigation difficulty was confirmed. | Give a task to trace a workflow step to code and possible failure; measure time, backtracking, and missed evidence. |
| Connected Code Map | A repository-wide graph may be difficult to orient in without search, focus, or clear edge explanations. | Users might not reach the relevant code or context export. The participant’s map interactions were not captured. | Test representative Flask tasks with search, graph focus, and current controls; compare task time and wrong selections. |
| Risk explanations | A developer may need a consistent way to distinguish source-backed evidence, inference, uncertainty, and verification steps. | Poorly calibrated trust could lead to overlooked or over-trusted findings. No Flask finding content was retained to assess. | Ask reviewers to verify several findings against Flask source; record evidence lookup time, confidence calibration, and corrections. |
| Context ZIP and AI handoff | After export, users may need to decide what to include and how to introduce the bundle to an assistant. | Extra preparation can interrupt the transition from analysis to a useful AI task. The participant confirms export, but not that it was cumbersome. | Observe a real handoff using the ZIP; record time to first useful assistant response, scope changes, and manual preparation. |
| Return usage | A completed whole-repository review may not provide an obvious recurring trigger when code changes. | Without a repeatable workflow, the tool may remain a one-time exploration aid. The participant’s later return behavior is unknown; the challenge itself identifies repeat usage as a goal. | Follow users for 30 days; measure second review, repeated repository use, and the trigger for return. |

## Prioritized recommendations

Priority estimates combine potential adoption value and confidence in the evidence. Adoption benefit is qualitative and must be validated; there is no product telemetry in this investigation.

| Priority | Recommendation | Basis | Practical first step | Expected adoption benefit |
|---|---|---|---|---|
| 1 — Test first | Add a visible, branded change-review loop for a branch or commit against a saved baseline. Show changed files and link to affected workflow, code, and risk evidence. | Engineering recommendation based on the confirmed one-time Flask exploration and the challenge’s stated repeat-usage goal. No evidence yet that this participant wanted or would use it. | Prototype local baseline metadata plus changed-file-to-existing-report links; provide a compact branded summary suitable for a pull request. | Potentially high if developers have recurring repository tasks. Measure second review within 30 days, repeat reviews per repo, and PR-summary opens. |
| 2 — Test handoff support | Add a small assistant-ready index beside the context ZIP, including repository/commit provenance, scope, estimated size, included files, and a starter prompt. | The participant confirms using LLM Context and exporting the ZIP. Documentation says users should consider assistant context limits. Friction itself remains unverified. | Observe users handing the existing export to their preferred assistant; prototype only the handoff details they need. | Potentially medium to high by reducing time from export to useful assistant work. Measure handoff time and repeat export use. |
| 3 — Test evidence continuity | Link workflow steps, graph nodes, and risk evidence with stable navigation and a clear return path. | The participant explored all three areas, but no captured behavior shows they lost context. This is a product-design hypothesis. | Run a task-based study tracing one workflow to implementation and risk evidence; add links where participants backtrack or lose their place. | Medium if it reduces investigation time. Measure task completion time and evidence coverage. |
| 4 — Test graph orientation | Add search and a focused neighborhood view with explicit edge labels if usability sessions show users struggle to find relevant code. | Based on graph usability principles; no such difficulty was reported by the participant. | Compare current graph with a focused search prototype using Flask tasks. | Medium if it improves graph-to-export conversion. Measure successful selections and time to find relevant context. |
| 5 — Test risk evidence layout | Present finding claim, source evidence, uncertainty, impact, and verification steps consistently, with direct source navigation. | The participant reviewed findings; the content needed to assess clarity was not retained. | Ask developers to verify findings against source and note which evidence fields they need. | Medium if it improves calibrated trust. Measure verification time, corrections, and confidence calibration. |
| 6 — Improve first-run guidance if testing finds gaps | Add a concise preflight and completion summary for prerequisites, repository path, expected outputs, destination, and next steps. | Documentation provides installation and workflow guidance, but the participant’s setup experience is not described. | Observe first-time installation and review without coaching; change only steps where users hesitate or fail. | Low to medium; measure install-to-complete time and support requests. |
| 7 — Improve progress guidance if testing finds gaps | Show named stages, elapsed time, partial outputs, and a useful recovery instruction when applicable. | A reasonable response to long-running CLI workflow design; no progress complaint was recorded in this Flask journey. | Capture a review session and test whether users can explain stage and next action. Coordinate with existing progress/interruption work. | Medium if waits currently cause abandonment; measure abort and recovery rates. |

## Existing issue overlap

The following open reports were checked as of 6 November 2026. They are relevant prior engineering work and should not be restated as new user findings:

- [#422: Ctrl-C leaves run status as RUNNING and shows raw tracebacks](https://github.com/FinanceFlash/unvibecode/issues/422) — overlaps interruption and recovery feedback.
- [#463: Windows console encoding failure in progress rendering](https://github.com/FinanceFlash/unvibecode/issues/463) — a specific progress-rendering defect.
- [#334: hosted quota exhaustion and missing resume/BYOK behavior](https://github.com/FinanceFlash/unvibecode/issues/334) — a specific partial-analysis/recovery request.
- [#434: arrow keys do not navigate the results dashboard tablist](https://github.com/FinanceFlash/unvibecode/issues/434) — a specific accessibility/navigation defect.

The proposed change-review loop is a recurring-use product concept, not a duplicate of those defects. This check is bounded and is not a claim that no related discussion exists elsewhere.

## Recommended validation plan

1. Capture the participant’s Flask run version, commit, command, screenshots, and any notes if available; redact secrets and personal paths.
2. Run task-based sessions with developers new to UnvibeCode, covering workflow-to-code tracing, risk verification, and assistant handoff.
3. Prototype the baseline change-review flow only after confirming an actual recurring task.
4. Track time to useful result, second use within 30 days, context export reuse, and PR report opens. Pair usage data with interviews and corrections; do not interpret clicks alone as adoption.

## Conclusion

The verified journey is that the participant explored four output areas and exported the context ZIP while analyzing public Flask. It establishes breadth of use, not a specific usability defect. The strongest adoption hypothesis is a branded change-review loop that gives developers a reason to return as code changes; validate it before treating it as a confirmed user need.

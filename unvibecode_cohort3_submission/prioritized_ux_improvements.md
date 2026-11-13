# Prioritized UX Improvements

Ranks combine adoption potential and current evidence confidence. Benefits are qualitative estimates, not measured outcomes.

| Rank | Improvement | Evidence and friction | First step | Benefit | Duplicate check |
|---|---|---|---|---|---|
| 1 | Branded change review for branch/commit | Participant completed one Flask review; challenge identifies weaker repeat use. Current journey docs describe full review, not a recurring baseline-diff loop. | Save baseline metadata; link changed files to affected workflow, graph, and risk evidence; produce a branded PR summary. | High potential: track second review in 30 days and PR link opens. | Searched open issues; no matching adoption proposal surfaced. Bounded search. |
| 2 | Assistant-ready export handoff | Participant used LLM Context and export. Docs explain focused/full export and assistant limits. | Add an index with provenance, size, included files, and starter prompt; preserve current raw exports. | High: measure export-to-assistant handoff and repeat use. | #334 is quota/resume, not handoff UX. |
| 3 | Cross-link workflow, code, and risk | Participant reviewed all three views; docs describe related evidence but no Flask screenshot captures navigation. | Deep links, breadcrumbs, and preserved selection among workflow step, graph, and risk evidence. | Medium: measure cross-view task time. | #434 concerns keyboard tab behavior; different scope. |
| 4 | Searchable graph focus mode | Participant used map and context export; docs describe hover/click interactions. No specific graph difficulty recorded. | Search path/symbol, focus one-hop neighborhood, explain edge types, show context scope. | Medium: measure graph-to-context flow. | #419 is narrow-screen layout; distinct. |
| 5 | Evidence-first risk cards | Participant reviewed findings; actual Flask finding content unavailable. | Consistent claim, evidence status, source locations, impact, unknowns, and verification steps. | Medium: measure evidence opens and corrections. | Specific risk correctness issues exist; this is presentation clarity, not a new bug claim. |
| 6 | First-run preflight and contextual CLI help | Participant completed a run. README/QUICKSTART are explicit; local CLI help displays only the repository argument. No confusion was recorded. | Show examples, version/path/scope/output, privacy/network guidance, and next step. | Low/medium: first-run completion and fewer support requests. | #422/#463 are interruption/encoding bugs, not onboarding content. |
| 7 | Stage progress and partial-result guidance | QUICKSTART promises live progress; no Flask terminal capture. | Show stage, elapsed time, available partial outputs, and recovery path when supported. | Medium: measure abort and recovery rates. | Coordinate with #422, #463, and #334; avoid duplicating those fixes. |

## Evaluation

Test with developers unfamiliar with UnvibeCode on public repositories of different sizes. Measure install-to-complete, time to answer a code question, report-to-assistant handoff time, export scope, second review in 30 days, and PR report opens. Include trust calibration and user corrections; do not optimize for clicks alone.

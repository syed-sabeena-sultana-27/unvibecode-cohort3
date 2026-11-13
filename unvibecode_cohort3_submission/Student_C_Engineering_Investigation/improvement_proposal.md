# Improvement Proposal: Resolve Workflow References to Concrete Implementations

> This file includes a bounded investigation-specific traceability fix and the prioritized Track B adoption proposal. The repeated-usage workflow is a proposal only; it is not an existing UnvibeCode capability.

## Problem statement

The Business Workflow Map route entry points to Scaffold.add_url_rule in src/flask/sansio/scaffold.py:375-441. This base hook ends by raising NotImplementedError. Flask's concrete registration implementation is App.add_url_rule in src/flask/sansio/app.py:606-662. The exported ZIP contains that source, but the workflow-specific implementation list does not identify it.

## Existing behavior

The route workflow lists Scaffold.route, Scaffold.add_url_rule, and Scaffold.endpoint as implementation references. A reader following the add_url_rule reference reaches the documented abstract contract and must discover the subclass override independently. The route summary is broadly correct; the gap is which implementation is shown as evidence.

## Proposed behavior

For a workflow reference that resolves to an abstract/base method, show both:

1. The contract/decorator and its delegation path.
2. The concrete implementation that executes for the framework class under analysis.

Label the relationship explicitly, such as “Scaffold.route delegates to App.add_url_rule through the override.” Include concrete file and line references in both the HTML workflow card and workflow_context.md. If multiple concrete implementations exist or resolution is uncertain, state that uncertainty rather than choosing one silently.

## Technical approach

- Use static class and override resolution for the repository's parsed class hierarchy.
- Starting from the workflow method, follow calls such as self.add_url_rule to the applicable subclass implementation.
- Preserve the base contract as context while marking whether it is abstract, a protocol, or a concrete implementation.
- Add source references and relationship labels to serialized workflow evidence and render them consistently in HTML and context exports.
- When more than one implementation is plausible, list candidates and mark resolution as ambiguous.
- Avoid claiming runtime dispatch was executed when only static resolution was performed.

## Developer benefit

A reviewer can move from a workflow statement to code that performs the behavior without mistaking an abstract hook for the implementation. Clear labels also make generated context more useful to an AI assistant and reduce unsupported conclusions from incomplete navigation.

## Validation strategy

Create fixtures for:
- A base method that raises NotImplementedError and one subclass override.
- A decorator that delegates via self.method.
- Multiple subclass overrides.
- A protocol/abstract declaration with no in-repository implementation.
- A direct concrete method with no override.

For Flask, the expected workflow evidence should include Scaffold.route and concrete App.add_url_rule, distinguish the abstract Scaffold.add_url_rule body, and retain its source range. Confirm that HTML and workflow_context.md agree and that chunk IDs resolve to the expected numbered source sections. No production code has been changed as part of this investigation.

## Trade-offs

Override resolution adds complexity for inheritance, mixins, dynamic assignment, and plugin registration. The analyzer should fail transparently to a base-contract-only result when static resolution is ambiguous, rather than overstate certainty or omit the uncertainty.

## Track B: Repository Change Impact Review

### Evidence-based journey review

The “actual experience” column records observed command results or artifacts. Where the workspace does not record a user's action or reaction, that absence is explicit; friction and impact are hypotheses in those rows.

| Stage and user goal | Actual experience and evidence | Observed friction / impact | Practical improvement |
|---|---|---|---|
| 1. Install: get a supported local tool | UnvibeCode 0.3.15 was already installed in the workspace virtual environment. No clean install was performed in this investigation. README documents Python 3.11+ and pip installation. | No install friction observed; clean-machine setup is untested. | Test a fresh Windows/macOS/Linux setup and refine only the steps where users fail or hesitate. |
| 2. Discover commands: learn how to start | `--help` lists `review`; `review --help` requires `--repository`. The shown command is direct. | No command discovery failure observed. There is no baseline/diff command in the inspected help, so returning after code changes has no discoverable entry point. | Add a `review --changed-since` or explicit `changes` command after baseline demand is validated; show examples and output path in help. |
| 3. First analysis: get useful outputs | The saved 6 Nov run completed; it records 194,479 estimated tokens, code-map lane 3.517 s, business lane 101.217 s, and `COMPLETE`. On 13 Nov, the default console failed printing `●`; `-X utf8` produced map and context but the hosted business lane failed with connection errors. | Confirmed Windows `cp1252` progress-rendering crash (#659); retry remains vulnerable to hosted-service/network failure. Impact: the default invocation can stop before the full review. | Make progress output encoding-safe and show a clear, reliable retry/recovery path. The defect is already reported; this is not a new issue claim. |
| 4. Understand workflows: verify what the repository does | The prior map's JSON response explanation agrees with Flask source. The route card points to `Scaffold.add_url_rule` but not concrete `App.add_url_rule`. | Confirmed evidence-navigation gap; a developer must inspect inheritance and search for the concrete implementation. | Link base contracts to concrete implementations and label the relation. This overlaps existing reports #281/#243. |
| 5. Explore connected code: find related files and symbols | A fresh Connected Code Map artifact was created in the 13 Nov partial run. The saved complete ZIP has 403 verified cross-file connections in its manifest. No screenshot or interaction trace is available. | No map usability complaint or specific graph error observed. Difficulty locating a node is a hypothesis, not a finding. | Test search/focus tasks; add neighborhood focus or edge explanations only if developers struggle. |
| 6. Review risks: decide what deserves investigation | The saved full run shows `NO_REPORTABLE_FINDINGS`, 12 candidates, 7 rejected, and 5 investigation gaps. The report cautions that zero accepted findings is not proof of no defects. The new run produced no risk report. | No false risk finding was verified. The 13 Nov run's incomplete coverage could be mistaken for a clean result if partial state is missed. | Keep completion coverage and “not analyzed” states prominent beside counts; do not show an empty report as a completed zero-risk result. |
| 7. Export context: take source into another tool | The saved context ZIP (269,911 bytes) contains manifest, chunks, connections, selections, unresolved relationships, README, and workflow context. Its README instructs users to attach `workflow_context.md` and `chunks.jsonl` together. | The files explain how to use the bundle, but there is no evidence the investigator used the bundle in an external assistant or encountered handoff friction. | Test time-to-first-useful assistant answer; if users need it, add a concise provenance/size index and starter prompt. |
| 8. Reuse results in development: apply understanding to a task or PR | The ZIP README supplies prompts for understanding workflows, planning a change, and reviewing risks. No actual code change, PR, assistant conversation, or context reuse was retained. | Reuse value and friction are unmeasured. Manual copy into a PR or assistant may interrupt work; this is a hypothesis. | Offer a user-reviewed branded Markdown summary and focused context export, without automatic publication. |
| 9. Return after code changes: get value from the next commit | The inspected CLI/help and output docs describe full reviews and snapshots, with no saved baseline/change-review workflow. No return visit after modifying code was observed. | Product-surface gap confirmed; whether it drives weak retention is a hypothesis consistent with the challenge prompt, not measured user research. | Prototype the Repository Change Impact Review below; measure second review in 30 days and task time before investing in full incremental analysis. |

### Developer problem and evidence

The completed Flask trial produced a connected-code map, complete context ZIP, workflow map, and risk report. Those outputs explain a repository snapshot. The installed CLI exposes one analysis command (`review --repository`) and has no baseline, Git-diff, branch, or pull-request option. The output documentation explains full and focused context handoff, but the inspected help/docs provide no repeatable workflow for refreshing the understanding after code changes. This is an observed product-surface gap; the assumption that it will increase retention must be tested with developers.

### Proposed journey

1. On the first `review`, offer an explicit **Save this review as a baseline** action that stores repository identity, commit, file fingerprints, workflow references, source chunks, and verified graph connections.
2. After a commit or branch change, let the developer run **Review changes**. Show changed files and symbols, then link to baseline workflows, nearby code connections, affected risk evidence, and candidate tests. Mark each impact as a static link or a hypothesis, with direct source and commit references.
3. Generate a compact, branded Markdown pull-request summary and a focused assistant context bundle for the changed area. The developer reviews and copies the text; the tool does not publish it automatically.

### Technical feasibility from the current architecture

- **Available building blocks:** the current review already prepares a static code graph, source chunks, cross-file connections, per-file context selections, workflow references, and risk outputs. The exported context format includes `manifest.json`, `chunks.jsonl`, `connections.jsonl`, `selections.jsonl`, and `workflow_context.md`.
- **Missing capability:** current CLI help only offers `review` and `--repository`; it does not identify a saved-baseline or change-review command. The installed CLI performs a fresh review and saves new result folders. No claim is made that incremental analysis already exists.
- **Feasible MVP path:** use Git's changed-file list between a stored base commit and the current commit; map changed paths/symbol ranges to the baseline graph and workflow references; then rank affected workflows using direct file/symbol links. Re-run analysis for the changed files plus their connected neighborhood, while labeling unverified transitive or business impacts as candidates. Preserve a full-review fallback when symbols, branch ancestry, or graph coverage are uncertain.
- **Architecture dependency:** the client can compute a diff and present stored graph/context, but reliable refreshed workflows and risk deltas require the analysis service to accept focused changed context and return comparable structured outputs. The current client does not establish that server capability, so an MVP needs a service contract change or a less ambitious local-only affected-reference view.

### MVP scope and implementation stages

1. **Baseline format:** store commit SHA, source-file hashes, symbol and file IDs, workflow-to-source references, risk IDs, analysis version, and a schema version. Exclude credentials and repository source from telemetry; let the user choose a local baseline directory.
2. **Diff and impact view:** use `git diff --name-status <base>...<head>`; map added/modified/deleted paths to baseline graph nodes and workflow evidence; show direct matches separately from inferred neighbor impacts. Handle renames, deleted files, uncommitted changes, shallow clones, and missing baselines explicitly.
3. **Focused refresh and summary:** submit only selected changed context plus relevant connected chunks to a service endpoint that supports stable workflow/risk IDs and `added / changed / removed / unchanged` states. Generate a user-reviewed Markdown summary and context bundle. If the service cannot return comparable results, ship stage 2 as an evidence navigator and label it as such.

### Success measures

- **Repeat use:** percentage of first-time review users who run a second change review on the same repository within 30 days; compare against a matched cohort without the feature.
- **Useful impact:** engineer-labeled precision and recall of affected workflows on a benchmark of real pull requests; record false negatives separately from low-confidence candidates.
- **Time saved:** median time to answer “what workflows may this change affect?” versus manual code search, measured in task sessions.
- **PR adoption:** percentage of change reviews where users copy/export the summary and developer rating of its usefulness. Do not optimize only for click-through.
- **Trust:** rate at which developers can navigate to supporting code and correctly distinguish verified links from hypotheses.

### Risks and limits

Static imports/call edges cannot prove runtime paths or business impact. A changed helper may affect code through reflection, configuration, generated code, or external calls that the graph cannot resolve. Baselines can become stale across rebases and analyzer upgrades. Stable IDs and migration rules are needed; confidence labels and a full-review fallback are required to avoid implying complete impact coverage. Repeat usage and retention are hypotheses until measured.

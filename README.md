# UnvibeCode × Engineering Challenge 2026 — Cohort 3

This repository combines a portfolio copy of the public UnvibeCode repository with an independent Cohort 3 challenge submission. The original project and my investigation are described separately below.

The upstream snapshot and existing Git history are preserved through commit `c75b75e26cfd2cca923d2030f3b0a7056eadd89d` (4 November 2026).

## About UnvibeCode

[UnvibeCode](https://github.com/FinanceFlash/unvibecode) analyzes a repository and produces a Business Workflow Map, a Connected Code Map, Business Risk Findings, and a Complete Repository Context export. The aim is to help developers trace how application behavior relates to source code and investigate possible risks.

The product's published repository is primarily documentation, workflow packs, and related materials. The installable CLI is distributed as the `unvibecode` Python package; this portfolio repository does not contain the package's full implementation source. See the [original UnvibeCode README](README_UNVIBECODE_ORIGINAL.md) and its [licensing clarification](docs/LICENSE_CLARIFICATION.md) for product details and license scope.

## Cohort 3 challenge work

I reviewed UnvibeCode's outputs on the public [Flask](https://github.com/pallets/flask) repository at commit `49943b5a94413a530761350f04e896f76e8d620e`.

The engineering investigation traced two Flask workflows against source code:

1. Creating a JSON HTTP response from supplied values (`jsonify` and the active JSON provider).
2. Registering URL rules and endpoint-to-view associations (`Scaffold.route`, the concrete `App.add_url_rule`, and request dispatch).

The JSON workflow's main explanation matched Flask's source. The route workflow was directionally accurate, but its workflow-specific evidence pointed to a base method that raises `NotImplementedError` without surfacing the concrete application implementation. This is a traceability limitation in the generated report, not a Flask routing failure. A separate Windows console encoding crash was reproduced, but already exists in the UnvibeCode issue tracker. No new issue was submitted because the confirmed candidates were duplicate or overlapping reports.

For developer adoption, I propose a visible, branded **Repository Change Impact Review**: compare a changed branch or commit with a saved analysis, link changed code to potentially affected workflows and risks, and prepare a developer-reviewed pull request summary. The current CLI does not offer baseline or change-review functionality; the proposal explains the implementation boundary and how to evaluate it.

## Detailed reports

- [Official Cohort 3 challenge brief](docs/UnvibeCode_Engineering_Challenge_2026_Cohort_3.md)
- [Engineering investigation](unvibecode_cohort3_submission/Student_C_Engineering_Investigation/engineering_investigation.md)
- [Workflow-to-code verification](unvibecode_cohort3_submission/Student_C_Engineering_Investigation/workflow_code_verification.md)
- [Evidence and validation](unvibecode_cohort3_submission/Student_C_Engineering_Investigation/evidence_and_validation.md)
- [Developer adoption and change-impact proposal](unvibecode_cohort3_submission/Student_C_Engineering_Investigation/improvement_proposal.md)
- [Final submission summary](unvibecode_cohort3_submission/Student_C_Engineering_Investigation/final_submission.md)
- [Track A decision: no issue submitted](unvibecode_cohort3_submission/Student_C_Engineering_Investigation/no_issue_submitted.md)
- [Developer adoption report](unvibecode_cohort3_submission/developer_adoption_report.md)
- [User journey analysis](unvibecode_cohort3_submission/user_journey_analysis.md)
- [Prioritized UX improvements](unvibecode_cohort3_submission/prioritized_ux_improvements.md)
- [Screenshot evidence and limitations](unvibecode_cohort3_submission/screenshot_evidence.md)
- [Saved analysis summary and artifact notes](unvibecode_cohort3_submission/evidence/flask-analysis-20261106/analysis-summary.md)
- [Saved complete Flask report](unvibecode_cohort3_submission/evidence/flask-analysis-20261106/flask-unvibecode-full.html)
- [Flask repository context export](unvibecode_cohort3_submission/evidence/flask-analysis-20261106/flask-repository-context.zip)

The saved complete report is dated 6 November 2026. A fresh review on 13 November produced code-map and context outputs, but its hosted workflow/risk analysis failed before completing. The evidence documents distinguish the two runs. No participant screenshots were available, and none are presented as evidence.

## Repository contents

```text
.
├── .github/                         CI and repository guidance
├── AI Engineering Cheatsheet/       AI engineering guides
├── docs/                            Product documentation and sample analyses
├── prebuilt-workflow-paths/         Example workflow packs
├── skills/                          UnvibeCode-related skill materials
├── unvibecode_cohort3_submission/   Independent challenge reports and evidence
├── LICENSE                          Original project license
├── README.md                        Portfolio overview
└── README_UNVIBECODE_ORIGINAL.md    Preserved upstream product README
```

Local virtual environments, caches, temporary analysis results, and raw run logs are excluded by `.gitignore`. The curated 6 November report and context export are included under the challenge evidence folder.

## Install and run UnvibeCode

Requires Python 3.11 or newer and internet access for hosted business analysis. Install the published package:

```bash
python -m pip install --upgrade unvibecode
python -m unvibecode --help
python -m unvibecode review --repository "/path/to/repository"
```

On Windows, use a quoted Windows path, for example:

```powershell
py -m unvibecode review --repository "D:\Projects\my-repository"
```

The supported command and output scope can vary by package version. Check the CLI's completion status before treating a report as complete. No customer OpenAI API key is required; analysis uses UnvibeCode's hosted service as described in the [data processing documentation](docs/DATA_PROCESSING.md).

## Tools used for this challenge

- UnvibeCode CLI 0.3.15 and its generated HTML/context outputs.
- Python 3.13.6 and Git for environment, repository, and source inspection.
- Flask source at the commit recorded above; function-level references are in the workflow verification report.
- GitHub issue tracker review for duplicate checking.

## Project and submission are distinct

The UnvibeCode product materials in this repository remain the upstream project's work. The Cohort 3 documents are my independent analysis and proposal; they do not claim to be official product documentation or an accepted contribution. No GitHub issue, pull request, or challenge form was submitted as part of this preparation.

## License

The original [LICENSE](LICENSE) and [licensing clarification](docs/LICENSE_CLARIFICATION.md) are preserved. UnvibeCode documents a mixed licensing model for the official Python package, so do not assume every packaged asset is covered by the repository's Apache license. The Flask context export includes source excerpts and is accompanied by the applicable [Flask license notice](unvibecode_cohort3_submission/evidence/flask-analysis-20261106/FLASK_LICENSE.txt).

The challenge submission is independent analysis. No separate license has been selected for those materials in this preparation; confirm the intended license scope before publication if you want to grant reuse rights.

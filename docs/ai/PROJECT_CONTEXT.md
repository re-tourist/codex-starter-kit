# PROJECT_CONTEXT

## 1. Project Summary

- project_name: codex-starter-kit
- project_type: tooling / infra
- description: A repository starter kit for milestone-driven Codex workflows.
- primary_stack: Markdown, TOML, GitHub templates, PowerShell-friendly docs.

## 2. Current Phase

- current_milestone: rule-layer hardening
- why_this_phase_exists: make milestone -> issue -> implementation deterministic and repeatable.
- what_this_phase_should_prove: a single milestone spec can reliably generate an issue plan draft and then issue bodies without ad hoc prompts.
- out_of_scope: scripts, parsers, API automation, and directory re-architecture.

## 3. Supported Milestone Types

The supported milestone types are fixed:

- freeze
- feature
- research
- refactor
- infra
- evaluation
- docs

Rules:

- type must be one of the supported values above.
- type selects the default issue skeleton used for decomposition.
- type is a policy signal, not a free-text label.

## 4. Default Skeletons by Milestone Type

Use these as the default issue skeletons before pruning by scope.

### feature
- design / contract
- dataset / input
- model / core logic
- train / integration
- eval / output contract
- docs / validation / closeout

### research
- protocol freeze
- baseline reproduction
- method insertion
- experiment execution
- result analysis
- docs / closeout

### refactor
- boundary freeze
- interface migration
- internal refactor
- regression validation
- docs / closeout

### freeze
- contract freeze
- allowed-change definition
- validation gate
- closeout / handoff

### infra
- environment setup
- tooling update
- integration validation
- docs / closeout

### evaluation
- metric contract
- baseline comparison
- run execution
- analysis / report
- docs / closeout

### docs
- source review
- structure / template update
- example / guidance
- validation / consistency check
- closeout

Rules:

- default skeletons are starting points only.
- the milestone spec may prune or merge skeletons.
- implementation issues must not appear before required design / freeze work.

## 5. Module Map

The canonical module enum for this repository is:

- data
- dataset
- model
- train
- eval
- infra
- docs
- experiment

Rules:

- default issue split is by module.
- each issue should keep one primary module whenever possible.
- cross-module issues need explicit justification in the milestone spec.
- module names must not be invented ad hoc.

## 6. Task Decomposition Policy

These rules are mandatory for issue derivation:

- the milestone spec is the only upstream source for issue derivation.
- the first generated artifact must be an issue plan draft, not a full issue body.
- issue plan drafts are for human review of structure, dependency, and coverage.
- each issue must have a single primary responsibility.
- every issue must state its input, output, and acceptance clearly.
- design / freeze issues must come before implementation issues.
- validation / docs / closeout issues must come after implementation issues.
- do not exceed the milestone's `max_issue_count` without human approval.

Default issue plan fields:

- issue_id
- title
- issue_type
- module
- goal
- depends_on
- priority

## 7. Priority Policy

Priority meaning is fixed:

- P0: blocking, correctness or contract failure, stop and escalate.
- P1: serious, must fix before milestone close.
- P2: non-blocking follow-up, can be scheduled later.

Ordering rules:

- P0 outranks P1, which outranks P2.
- dependency order always stays explicit even when priority is higher.
- when unsure, prefer the higher priority rather than hiding risk.

## 8. Issue Derivation Policy

The issue derivation flow is fixed:

1. choose the default skeleton from milestone type.
2. prune the skeleton by `in_scope` and `out_of_scope`.
3. apply `must_keep`, `must_change`, and `must_not_change` as compatibility constraints.
4. map `required_outputs` into output-oriented issues such as eval, docs, or validation.
5. split by module with one primary module per issue.
6. assign dependency edges so design / freeze issues appear before implementation issues.
7. emit a reviewable issue plan draft before any issue body is written.
8. expand each issue body only after the issue plan draft is approved.

The issue body must inherit milestone-spec terminology whenever possible.
Do not rename the same concept across milestone spec, issue plan, issue body, and PR body.

## 9. Canonical Docs Map

- `docs/ai/WORKFLOW_GUIDE.md`: milestone compilation workflow.
- `docs/plan/plan_stage.template.md`: milestone spec template.
- `docs/plan/issue_stage.template.md`: issue plan draft and issue expansion rules.
- `docs/contracts/commit_message_format.md`: commit format contract.
- `.github/ISSUE_TEMPLATE.md`: GitHub issue body template.
- `.github/pull_request_template.md`: GitHub PR body template.
- `templates/PR_TEMPLATE.md`: canonical PR body template.
- `templates/issue_report_template.md`: canonical issue report template.
- `templates/milestone_review_report.template.md`: canonical milestone review report template.
- `docs/review/code_review.template.md`: review checklist and verdict format.
- `docs/handoff/milestone_closeout.template.md`: milestone closeout and handoff template.

## 10. Stop Conditions

Stop and report instead of pushing forward if:

- the requested change requires a new external dependency.
- the requested change would alter the directory structure.
- the milestone spec is missing and cannot be inferred safely.
- the issue plan would exceed the allowed max issue count.
- an issue would need to violate a frozen contract.
- a validation step is missing for a P0 or P1 change.

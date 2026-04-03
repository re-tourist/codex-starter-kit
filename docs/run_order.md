# run_order

This file is the command execution ledger for the repository.

## Format

- Write one command group per section.
- Start each group with a comment line that explains why the commands are being run.
- Include an ISO 8601 timestamp in the comment line.
- Put one command per line under the comment.
- Add a blank line between command groups.

## Example

# [2026-04-03T10:00:00+08:00] inspect repository policy docs
Get-Content AGENTS.md
Get-Content docs\ai\WORKFLOW_GUIDE.md

# [2026-04-03T10:05:00+08:00] verify milestone templates
Get-Content docs\plan\plan_stage.template.md
Get-Content docs\plan\issue_stage.template.md
# [2026-04-03T00:00:00+08:00] verify git and github tooling before sync
git branch --show-current
Get-Command gh -ErrorAction SilentlyContinue
git remote -v
# [2026-04-03T00:05:00+08:00] create sync branch and inspect staged scope
git checkout -b codex/github-sync-rule-layer
git diff --stat
# [2026-04-03T00:10:00+08:00] stage and commit rule-layer sync
git add -A
git commit -m "docs(workflow | rule-layer): sync milestone compilation templates" -m "why:" -m "- make the starter kit deterministic for milestone-to-issue derivation and keep the repository-level rules aligned across AGENTS, workflow, and templates." -m "what:" -m "- add the project context rule layer, milestone spec template, issue plan draft template, command log, and synchronized GitHub/report templates." 

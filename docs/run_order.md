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
# [2026-04-03T00:15:00+08:00] push sync branch to origin
git push -u origin codex/github-sync-rule-layer
# [2026-04-03T00:20:00+08:00] verify clean working tree after push
git status --short
git log -1 --oneline
# [2026-04-03T00:25:00+08:00] commit run_order audit entry
git add docs/run_order.md
git commit -m "docs(run_order | audit): record GitHub sync ledger" -m "why:" -m "- keep the execution ledger aligned with the repository rule that command groups must be recorded before material task steps." -m "what:" -m "- add the GitHub sync and verification entries to docs/run_order.md so the audit trail is preserved in the repo history." 
git push
# [2026-04-03T00:30:00+08:00] push audit log commit
git push
# [2026-04-03T00:35:00+08:00] final commit and push for run_order log
git add docs/run_order.md
git commit -m "docs(run_order | audit): record GitHub push log" -m "why:" -m "- keep the command execution ledger committed so the repository mirrors the same audit trail that was used during the GitHub sync." -m "what:" -m "- add the final sync entries to docs/run_order.md and publish them with the branch history." 
git push

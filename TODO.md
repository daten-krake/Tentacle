# TODO: Lint-on-Promote Workflow

## Goal

Create `.github/workflows/lint-promote.yml` that triggers when rules are promoted to `flight/` or `prod/`, runs `tentacle-lint --strict` on them, and handles failures.

## Must-fix before shipping

- [ ] **No auto-revert from prod** — `flight/` auto-reverts to `dev/` on lint failure. `prod/` creates a GitHub Issue instead — no auto-revert.
- [ ] **Concurrency** — add `concurrency: group: lint-promote cancel-in-progress: false`
- [ ] **Pin lint version** — `env: TENTACLE_LINT_VERSION: "v0.1.0"`, deliberate bumps only
- [ ] **Use `yq` instead of `sed`** for YAML state mutation — `yq -i '.state = "dev"'`
- [ ] **Filename collision check** — before any move, ensure no duplicate filenames across the revert set
- [ ] **`workflow_run` conclusion guard** — `if: github.event.workflow_run.conclusion == 'success'` + add `workflow_dispatch` trigger
- [ ] **Exit code 2 handling** — 0=pass, 1=failures+revert logic, 2=runtime error (fail immediately, do nothing)
- [ ] **Audit trail** — commit message includes lint errors, job summary lists reverted files, prod failures create Issues

## Workflow flow (once implemented)

```
1. trigger: workflow_run (route workflow succeeded) + workflow_dispatch
2. concurrency group serializes runs
3. checkout default branch
4. find YAMLs in Detections/flight/ and Detections/prod/
5. none found → skip
6. download pinned tentacle-lint (v0.1.0), verify SHA256
7. run tentacle-lint --strict --format json on flight/
8. run tentacle-lint --strict --format json on prod/
9. exit code 2 → fail workflow immediately, no changes
10. exit code 0 → done, all passed
11. exit code 1:
    a. flight/ failures → yq '.state = "dev"', mv to dev/, commit with errors in message
    b. prod/ failures → create GitHub Issue with lint details, do NOT revert
    c. check for filename collisions before any move
12. job summary with filenames and lint errors per file
```

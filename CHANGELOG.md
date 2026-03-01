## v1.0.12 — 2026-03-01

## What's Changed
* chore: batch update changelog for all skipped releases by @greynewell in https://github.com/greynewell/claude-software-factory/pull/267
* fix: add Bash(date:*) to allowedTools in batch-changelog.yml and changelog.yml by @greynewell in https://github.com/greynewell/claude-software-factory/pull/269


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v1.0.11...v1.0.12

## v1.0.11 — 2026-03-01

## What's Changed
* chore: batch update changelog for all skipped releases by @greynewell in https://github.com/greynewell/claude-software-factory/pull/261
* docs: instruct Claude to checkout PR head branch when responding to PR comments by @greynewell in https://github.com/greynewell/claude-software-factory/pull/265
* fix: add idempotency check when gh pr create fails after successful push by @greynewell in https://github.com/greynewell/claude-software-factory/pull/264


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v1.0.10...v1.0.11

## v1.0.10 — 2026-03-01

## What's Changed
* fix: add gh label create guard and tool permission to changelog.yml by @greynewell in https://github.com/greynewell/claude-software-factory/pull/257


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v1.0.9...v1.0.10

## v1.0.9 — 2026-03-01

## What's Changed
* chore: batch update changelog for all skipped releases by @greynewell in https://github.com/greynewell/claude-software-factory/pull/254
* fix: add duplicate-PR guard to batch-changelog.yml by @greynewell in https://github.com/greynewell/claude-software-factory/pull/258


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v1.0.8...v1.0.9

## v1.0.8 — 2026-03-01

## What's Changed
* fix: add in-flight guard to batch-changelog triggers in proactive scanners by @greynewell in https://github.com/greynewell/claude-software-factory/pull/249
* fix: add gh label create guard in batch-changelog.yml by @greynewell in https://github.com/greynewell/claude-software-factory/pull/248


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v1.0.7...v1.0.8

## v1.0.7 — 2026-03-01

## What's Changed
* chore: batch update changelog for all skipped releases by @greynewell in https://github.com/greynewell/claude-software-factory/pull/244
* fix: embed failing check names in CI failure comment from shepherd by @greynewell in https://github.com/greynewell/claude-software-factory/pull/250


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v1.0.6...v1.0.7

## v1.0.6 — 2026-03-01

## What's Changed
* fix: add --delete-branch to changelog gh pr merge commands by @greynewell in https://github.com/greynewell/claude-software-factory/pull/242


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v1.0.5...v1.0.6

## v1.0.5 — 2026-03-01

## What's Changed
* chore: batch update changelog for all skipped releases by @greynewell in https://github.com/greynewell/claude-software-factory/pull/237
* fix: close changelog-skipped issues via PR body Closes syntax by @greynewell in https://github.com/greynewell/claude-software-factory/pull/239


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v1.0.4...v1.0.5

## v1.0.4 — 2026-03-01

## What's Changed
* fix: update batch-changelog prompt to parse tag from correct title format by @greynewell in https://github.com/greynewell/claude-software-factory/pull/233


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v1.0.3...v1.0.4

## v1.0.3 — 2026-03-01

## What's Changed
* chore: batch update changelog for all skipped releases by @greynewell in https://github.com/greynewell/claude-software-factory/pull/228
* fix: handle TOCTOU race in auto-tag git push by @greynewell in https://github.com/greynewell/claude-software-factory/pull/234


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v1.0.2...v1.0.3

## v1.0.2 — 2026-03-01

## What's Changed
* fix: add actions:write permission and batch-changelog recovery to weekly scanner by @greynewell in https://github.com/greynewell/claude-software-factory/pull/223


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v1.0.1...v1.0.2

## v1.0.1 — 2026-03-01

## What's Changed
* chore: batch update changelog for all skipped releases by @greynewell in https://github.com/greynewell/claude-software-factory/pull/219
* fix: use exact tag title match for changelog-skipped dedup by @greynewell in https://github.com/greynewell/claude-software-factory/pull/224


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v1.0.0...v1.0.1

## v1.0.0 — 2026-03-01

## What's Changed
* fix: use full commit message format for BREAKING CHANGE footer detection by @greynewell in https://github.com/greynewell/claude-software-factory/pull/214


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v0.16.1...v1.0.0

## v0.16.1 — 2026-03-01

## What's Changed
* chore: batch update changelog for all skipped releases by @greynewell in https://github.com/greynewell/claude-software-factory/pull/210
* fix: add concurrency group to batch-changelog.yml to prevent duplicate PRs by @greynewell in https://github.com/greynewell/claude-software-factory/pull/215


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v0.16.0...v0.16.1

## v0.12.11 — 2026-03-01

## What's Changed
* fix: add id-token: write permission to changelog.yml by @greynewell in https://github.com/greynewell/claude-software-factory/pull/191
* fix: add retry loop for changelog commit push to reduce Changelog-skipped failures by @greynewell in https://github.com/greynewell/claude-software-factory/pull/189


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v0.12.10...v0.12.11

## v0.12.10 — 2026-03-01

## What's Changed
* fix: add author whitelist to issue_comment and pull_request_review_comment triggers by @greynewell in https://github.com/greynewell/claude-software-factory/pull/181


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v0.12.9...v0.12.10

## v0.12.9 — 2026-03-01

## What's Changed
* fix: add authorization gate for pull_request_review trigger by @greynewell in https://github.com/greynewell/claude-software-factory/pull/177
* fix: add Bash(gh release:*) to claude.yml allowedTools by @greynewell in https://github.com/greynewell/claude-software-factory/pull/176
* feat: add health check for claude-code-review.yml in proactive scanner by @greynewell in https://github.com/greynewell/claude-software-factory/pull/175


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v0.12.8...v0.12.9

## v0.12.8 — 2026-02-28

## What's Changed
* fix: add --limit 100 to gh pr list in claude-pr-shepherd.yml by @greynewell in https://github.com/greynewell/claude-software-factory/pull/169


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v0.12.7...v0.12.8

## v0.12.7 — 2026-02-28

## What's Changed
* fix: skip CHANGES_REQUESTED notification when review predates latest commit by @greynewell in https://github.com/greynewell/claude-software-factory/pull/162


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v0.12.6...v0.12.7

## v0.12.6 — 2026-02-28

## What's Changed
* fix: add idempotency guard to auto-tag.yml to prevent spurious 'Release missing' issues by @greynewell in https://github.com/greynewell/claude-software-factory/pull/164
* feat: add Bash(gh run view:*) and Bash(gh run list:*) to allowedTools in claude.yml by @greynewell in https://github.com/greynewell/claude-software-factory/pull/163


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v0.12.5...v0.12.6

## v0.12.5 — 2026-02-28

## What's Changed
* fix: add claude-task label to auto-tag notification issues by @greynewell in https://github.com/greynewell/claude-software-factory/pull/156
* fix: add Bash(gh run view:*) to allowedTools in claude-proactive.yml by @greynewell in https://github.com/greynewell/claude-software-factory/pull/155


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v0.12.4...v0.12.5

## v0.12.4 — 2026-02-28

## What's Changed
* fix: add Bash(gh run view:*) to allowedTools in claude-self-improve.yml by @greynewell in https://github.com/greynewell/claude-software-factory/pull/148


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v0.12.3...v0.12.4

## v0.12.0 — 2026-02-28

## What's Changed
* feat: add workflow_dispatch trigger to auto-tag.yml by @greynewell in https://github.com/greynewell/claude-software-factory/pull/134


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v0.11.2...v0.12.0

## v0.9.10 — 2026-02-28

## What's Changed
* fix: handle git push failure after successful rebase in auto-tag.yml by @greynewell in https://github.com/greynewell/claude-software-factory/pull/112


**Full Changelog**: https://github.com/greynewell/claude-software-factory/compare/v0.9.9...v0.9.10

## v0.11.2 — 2026-02-28

- fix: remove ambiguous label guard note from shepherd prompt

## v0.11.1 — 2026-02-28

- fix: add claude-task label guard to merge step in pr-shepherd

## v0.11.0 — 2026-02-28

- feat: add Bash(gh run list:*) to deep scan allowedTools

## v0.10.0 — 2026-02-28

- fix: address shepherd health check review feedback
- feat: add shepherd health check to proactive scanner

## v0.9.13 — 2026-02-28

- fix: add @claude trigger to auto-tag failure notification issue body

## v0.9.12 — 2026-02-28

- fix: handle gh release create failure in auto-tag workflow

## v0.9.11 — 2026-02-28

- fix: add updatedAt to pr list and gate stuck-shepherd on 2h threshold

## v0.9.9 — 2026-02-28

- fix: handle git pull --rebase failure in auto-tag with fallback and notification

## v0.9.8 — 2026-02-28

- fix: add || true to tag pipeline to prevent pipefail abort on empty grep
- fix: use parameter expansion for v0.0.0 fallback in auto-tag.yml

## v0.9.7 — 2026-02-28

- fix: update changelog before tagging so tagged commit contains changelog entry
- fix: move mergeable:null guard to early-exit in shepherd step 4

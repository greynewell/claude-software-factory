## v0.15.2 — 2026-03-01

- fix: add --repo flag to gh pr merge and gh issue edit in changelog workflows

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

## v0.9.8 — 2026-02-28

- fix: add || true to tag pipeline to prevent pipefail abort on empty grep
- fix: use parameter expansion for v0.0.0 fallback in auto-tag.yml

## v0.9.7 — 2026-02-28

- fix: update changelog before tagging so tagged commit contains changelog entry
- fix: move mergeable:null guard to early-exit in shepherd step 4

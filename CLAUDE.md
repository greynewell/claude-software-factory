# Claude Software Factory — Claude Instructions

This repo is the factory itself. It is a GitHub Actions template that autonomously
implements, reviews, and merges code. It improves itself via the same loop it provides
to users.

## Pull Requests

Always create PRs using `gh pr create`. Never substitute a compare link.

```
gh pr create \
  --repo OWNER/REPO \
  --title "..." \
  --body "..." \
  --base main \
  --head <branch>
```

The PR `--body` must include `Closes #<issue-number>` so GitHub auto-closes the originating
issue on merge. Example body footer:

```
Closes #42
```

After creating a PR, apply the `claude-task` label so the stale workflow does not auto-close it:

```
gh issue edit <PR-number> --repo OWNER/REPO --add-label claude-task
```

(GitHub treats PRs as issues for the label API, so `gh issue edit` works on PR numbers.)

Always run this as the final step. The PR must exist before marking the task complete.

## Issues

When creating a GitHub issue, always include `@claude` at the end of the body so the
workflow auto-triggers. Example closing line:

```
@claude please implement this
```

## Development

This repo contains only GitHub Actions YAML and shell scripts. There is no compiled code.

- Validate YAML: `find .github/workflows -name '*.yml' -exec python3 -c "import yaml,sys; yaml.safe_load(open(sys.argv[1]))" {} \; && echo "All YAML valid"`
- No build or test commands required beyond YAML validation

Before committing, confirm all workflow YAML is syntactically valid.

## Self-Improvement Loop

The factory runs on itself:
1. `claude-proactive.yml` (hourly) and `claude-self-improve.yml` (weekly) scan for issues
2. Issues trigger `claude-auto-assign.yml` → `claude.yml` implements them
3. `claude-code-review.yml` reviews the PR
4. `claude-pr-shepherd.yml` merges when CI passes
5. `auto-tag.yml` tags the release
6. Repeat

When filing improvement issues, be specific about which workflow file, what line or
behavior to change, and why it improves the factory.

## Commits

Use [Conventional Commits](https://www.conventionalcommits.org/):

- `feat:` — new workflow or capability (bumps MINOR version)
- `fix:` — bug fix in workflow logic (bumps PATCH version)
- `feat!:` or `BREAKING CHANGE` — breaking change to the loop (bumps MAJOR version)
- `chore:`, `docs:`, `test:`, `refactor:` — no version bump

## Branch Naming

`claude/issue-{number}-{YYYYMMDD}-{HHMM}`

## PR Branch Checkout

When triggered by a comment or review on a **pull request**, `actions/checkout` in
`claude.yml` resolves `github.sha` to the default branch (`main`) — not the PR head
branch. Any file edits or commits will silently target the wrong branch unless you
explicitly check out the PR branch first.

**Before making any file changes when responding to a PR comment or review**, run:

```bash
# Get the PR head branch (replace <PR-number> with the actual PR number from context)
PR_BRANCH=$(gh pr view <PR-number> --json headRefName -q .headRefName)

# Fetch and switch to the correct branch
git fetch origin "$PR_BRANCH"
git checkout "$PR_BRANCH"
```

How to detect you are in a PR context: the task context will show `is_pr: true` or the
triggering comment URL will contain `/pull/`. When unsure, run `gh pr view <number>` —
if it succeeds, always checkout its head branch before editing any files.

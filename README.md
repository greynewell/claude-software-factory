# Claude Software Factory

**Open an issue. Get a pull request.**

Six workflow files that turn any GitHub repo into a self-running software factory. You write issues. [Claude Code](https://docs.anthropic.com/en/docs/claude-code) writes the code, reviews PRs, fixes comments, merges when CI is green, tags releases, and scans for bugs — in a loop.

No application code. No runtime. No server. Just GitHub Actions.

## What happens when you create an issue

1. You open a GitHub issue ending with `@claude`
2. Claude reads the issue, creates a branch, writes the code, opens a PR
3. A second Claude instance reviews the PR and posts comments
4. If there are review comments, Claude fixes them automatically
5. When CI is green and reviews pass, the PR gets merged
6. A semver tag is created from the commit message
7. An hourly scan finds new bugs and TODOs — files more issues — and the loop continues

## The Lifecycle

```
 ┌─────────────────────────────────────────────────────────────┐
 │                                                             │
 │   ┌──────────┐    ┌──────────────┐    ┌──────────────┐     │
 │   │  ISSUE   │───▶│ AUTO-ASSIGN  │───▶│  CLAUDE CODE │     │
 │   │ created  │    │ @claude      │    │  implements   │     │
 │   └──────────┘    └──────────────┘    └──────┬───────┘     │
 │        ▲                                      │             │
 │        │                                      ▼             │
 │   ┌────┴─────┐                         ┌──────────────┐    │
 │   │ PROACTIVE│                         │  PULL REQUEST │    │
 │   │ SCANNER  │                         │  opened       │    │
 │   │ (hourly) │                         └──────┬───────┘    │
 │   └──────────┘                                │             │
 │        ▲                                      ▼             │
 │        │                              ┌───────────────┐    │
 │        │                              │  CODE REVIEW   │    │
 │        │                              │  (automated)   │    │
 │        │                              └───────┬───────┘    │
 │        │                                      │             │
 │        │                                      ▼             │
 │        │                              ┌───────────────┐    │
 │        │                              │  PR SHEPHERD   │    │
 │        │                              │  fix comments  │    │
 │        │                              │  check CI      │    │
 │        │                              │  merge when    │    │
 │        │                              │  ready         │    │
 │        │                              └───────┬───────┘    │
 │        │                                      │             │
 │        │         ┌──────────────┐             │             │
 │        │         │  AUTO-TAG    │◀────────────┘             │
 │        └─────────│  semantic    │     (merged to main)      │
 │                  │  versioning  │                            │
 │                  └──────────────┘                            │
 │                                                             │
 └─────────────────────────────────────────────────────────────┘
```

### Phase 1: Issue Creation

An issue is created — either by a human or by the proactive scanner. The issue body ends with `@claude` to signal that Claude should pick it up.

**Workflow:** `claude-auto-assign.yml`
**Trigger:** `issues.opened`
**Behavior:** Checks if the author is an org member (or Claude itself). If so, posts `@claude please implement this issue` as a comment, which triggers the next phase.

### Phase 2: Implementation

Claude Code receives the `@claude` mention and goes to work. It reads the issue, creates a branch, writes the code, verifies the build, and opens a pull request.

**Workflow:** `claude.yml`
**Trigger:** `@claude` mention in issue comment, PR comment, or review
**Behavior:** Full implementation cycle — branch, code, build, commit, PR. Claude has access to git, gh, and your project's build/lint tools.

### Phase 3: Code Review

The moment a PR is opened (or updated), automated code review kicks in. Claude Code reviews the diff and posts comments on potential issues.

**Workflow:** `claude-code-review.yml`
**Trigger:** `pull_request` opened, synchronized, ready_for_review, reopened
**Behavior:** Runs the `code-review` plugin from Claude Code Actions, posting review comments directly on the PR.

### Phase 4: PR Shepherd

Every 15 minutes, the shepherd checks all open PRs. It reads review comments, applies fixes, verifies CI, and merges when everything is green.

**Workflow:** `claude-pr-shepherd.yml`
**Trigger:** Cron (`*/15 * * * *`) + manual dispatch
**Behavior:**
1. Fetches unresolved review comments (including from CodeRabbit or other bots)
2. Applies fixes and commits them
3. Checks CI status
4. Merges via rebase when: CI green, no unresolved comments, not draft, no conflicts

### Phase 5: Semantic Versioning

When a PR merges to `main`, the auto-tagger examines the commit message and bumps the version accordingly.

**Workflow:** `auto-tag.yml`
**Trigger:** Push to `main`
**Behavior:**
| Commit pattern | Version bump |
|---|---|
| `BREAKING CHANGE` or `type!:` | MAJOR (resets minor + patch) |
| `feat:` or `feat(scope):` | MINOR (resets patch) |
| Everything else | PATCH |

### Phase 6: Proactive Scanning

Once per hour, Claude scans the codebase looking for problems and opportunities. It creates up to 3 issues per run, each ending with `@claude please implement this`, feeding the loop.

**Workflow:** `claude-proactive.yml`
**Trigger:** Cron (`0 * * * *`) + manual dispatch
**Detects:**
- Logic errors, unhandled errors, race conditions
- Missing tests
- Performance issues
- Security concerns
- TODO/FIXME comments
- Feature gaps

## Setup (3 steps)

1. **Click "Use this template"** to create a new repository (or copy `.github/workflows/` into an existing one)

2. **Add your API key as a secret:**
   ```
   Settings → Secrets and variables → Actions → New repository secret
   Name: ANTHROPIC_API_KEY
   Value: <your key from console.anthropic.com>
   ```

3. **Install the Claude GitHub App** at [github.com/apps/claude](https://github.com/apps/claude) and grant it access to your new repo

That's it. Create an issue ending with `@claude please implement this` and watch it go.

### Optional: Customize for your stack

Edit `CLAUDE.md` with your language, build, lint, and test commands. Search for `# CUSTOMIZE:` in the workflow files to lock down tool access. The template ships language-agnostic — it works with Go, Node, Python, Rust, or anything with a CLI build tool.

## File Structure

```
.github/
├── ISSUE_TEMPLATE/
│   ├── feature.yml              # Feature request (auto-includes @claude)
│   └── bug.yml                  # Bug report (auto-includes @claude)
├── PULL_REQUEST_TEMPLATE.md     # PR template
└── workflows/
    ├── claude.yml               # Core: responds to @claude mentions
    ├── claude-auto-assign.yml   # Gates and triggers Claude on new issues
    ├── claude-code-review.yml   # AI code review on every PR
    ├── claude-pr-shepherd.yml   # Merges when ready, asks Claude to fix comments
    ├── claude-proactive.yml     # Hourly codebase scan, files issues
    └── auto-tag.yml             # Semantic versioning from conventional commits
.claude/
└── settings.json                # Sandbox config for Claude Code
CLAUDE.md                        # Project instructions for Claude
```

## Customization

### Language Support

The template ships language-agnostic. Anywhere you see `# CUSTOMIZE:` in the workflow files, replace the placeholder commands with your own:

| Placeholder | Example (Go) | Example (Node) | Example (Python) |
|---|---|---|---|
| `your-build-command` | `go build ./...` | `npm run build` | `python -m py_compile *.py` |
| `your-lint-command` | `go vet ./...` | `npm run lint` | `ruff check .` |
| `your-test-command` | `go test ./...` | `npm test` | `pytest` |

### Org Membership Check

`claude-auto-assign.yml` verifies the issue author is an org member before triggering Claude. To change this:

- **Open to everyone:** Remove the org membership check entirely
- **Specific users:** Replace with a username allowlist
- **Label-based:** Trigger only on issues with a specific label

### PR Merge Strategy

The shepherd uses `--rebase` by default. Change to `--squash` or `--merge` in `claude-pr-shepherd.yml` to match your preference.

### Proactive Scanner Frequency

Default: hourly. Adjust the cron in `claude-proactive.yml`:
- `0 */4 * * *` — every 4 hours
- `0 9 * * 1-5` — weekdays at 9am
- Remove entirely if you only want human-created issues

## Secrets Reference

| Secret | Required | Used By |
|---|---|---|
| `ANTHROPIC_API_KEY` | Yes | All Claude workflows |
| `GITHUB_TOKEN` | Auto-provided | All workflows (GitHub Actions default) |

## Design Principles

**Closed loop.** Every output feeds back into the system. Merged PRs trigger tags. Proactive scans create issues. Issues trigger implementations.

**Human steering.** Humans create issues and set priorities. They can review PRs before the shepherd merges, or let it run fully autonomous. The level of oversight is a dial, not a switch.

**Fail safe.** Every workflow is designed to do nothing rather than do harm. If CI is red, the shepherd waits. If the build breaks, Claude won't merge. If the proactive scanner finds nothing, it creates no issues.

**One PR at a time.** The shepherd processes PRs sequentially to avoid merge conflicts and maintain a clean history.

**Conventional commits.** The auto-tagger relies on [Conventional Commits](https://www.conventionalcommits.org/) (`feat:`, `fix:`, `BREAKING CHANGE`) to determine version bumps. Claude is instructed to follow this convention in `CLAUDE.md`.

## What this is NOT

This is not a hosted service, a SaaS product, or a managed platform. It's 6 YAML files. You own the workflows, you control the prompts, you pay Anthropic directly for API usage. There's no middleman and no vendor lock-in beyond the Claude API itself.

## Credits

Extracted from [Uncompact](https://github.com/supermodeltools/Uncompact) by [Grey Newell](https://github.com/greynewell).

## License

MIT

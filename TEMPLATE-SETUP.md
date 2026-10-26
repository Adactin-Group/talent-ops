# New project setup checklist

Complete this on day one for every repository created from `ai-dev-template`.
GitHub copies **files** from a template, **not settings**: rulesets, security
settings, Actions policy, variables and team access must be applied again.
Work top to bottom — the order matters.

## 1. Create the repository

- [ ] *Use this template* → *Create a new repository* in the `Adactin-Group` organisation
- [ ] Visibility agreed with the Technical Director (public only if the code may be visible to anyone)
- [ ] Clone it, then create the integration branch:
      `git switch -c dev` → `git push -u origin dev`

## 2. Repository settings (Settings → General)

- [ ] Pull requests: **squash merging only**; "Always suggest updating PR branches" on; "Automatically delete head branches" on; auto-merge off
- [ ] Wikis, Projects and Discussions off unless needed

## 3. Access (Settings → Collaborators and teams)

- [ ] `platform-admins` Admin · `leads` Maintain · `engineers` Write · `security-reviewers` **Write** (code owners need write access)
- [ ] No individual (non-team) access

## 4. Actions policy (Settings → Actions → General)

The organisation policy is already set; confirm the repository matches it.

- [ ] "Allow Adactin-Group, and select non-Adactin-Group, actions and reusable workflows"
- [ ] "Allow actions created by GitHub" ticked; "Marketplace verified creators" **unticked**
- [ ] "Require actions to be pinned to a full-length commit SHA" **ticked**
- [ ] Workflow permissions: **read repository contents**; Actions may **not** create or approve pull requests
- [ ] Fork pull request workflows: require approval for all external contributors
- [ ] Verify: `gh api repos/Adactin-Group/<repo>/actions/permissions` shows `"allowed_actions": "selected"` and `"sha_pinning_required": true`

> Every `uses:` in a workflow must be pinned to a full commit SHA with a version
> comment, e.g. `actions/checkout@<40-char-sha> # v4`. Get a SHA with
> `gh api repos/<owner>/<action>/commits/<tag> --jq .sha`. Unpinned actions fail
> instantly with "Startup failure" and 0s elapsed. Any non-GitHub action must be
> approved and added to the allowed list deliberately.

## 5. Security (Settings → Advanced Security)

- [ ] Dependency graph, Dependabot alerts and Dependabot security updates on
- [ ] Secret scanning and **push protection** on
- [ ] Private vulnerability reporting on
- [ ] CodeQL analysis → **Default** setup

## 6. Variables (Settings → Secrets and variables → Actions → Variables)

- [ ] `OPENSPEC_VERSION` = the OpenSpec version the team uses (`openspec --version`)

## 7. Replace placeholders

- [ ] `openspec/config.yaml` — project, owners, risk tier, data classification
- [ ] `CLAUDE.md` — project name, purpose, stack, tier
- [ ] `.github/CODEOWNERS` — confirm `@Adactin-Group/...` teams; adjust security-sensitive paths
- [ ] `SECURITY.md` — security contact
- [ ] `README.md` — project description

Raise these as the first pull request (`chore: configure project from template`)
**before** step 8, so the checks run once.

## 8. Branch rulesets (Settings → Rules → Rulesets)

Create `protect-main` (target: default branch), then copy it as `protect-dev` (target: `dev`).

| Rule | Setting |
|---|---|
| Enforcement | Active |
| Bypass list | **Empty** — in an emergency an admin disables the ruleset (audited) |
| Restrict deletions | On |
| Require linear history | On |
| Block force pushes | On |
| Require a pull request before merging | On — see approvals below |
| Require conversation resolution | On |
| Allowed merge methods | Squash |
| Require status checks to pass | On, plus "Require branches to be up to date" |
| Required checks | `PR title follows Conventional Commits`, `PR checklist and AI declaration`, `OpenSpec validation`, `Dependency review` |
| Require code scanning results | On → CodeQL |
| Restrict updates / creations, signed commits | Off (signed commits: later step) |

> **Order matters.** Required checks can only be picked from the dropdown after
> they have run once on a pull request. Never type check names by hand — a name
> that is never reported blocks every merge.

**Approvals — depends on team size:**

| Team | Required approvals | Code Owner review | Approval of most recent push |
|---|---|---|---|
| One maintainer only | 0 | Off | **Off** (otherwise nothing can merge) |
| Two or more reviewers | **1** | **On** | **On** |

- [ ] Switch to the two-reviewer settings the day a second reviewer joins

## 9. Prove the gate works

- [ ] Direct push to `main` is rejected (`GH013: Repository rule violations`)
- [ ] A test PR titled `bad title` with an empty description fails two checks and cannot be merged
- [ ] Close the test PR: `gh pr close <number> --delete-branch`

## 10. Developer machines

- [ ] Node.js 20.19+, Git, GitHub CLI (`gh auth login`), Claude Code installed
- [ ] `npm install -g @fission-ai/openspec@latest`
- [ ] OpenSpec telemetry off: `openspec config set telemetry.enabled false`
- [ ] 2FA on every GitHub account
- [ ] Each developer has read `CLAUDE.md` and the AI acceptable-use rules
- [ ] gitleaks installed: `winget install --id Gitleaks.Gitleaks -e` (Mac: `brew install gitleaks`)
- [ ] Pre-commit hooks enabled once per clone: `git config core.hooksPath .githooks` (first line of defence; `git commit --no-verify` skips it, so GitHub push protection is the backstop)

## 11. First change

- [ ] First feature raised with `/opsx:propose`, reviewed by a human, merged by pull request

- [ ] Commit signing set up (SSH signing key added to GitHub as a *signing* key; `commit.gpgsign true`) - required once 'Require signed commits' is on

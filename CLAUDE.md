# CLAUDE.md — instructions for AI coding assistants

This repository follows the Adactin AI Governance Framework. These rules apply to
Claude Code and any other AI assistant working here. Humans remain accountable
for every change.

## Project

- Name: <PROJECT_NAME>
- Purpose: <ONE_LINE_PURPOSE>
- Stack: <e.g. Angular / Bun + Hono / PostgreSQL / Terraform / Azure>
- Risk tier: <1|2|3|4> · Data classification: <...>
- Specs and project rules: `openspec/config.yaml`, `openspec/specs/`

## How work is done

1. Every feature or fix starts as an OpenSpec change: `/opsx:propose`.
2. A human reviews `proposal.md`, `design.md` and `tasks.md` before any code.
3. Implement with `/opsx:apply` on a feature branch only.
4. Open a pull request into `dev`. CI and a human code owner must approve.
5. After merge, archive the change with `/opsx:archive`.

## Git rules

- Branch names: `feat/<short-name>`, `fix/<short-name>`, `chore/<short-name>`.
- Conventional commit messages (`feat:`, `fix:`, `chore:`, `docs:`, `test:`).
- Add the trailer `AI-Assisted: claude-code` to commits you author.
- Never push to `main` or `dev`, never force-push, never rewrite shared history.

## Never do

- Read, create or print secrets, `.env` files, keys, certificates or Terraform state.
- Use real personal, employee, candidate or client data, even in tests. Use synthetic data.
- Run cloud commands that change resources or access (`az`, `terraform apply`, `gh secret`, `gh api` writes).
- Disable, skip or weaken tests, linters, security scans or CI checks.
- Modify `.github/`, `.claude/`, `CLAUDE.md`, `SECURITY.md` or `openspec/config.yaml` unless the task is a governance change.
- Invent business rules, permissions, prices, legal requirements or approvals. Ask instead.

## Secure coding baseline

- Validate all input at the boundary; encode all output.
- Parameterised queries only; no string-built SQL.
- Deny-by-default authorization, checked on the server for every request.
- No `eval`, dynamic `require` or shell execution built from user input.
- Log events, not personal data; never log tokens, passwords or document contents.
- Treat uploaded files as untrusted: check type and size, store privately, scan.

## Dependencies

- Do not add a dependency without stating why in `design.md`.
- Confirm the package exists, is maintained and is the intended package (beware typosquats).
- Commit lockfile changes with the change that needs them.

## When unsure

Stop and ask. A question costs minutes; a wrong assumption in auth, data or
infrastructure costs far more.

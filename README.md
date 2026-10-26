# ai-dev-template

Governed starting point for AI-native projects at Adactin, where engineers build with
AI coding assistants such as Claude Code.

## What it gives a new project

- **Spec-driven workflow** with OpenSpec: every change starts as a reviewed proposal.
- **AI-assistant rules**: `CLAUDE.md` and `.claude/settings.json` define what agents may and may not do.
- **Review ownership**: `.github/CODEOWNERS` routes governance, infrastructure and security code to the right reviewers.
- **Pull request discipline**: a template that records AI assistance and security impact.
- **Security policy**: `SECURITY.md` and private vulnerability reporting.
- **Secret hygiene**: `.gitignore` blocks keys, `.env` files and Terraform state.

CI quality gates, security scanning and branch rulesets are added in later steps.

## Start a new project

1. *Use this template* → *Create a new repository*.
2. Work through [`TEMPLATE-SETUP.md`](TEMPLATE-SETUP.md) on day one.

## Workflow

`/opsx:propose` → human review → `/opsx:apply` on a feature branch → pull request to `dev`
→ CI + code-owner approval → merge → `/opsx:archive`.

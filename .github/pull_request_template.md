## Summary

<!-- What does this change do, and why? One or two sentences. -->

**OpenSpec change:** `openspec/changes/<change-name>` (or "n/a - governance/chore")

## Type

- [ ] Feature
- [ ] Fix
- [ ] Chore / refactor
- [ ] Governance / CI / infrastructure

## AI assistance

- [ ] No AI assistance
- [ ] AI-assisted (tool: <!-- e.g. Claude Code -->). I have read and understood every line and can explain it.

## Author checklist

- [ ] Tests added or updated, and passing locally
- [ ] No secrets, keys, `.env` files, real personal data or client data
- [ ] No new dependency, OR each new dependency is justified in `design.md`
- [ ] No checks, tests or scans were disabled or skipped
- [ ] Documentation and specs updated where behaviour changed

## Security impact

Does this change touch any of the following? If yes, tick it and request a security reviewer.

- [ ] Authentication or sessions
- [ ] Authorization, roles or permissions
- [ ] Personal, financial or identity data
- [ ] File upload or download
- [ ] External integration, webhook or API
- [ ] Infrastructure, pipelines or AI-assistant configuration
- [ ] AI/LLM feature or prompt

**Threat model:** update `docs/security/threat-model.md` in this PR if anything above is ticked.
If security-sensitive files changed but the threat is unchanged, tick this and explain below:

- [ ] Threat model: no update needed

**Threat considerations / mitigations:**
<!-- Brief STRIDE notes for anything ticked above, or "None". -->

## Rollback

<!-- How do we undo this if it goes wrong? -->

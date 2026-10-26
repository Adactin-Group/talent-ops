# Security Policy

## Reporting a vulnerability

Please do **not** open a public issue for security problems.

- Use GitHub's **private vulnerability reporting**: the *Security* tab →
  *Report a vulnerability*, or
- Email **<security-contact@adactin.com>**.

Include what you found, how to reproduce it and the potential impact. Do not
access, modify or retain data that is not yours while investigating.

## What to expect

| Step | Target |
|---|---|
| Acknowledgement | 2 business days |
| Initial assessment | 5 business days |
| Fix or mitigation for critical issues | 7 days |
| Fix or mitigation for high issues | 30 days |

We will keep you informed and credit you, with your permission, once fixed.

## Scope

In scope: the code in this repository and its CI/CD workflows.
Out of scope: third-party services, social engineering and denial-of-service testing.

## Our commitments in this repository

- No secrets or real personal data are stored in the repository.
- Secret scanning with push protection, dependency alerts and code scanning are enabled.
- Changes to `main` require a pull request, passing checks and code-owner review.
- AI-assisted changes follow the same review and security gates as all other changes.

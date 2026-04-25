# Security

Security in clinical software is not optional. A breach of clinical data is a breach of patient trust, and patient trust is the substrate of clinical care. This chapter covers the basics. The basics are most of what you need.

## The mindset

You don't need to be a security expert to build secure clinical software. You need to take a small number of practices seriously, every time, without exceptions.

The bar is not 'no vulnerabilities ever'. The bar is 'no obvious, easily-exploited vulnerabilities, and a clear path to fix the ones you find'.

## Secrets management

**Rule one: never commit credentials to source control.** Not API keys, not database passwords, not OAuth client secrets, not signed certificates. Not even 'just for now', not even 'in a private repo'.

Practical patterns:

- Use a `.env` file for local secrets, gitignored. Use a library like `python-dotenv` or `pydantic-settings` to load it.
- Use environment variables in production, populated by your hosting platform's secret store.
- Use a secret manager (Bitwarden, 1Password, HashiCorp Vault, AWS Secrets Manager, GitHub Actions secrets) for shared secrets.
- Add a pre-commit hook that scans for accidentally-staged secrets. `gitleaks` and `detect-secrets` are good options.
- If a secret is committed by accident, **rotate it**. Removing it from the Git history doesn't help; assume it's already harvested.

## Authentication and authorisation

A few rules:

- **Don't roll your own auth.** Use a vetted library. For Django, use `django.contrib.auth`. For FastAPI, use `fastapi-users` or integrate with an OAuth provider. For NHS-facing tools, use NHS login or NHS CIS2 as appropriate.
- **Hash passwords with a modern algorithm.** Argon2 or bcrypt. Never store passwords in plaintext. Never roll your own hashing.
- **Use HTTPS everywhere.** Including local development if you can. Let's Encrypt makes this free. There is no excuse for HTTP in 2026.
- **Distinguish authentication (who are you) from authorisation (what can you do).** A logged-in user is not necessarily an authorised user. Check permissions on every request that touches data.
- **Default deny.** Permissions should be opt-in, not opt-out. A new endpoint should require explicit permission to access, not require explicit denial.
- **Don't trust the client.** Client-side validation is a UX feature, not a security control. Validate everything on the server too.

## Data minimisation and pseudonymisation

The safest data is the data you don't have.

- **Collect only what you need.** Every field you collect is a field that can leak. If you don't need date of birth, don't collect it.
- **Pseudonymise where possible.** Replace identifiers with stable but non-identifying tokens. Pseudonymisation is not anonymisation; the original data still exists somewhere, but the data in use can't directly identify the patient.
- **Anonymise where you can.** If you genuinely don't need to re-identify, fully anonymise. For research datasets, aim for k-anonymity or stronger.
- **Encrypt at rest and in transit.** Modern hosting platforms make this easy. Use it.
- **Audit access.** For any system holding patient data, log who accessed what, when. Audit logs are also a clinical safety control: they let you investigate when something goes wrong.

## Common vulnerabilities to know

You should at least be familiar with the OWASP Top 10. The ones that bite clinician-developers most often:

- **Injection.** SQL injection, command injection, XSS. Use ORMs (don't build SQL by string concatenation), use templating libraries that auto-escape (Jinja2, Django templates), validate inputs.
- **Broken authentication.** Session fixation, weak passwords, no rate limiting on login. Use a vetted auth library and don't override its defaults without thinking.
- **Sensitive data exposure.** Data over HTTP, secrets in logs, error messages that leak stack traces. Treat your logs as a security boundary too.
- **Broken access control.** Forgetting to check authorisation on a new endpoint. Default deny mitigates most of this.
- **Vulnerable dependencies.** Use `pip-audit`, `npm audit`, or GitHub Dependabot. Keep dependencies patched.

## Dependencies

Modern software is mostly other people's code. Each dependency is a security surface.

- **Pin versions.** Don't deploy `package>=1.0`; deploy `package==1.4.7`. Reproducibility is a security property too.
- **Audit regularly.** Run `pip-audit` (Python), `npm audit` (Node), or equivalent for your language. Dependabot in GitHub will open PRs for security updates.
- **Be selective.** A library that does what you need with three dependencies is safer than one with three hundred. Don't install a dependency for something a few lines of standard library code would do.
- **Update on a cadence.** Security patches that sit unmerged for months are the worst of both worlds. Pick a cadence (weekly, monthly) and stick to it.

## Threat modelling

For any clinical system, ask:

- **Who are the realistic attackers?** Disgruntled insiders, opportunistic external attackers, automated bots. Most clinical software is not nation-state target.
- **What are they after?** Patient data, credentials, compute resources, reputational damage.
- **What's the worst case?** Patient harm, reportable data breach, ICO fine, loss of trust.
- **What controls reduce the worst case?** Access control, audit logging, encryption, data minimisation, incident response plan.

You don't need a formal threat model document for a small project. You do need to have thought about it.

## Incident response

When (not if) something goes wrong:

1. **Contain.** Stop the bleeding. Disable affected accounts, take affected services offline if necessary.
2. **Assess.** What was accessed, by whom, when, how. Get this from logs.
3. **Notify.** If patient data was exposed, the ICO has a 72-hour notification clock under UK GDPR. Affected individuals also need to be told. Your organisation's information governance lead is your first call.
4. **Patch.** Fix the underlying vulnerability. Don't just rotate the affected credential.
5. **Learn.** Write the incident up. What controls failed, what controls saved you, what changes prevent recurrence.

## Resources

- OWASP Top 10: <https://owasp.org/www-project-top-ten/>
- NHS Digital Data Security and Protection Toolkit: <https://www.dsptoolkit.nhs.uk/>
- ICO guidance on personal data breaches: <https://ico.org.uk/for-organisations/report-a-breach/>
- `gitleaks`: <https://github.com/gitleaks/gitleaks>
- `pip-audit`: <https://github.com/pypa/pip-audit>

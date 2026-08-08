# Security Policy

Slang processes customer conversations across many independent organizations.
A vulnerability here is not an inconvenience — it can expose one company's
private communications to another. We treat security reports with corresponding
seriousness.

---

## Supported versions

| Version | Supported |
|---|:---:|
| `0.x` (pre-release) | Latest only |

Once Slang reaches `1.0`, this table will list the current major version plus
the previous one for twelve months.

---

## Reporting a vulnerability

**Do not open a public issue, discussion, or pull request for a security
vulnerability.** Public disclosure before a fix puts every user at risk.

### GitHub Security Advisories

Report privately via
**[Report a vulnerability](https://github.com/QadeesAsghar/slang-platform/security/advisories/new)**.
This creates a private thread visible only to maintainers, and lets us
coordinate disclosure with you.

This is currently the **only** reporting channel. Slang does not yet operate a
security mailbox, and we would rather say so than publish an address that
nobody reads. If you cannot use GitHub advisories, open a normal issue asking
for a private contact - **without any vulnerability detail in it** - and we
will arrange a channel.

---

## What to include

The more of this you provide, the faster the fix:

- **Type** of vulnerability (e.g. XSS, IDOR, tenant isolation bypass, SSRF)
- **Affected component** and version or commit SHA
- **Reproduction steps** — precise enough for us to reproduce independently
- **Proof of concept**, if you have one
- **Impact** — what an attacker gains
- **Any suggested mitigation**

---

## Our commitment

| Stage | Target |
|---|---|
| Acknowledgement | **48 hours** |
| Initial assessment and severity | **5 business days** |
| Status updates | Every **7 days** until resolved |
| Fix for critical severity | **30 days** |
| Public disclosure | **90 days**, or sooner once a fix ships |

We will credit you in the advisory and release notes unless you prefer to remain
anonymous. Tell us which you want.

---

## Scope

### In scope

- `slang-platform` — the monorepo, which contains the API, the dashboard, and
  the widget
- **Tenant isolation failures** — any path where one organization can reach another's data. We treat these as critical by default.
- Authentication and session handling
- Authorization and privilege escalation
- Injection (SQL, command, template), XSS, SSRF, CSRF
- Insecure direct object references
- Secrets exposed in code, logs, or API responses
- Widget vulnerabilities that could compromise a **customer's** website

### Out of scope

- Denial of service and volumetric attacks
- Social engineering of staff or users
- Findings from automated scanners with no demonstrated exploitability
- Missing hardening headers with no exploit path
- Vulnerabilities in third-party dependencies already publicly disclosed and pending an upstream patch
- Issues requiring physical access or a compromised device
- Self-XSS
- Reports about email SPF/DKIM/DMARC configuration on non-mail domains

**There is no hosted Slang service yet.** Slang is in early development and is
not deployed anywhere. Any domain currently serving something under the Slang
name is not operated by this project, and reports about it are out of scope.

---

## Safe harbour

We will not pursue legal action against researchers who:

- Make a good-faith effort to avoid privacy violations, data destruction, and service disruption
- Only interact with accounts they own or have explicit permission to test
- **Do not access, modify, or retain data belonging to other organizations** — if you encounter such data, stop immediately and report it
- Give us reasonable time to remediate before public disclosure
- Do not exploit the finding beyond what is required to demonstrate it

---

## Bug bounty

**There is no bounty programme, and no rewards of any kind.** Slang is in early
development and has no paid tier, no merchandise, and no platform credit to
give. We would rather state that plainly than imply a reward that does not
exist.

What we can offer is public credit in the advisory and the release notes, if
you want it. A formal programme may follow once the platform reaches general
availability.

---

## Security practices

For transparency, and limited to what is actually implemented and verifiable in
the repository today:

- Passwords hashed with **Argon2id** at OWASP baseline parameters, never stored
  in plaintext or reversibly encrypted
- **Tenant isolation enforced at the database layer** through PostgreSQL
  row-level security and a non-superuser application role, not by application
  logic alone. An automated isolation suite runs as a release gate
- Session tokens are httpOnly, are never returned in a response body, and are
  stored hashed
- Audit logging on authentication, permission, and configuration changes, in an
  append-only table where `UPDATE` and `DELETE` are revoked at the database level
- Secrets are kept in environment configuration and excluded from version
  control by `.gitignore`

**Not yet in place**, listed so this page cannot be mistaken for more than it
is: transport security and infrastructure hardening (nothing is deployed),
automated dependency scanning, code scanning, secret-scanning push protection,
and any external security review.
- Least-privilege role-based access control

---

*Last updated: 2026-08-02*

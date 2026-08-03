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

### Preferred: GitHub Security Advisories

Report privately via
**[Report a vulnerability](https://github.com/slang/slang-platform/security/advisories/new)**.
This creates a private thread visible only to maintainers, and lets us issue a
CVE and coordinate disclosure with you.

### Alternative: Email

**security@slang.com**

Encrypt with our PGP key if the report is sensitive. Key fingerprint published at
`https://slang.com/.well-known/security.txt`.

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

- `slang-platform`, `slang-api`, `slang-widget`, `slang-sdk-js`, `slang-integrations`
- The hosted service at `*.slang.com`
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

We do not currently run a paid bounty programme. We do offer public credit,
Slang swag, and free platform credit for valid reports. A formal programme is
planned once the platform reaches general availability.

---

## Security practices

For transparency, current measures:

- Passwords hashed with **Argon2id**, never stored in plaintext or reversibly encrypted
- All traffic over **TLS 1.3**
- Tenant isolation enforced at the **database layer** via row-level security, not application logic alone
- Secrets held in environment configuration, never committed — enforced by push protection
- **Dependabot** and **CodeQL** run on every repository
- Audit logging on all authentication, permission, and configuration changes
- Least-privilege role-based access control

---

*Last updated: 2026-08-02*

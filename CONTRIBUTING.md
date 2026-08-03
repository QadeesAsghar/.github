# Contributing to Slang

Thanks for considering a contribution. This guide covers everything from a typo
fix to a new integration.

By participating you agree to our [Code of Conduct](CODE_OF_CONDUCT.md).

---

## Ways to contribute

You do not need to write code to be useful:

| Contribution | Where |
|---|---|
| Report a bug | [Bug Reports](https://github.com/slang/slang-community/discussions/categories/bug-reports) |
| Suggest a feature | [Feature Requests](https://github.com/slang/slang-community/discussions/categories/feature-requests) |
| Improve documentation | [`slang-docs`](https://github.com/slang/slang-docs) |
| Build an integration | [`slang-integrations`](https://github.com/slang/slang-integrations) |
| Translate the widget | [`slang-widget`](https://github.com/slang/slang-widget) |
| Answer questions | [Q&A](https://github.com/slang/slang-community/discussions/categories/q-a) |
| Write code | Read on |

**New here?** Start with [`good first issue`](https://github.com/search?q=org%3Aslang+label%3A%22good+first+issue%22+state%3Aopen&type=issues).

---

## Before you write code

**Open an issue or discussion first** for anything beyond a small fix.

This is not bureaucracy — it protects your time. A large PR that does not match
the planned architecture is painful for everyone to reject, and we would much
rather redirect the effort before you spend it.

No issue needed for: typos, broken links, obvious documentation errors, or
comment clarifications. Just open the PR.

---

## Development setup

### Prerequisites

| Tool | Version |
|---|---|
| Node.js | 24 LTS or later |
| pnpm | 9+ (`corepack enable`) |
| Docker | For PostgreSQL and Redis |
| Git | 2.40+ |

### Getting started

```bash
git clone https://github.com/slang/slang-platform.git
cd slang-platform

corepack enable
pnpm install

cp .env.example .env.local

docker compose up -d          # PostgreSQL + Redis
pnpm db:migrate
pnpm db:seed

pnpm dev
```

The app runs with a **completely empty `.env.local`** — no third-party
credentials required. Email prints to the terminal, unconfigured OAuth providers
hide their buttons, and AI features stay behind a feature flag. If you hit a
setup step that demands a paid service, that is a bug — please report it.

---

## Workflow

### 1. Branch

Branch from `main` using the pattern `type/short-description`:

```
feat/conversation-search
fix/widget-mobile-scroll
docs/webhook-examples
refactor/inbox-state
test/auth-flow
chore/bump-drizzle
```

### 2. Commit

We follow [Conventional Commits](https://www.conventionalcommits.org/). Commit
messages drive changelog generation and semantic versioning, so the format is
enforced by a hook.

```
feat(inbox): add saved reply shortcuts
fix(widget): prevent scroll lock on iOS Safari
docs(api): document pagination cursors
perf(api): add composite index on conversation lookup
```

Types: `feat` · `fix` · `docs` · `style` · `refactor` · `perf` · `test` · `build` · `ci` · `chore`

Breaking changes get a `!` and a `BREAKING CHANGE:` footer:

```
feat(api)!: rename conversation.status values

BREAKING CHANGE: `open` is now `active`. Update webhook consumers.
```

### 3. Verify before pushing

```bash
pnpm lint
pnpm typecheck
pnpm test
pnpm build
```

These are the exact checks CI runs. Running them locally saves a round trip.

### 4. Open a pull request

- Fill in the PR template completely
- Link the issue: `Closes #123`
- Keep it focused — one concern per PR
- Add screenshots or a recording for any UI change
- Mark it draft if it is not ready

---

## Standards

### Code

- **TypeScript strict mode.** No `any` without a comment justifying it.
- **Validate at the boundary.** Every external input goes through a Zod schema.
- **Never trust the client for authorization.** Enforce in the API, every time.
- **Every query is tenant-scoped.** A query without a tenant filter is a data leak, not a bug.
- **Small modules.** If a file needs a table of contents, split it.
- **Readable over clever.** The next reader is you, in six months.

### Tests

Required for: new features, bug fixes (a regression test proving the fix), and
any change to authentication, authorization, or tenant isolation.

```bash
pnpm test              # unit + integration
pnpm test:e2e          # Playwright
pnpm test:watch
```

### Accessibility

Non-negotiable, especially in the widget — it renders on other people's sites.

- Semantic HTML before ARIA
- Every interactive element reachable by keyboard
- Visible focus states
- WCAG AA contrast minimum
- Screen-reader tested for new UI

### Performance

The widget has a **hard budget of 15 KB gzipped**. A PR that exceeds it will not
be merged without an explicit exemption. CI reports the delta on every PR.

---

## Review

| | |
|---|---|
| First response | Within 3 business days |
| What we look at | Correctness, security, tenant isolation, tests, accessibility, performance, readability |
| Approval | At least one maintainer |
| Merge | Squash, using the PR title as the commit message |

Review comments are about the code, never the person. If feedback ever reads
otherwise, tell us — that is a Code of Conduct matter and we want to know.

---

## Licensing of contributions

By contributing you agree that your work is licensed under the repository's
licence:

| Repository | Licence |
|---|---|
| `slang-platform`, `slang-api` | AGPL-3.0 |
| `slang-widget`, `slang-sdk-js`, `slang-examples` | MIT |
| `slang-integrations` | Apache-2.0 |
| `slang-docs`, `slang-community` | CC-BY-4.0 (code samples MIT) |

---

## Recognition

Contributors are credited in release notes and listed in the repository. Regular
contributors may be invited to become maintainers.

---

## Questions

Ask in [Discussions](https://github.com/slang/slang-community/discussions) —
there is no such thing as a question too basic.

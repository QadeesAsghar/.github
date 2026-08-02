<!--
Thanks for contributing to Slang.
Fill in the sections that apply and delete the rest.
-->

## Summary

<!-- What does this change and why? One or two sentences. -->

## Related issue

<!-- "Closes #123" or "Part of #123". Open an issue first for anything non-trivial. -->

Closes #

## Type of change

- [ ] 🐞 Bug fix (non-breaking change that fixes an issue)
- [ ] ✨ New feature (non-breaking change that adds functionality)
- [ ] 💥 Breaking change (existing behaviour changes)
- [ ] 📖 Documentation
- [ ] ♻️ Refactor (no behaviour change)
- [ ] ⚡ Performance
- [ ] 🧪 Tests
- [ ] 🔧 Build / CI / tooling

## How was this tested?

<!-- Describe what you ran and what you verified manually. -->

- [ ] Unit tests added or updated
- [ ] Integration tests added or updated
- [ ] E2E tests added or updated
- [ ] Manually verified

## Screenshots or recording

<!-- Required for any UI change. Before/after is ideal. -->

## Checklist

- [ ] `pnpm lint` passes
- [ ] `pnpm typecheck` passes
- [ ] `pnpm test` passes
- [ ] `pnpm build` succeeds
- [ ] Commits follow [Conventional Commits](https://www.conventionalcommits.org/)
- [ ] Documentation updated, if behaviour changed
- [ ] No secrets, tokens, or customer data in the diff

## Security and tenancy

<!-- Delete this section only if the change touches no data access whatsoever. -->

- [ ] All new queries are **tenant-scoped**
- [ ] Authorization is enforced **server-side**, not in the client
- [ ] All external input is validated with a Zod schema
- [ ] No sensitive values added to logs or error responses

## Accessibility

<!-- Required for UI changes. -->

- [ ] Keyboard navigable
- [ ] Visible focus states
- [ ] Meets WCAG AA contrast
- [ ] Semantic HTML, ARIA only where genuinely needed

## Performance

- [ ] No unnecessary re-renders introduced
- [ ] No N+1 queries introduced
- [ ] Widget bundle stays within the **15 KB gzipped** budget (if applicable)

## Breaking changes

<!-- If checked above: what breaks, and what should consumers do about it? -->

## Notes for reviewers

<!-- Anything you want a reviewer to look at closely, or decisions you were unsure about. -->

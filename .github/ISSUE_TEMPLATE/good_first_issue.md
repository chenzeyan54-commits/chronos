---
name: Good First Issue / Contributor Task
about: Template for scoped community tasks and starter issues
title: 'feat/fix: '
labels: 'good first issue, help wanted'
assignees: ''
---

### Problem Statement & Context
A concise explanation of the problem or feature opportunity.

### Desired Implementation
- **Target Files**:
  - Implementation: `path/to/file.ts`
  - Tests: `path/to/test.ts`
- **Architectural Boundary**: (e.g. zero runtime deps in core, lazy imports, fail-closed)

### Acceptance Criteria
- [ ] Negative failure cases handled with clear error messages
- [ ] Positive/sealed success cases passing
- [ ] Determinism guard remains 100% green (`pnpm vitest run packages/core/test/determinism.test.ts`)
- [ ] TypeScript strict mode and ESLint pass without warnings

### Verification Commands
```bash
# Test the target feature
pnpm test <path/to/test>

# Full verification bar
pnpm typecheck && pnpm lint && pnpm test && pnpm build
```

### Interested in working on this?
Leave a comment below saying you'd like to take it! Maintainers review PRs promptly.

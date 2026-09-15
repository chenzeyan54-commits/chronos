## Description
A concise summary of the changes made in this PR and the problem it solves. Fixes #(issue).

## Type of Change
- [ ] `feat`: New feature or capability
- [ ] `fix`: Bug fix or determinism patch
- [ ] `docs`: Documentation updates or example recipes
- [ ] `test`: New tests, benchmarks, or scenario fixtures
- [ ] `refactor`: Code reorganization without functional changes

## Architectural Checklist (Strict DST Guardrails)
- [ ] **The Golden Rule**: Determinism is preserved. No real timers (`setTimeout`), real I/O, or unseeded entropy (`Math.random()`, `Date.now()`) added to simulated paths.
- [ ] **Core Boundaries**: Zero runtime dependencies added to `@sx4im/chronos-core`.
- [ ] **Deterministic Replay**: The determinism guard test passes (`pnpm vitest run packages/core/test/determinism.test.ts`).
- [ ] **Failure Capsule**: If fixing a bug, includes a regression test (and failure capsule fixture if applicable).

## Verification
Paste test results from running:
```bash
pnpm typecheck && pnpm lint && pnpm test && pnpm build
```

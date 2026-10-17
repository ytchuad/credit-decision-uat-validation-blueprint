# Copilot instructions — public design blueprint

- This repository contains **generic documentation only**. The real validation workbench is elsewhere in a private, authorised environment; this repo does not contain its code or actual policies.
- **Audit first, decide second, implement third.** Inspect current functionality/tests before recommending incremental improvement, targeted refactor or clean rebuild. Recommend whichever is warranted by evidence; no predetermined outcome.
- Preserve working features when practical, but do not keep unfixable design merely to avoid a rewrite. Compare functional coverage, testability, coupling, cost, risk, and migration plan.
- Prefer small, tested, reviewable increments once a strategy is chosen; avoid speculative abstractions.
- Target engine request/response logs are XML; requests may have absent, empty, nil, zero, invalid or present values. Historical legacy logs are JSON; legacy conversion and parity are deferred because target behavior intentionally differs.
- E2E and standalone execution workflows should reuse independent validation logic when technically appropriate.
- Factor out genuinely shared subpopulation/business calculations; maintain traceable rule and dependency evidence.
- Expected outcomes must come from approved rules or independently verified fixtures, never automatically from target actual responses.
- Use deterministic scenario generation from valid XML baselines and reviewed rules. Avoid unbounded Cartesian products.
- Prefer reviewer-friendly Excel plus structured results; Jupyter is optional analysis tooling, not required production UI.
- Audit and test actual outcomes; distinguish PASS, FAIL, NOT_VERIFIABLE, NOT_APPLICABLE, NOT_RUN and INVALID_TEST_SETUP.
- Do not publish any internal workbench code, real data, institution-specific business rules or schemas, identifiable customer information, credentials or confidential test output to this repository.

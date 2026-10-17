# Copilot Chat handoff — use inside the existing workbench

This GitHub repository is **public, high-level design guidance only**. The actual workbench already exists in an authorised private environment. Your role is to determine the best implementation strategy **after inspecting that existing code**.

Read `README.md`, `docs/05-existing-workbench-audit.md`, `docs/07-decisions.md`, and `.github/copilot-instructions.md` first.

## First action: read-only audit

Inspect actual files, entry points, parsers, XML mappings, scenario generation, shared classifications, validation logic, current report/UI, tests, dependency versions, usage workflows, and known pain points. Run existing tests only in the authorised environment using permitted data. Show observations with evidence; do not assume a file works based on its name.

## Make an evidence-based architecture decision

Compare three possibilities:
1. **Incremental improvement** of existing workbench.
2. **Targeted refactoring** of defective or duplicated areas while retaining working capabilities.
3. **Clean rebuild**, only if justified by fundamental architectural/correctness problems and acceptable migration costs.

Use explicit criteria: current functional coverage, correctness/bugs, testability, coupling, duplicated policy logic, data safety, maintenance burden, user workflow, regression risk, estimated effort, and rollout/rollback strategy. Existing working features and files are assets, not liabilities. Equally, do **not** preserve broken design merely to minimise changes.

Present a short decision matrix (option, advantages, risks, estimated scope, evidence), choose one with justification, and identify what would change your conclusion.

## Then propose a minimal demonstrable vertical slice

- E2E target XML request/response validation.
- Standalone scenario plan -> target request XML -> manual execution by UAT team -> response matching.
- Shared subpopulation logic used by independent modular assessment-type validator.
- Reviewable Excel report plus structured result records.
- Independently verified golden and deliberately wrong response tests.

**Do not edit or scaffold before reporting the audit and recommendation.** After approval under local workflow, implement one focused change, run tests, show actual observed results, and identify unresolved issues. If the user explicitly directs immediate implementation, still document the choice and minimise avoidable risk.

## Hard constraints

- Target request/response logs: XML; request elements may be absent, empty, nil, zero or invalid.
- Legacy logs: JSON; actual target outputs may intentionally differ. Legacy conversion/parity is out of initial scope.
- Standalone inputs are freely controllable, but validity/expected handling must be documented.
- Do not derive expected policy outputs from actual target response.
- Do not use unapproved confidential examples in this public repo.
- Avoid new GUI/database/microservices/generic rule platform unless demonstrated necessary.
- Never publish proprietary policies, source code, real logs, customer data, credentials or internal schemas.

**Your first answer should be the audit findings, recommendation (improve/refactor/rebuild) with trade-offs, and a small proposed plan — no code changes yet.**

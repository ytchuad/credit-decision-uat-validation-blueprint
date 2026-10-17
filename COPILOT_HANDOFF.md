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

Present a **brief** decision comparison, choose one option based on observed evidence, and identify the **smallest high-value next change**. Avoid lengthy architectural redesign proposals or large batches of changes.

## Then propose a minimal demonstrable vertical slice

- E2E target XML request/response validation.
- Standalone scenario plan -> target request XML -> manual execution by UAT team -> response matching.
- An observable component validator (e.g. assessment type); reuse shared subpopulation logic **only if that component requires it**. Subpopulation itself is not a PCO output to validate.
- Reviewable Excel report plus structured result records.
- Independently verified golden and deliberately wrong response tests.

**Do not edit or scaffold before reporting the audit and recommendation.** After approval under local workflow, implement one focused change, run tests, show actual observed results, and identify unresolved issues. If the user explicitly directs immediate implementation, still document the choice and minimise avoidable risk.

## Hard constraints

- Target request/response logs: XML; request elements may be absent, empty, nil, zero or invalid.
- Legacy logs: JSON; actual target outputs may intentionally differ. Legacy conversion/parity is out of initial scope.
- Standalone inputs are freely controllable, but validity/expected handling must be documented.
- Do not derive expected policy outputs from actual target response.
- Do not use unapproved confidential examples in this public repo.
- **PCO response XML does not contain subpopulation classification. Do not build a Subpopulation PCO Validator, compare an invented actual value, or add Subpopulation PASS/FAIL rows.** If a component depends on subpopulation, calculate it internally, show it optionally in the component's trace, and verify the helper with small independent unit tests.
- Avoid new GUI/database/microservices/generic rule platform unless demonstrated necessary. No extra layers, extensive dependency frameworks or new Excel tabs for subpopulation.
- Never publish proprietary policies, source code, real logs, customer data, credentials or internal schemas.

**Your first answer should be a concise audit, an evidence-based choice (improve/refactor/rebuild), and at most the next 1–3 focused changes — no code changes yet.** Do not turn this blueprint into a comprehensive rewrite checklist.

# Existing workbench audit and architecture choice

The workbench already exists and is reportedly not well designed. **Its actual structure and correctness have not yet been examined here.** Do not assume either that the existing code should be retained or that a rebuild is justified.

## Step 1 — Observe without modifying

1. Inventory actual project files, entry points, runtimes, dependencies, tests, execution scripts, UI/reporting, and data paths.
2. Trace an E2E request/response case through parsing, rule evaluation, comparison and reporting.
3. Trace standalone test definition, XML generation, handoff, response matching and validation.
4. Inspect existing shared logic (e.g. subpopulation) and duplicated logic across modules.
5. Check whether missing vs empty vs nil vs zero vs invalid values remain distinct.
6. Verify expected-result provenance: approved rules, fixtures, or incorrectly copied engine actuals?
7. Run available tests with approved inputs. Record exact observed successes and failures.
8. Assess confidentiality and which artifacts are allowed to be committed, shared or used in logs.

## Step 2 — Compare options, not preferences

| Criterion | Incremental fixes | Targeted refactor | Clean rebuild |
|---|---|---|---|
| Current working functionality retained | Usually high | Medium to high | Must be reimplemented |
| Changes / regression surface | Usually smallest | Localized | Potentially extensive |
| Removes fundamental coupling | Limited | Often possible | Highest flexibility |
| Delivery effort | Often low | Moderate | Usually highest |
| Best fit | Mostly sound architecture, isolated gaps | Solid features with problematic boundaries | Fundamentally unreliable/untestable implementation |

Do not choose by this generic table alone; substantiate with actual files, tests and dependencies.

For each candidate provide:
- Observed evidence and specific defects/limitations.
- Capabilities worth preserving or migrating.
- Estimated relative change scope and testing effort.
- Risk of business-rule drift, regression, loss of proven behaviors, and transition.
- Rollback or parallel verification plan.
- A recommendation with explicit justification and alternatives rejected.

A clean rebuild can be appropriate when fundamental assumptions cannot be corrected safely. In that case inventory features and reference tests before replacement, then run old/new side by side on **approved reference fixtures** (not assume old behavior is correct).

## Step 3 — Minimum first implementation

Choose a thin, usable, end-to-end slice that demonstrates:
- Parsing a valid target XML request and a corresponding response.
- One independently verified shared classification + assessment-type rule.
- Reviewing and generating a small deterministic scenario batch.
- Reconciling returned responses including missing and ambiguous matches.
- Reporting structured results and four Excel tabs.
- Golden, deliberately-wrong-response, negative-input and status-handling tests.

If those capabilities exist and work, avoid rebuilding them. Choose a different missing or defective slice.

## Copilot audit response template

| Existing path/component | Verified current behavior | Defect/gap | Evidence | Proposed action |
|---|---|---|---|---|
| [inspect locally] | [observed] | [fact] | [test/path] | KEEP / FIX / REFACTOR / REPLACE |

Then a concise option matrix, recommended path, first change set with filenames, tests and acceptance criteria. **Do not modify code until the local reviewer sees the recommendation**, unless separately instructed by the reviewer.

## Public/private boundary

All findings involving institution-specific source, XML, policy rules, screenshots, customer records or credentials stay in the authorised environment, not in this public design repository.

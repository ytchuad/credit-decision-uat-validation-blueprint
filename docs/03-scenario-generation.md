# Effective standalone scenario generation

## Goal

Generate a **small, defensible set of scenarios with clear test intent and expected handling**, not all theoretical variable combinations. Standalone testers can change arbitrary target XML input variables; no legacy JSON conversion is required for initial testing.

## Workflow

1. Inventory approved business rules: ID, effective version, applicability, variables, comparators, thresholds, precedence and expected outcomes.
2. Select one valid XML baseline (or an approved real target request within the private environment).
3. Generate a **scenario plan spreadsheet** for human review before XML generation.
4. Apply specific XML-aware mutation operations; preserve an unmodified original baseline.
5. Check expected XSD/interface validity. Mark intentional invalid cases as negative tests, not unexpected generator errors.
6. Emit immutable XML request per case plus manifest: Case ID, source baseline, hash, module, rule, test type, mutation, expected handling, execution status.
7. Team executes in target engine and returns XML responses.
8. Reconcile each response by Case ID or trustworthy mapping and run the same independent validator used in E2E.
9. Export results and coverage.

## Mutation operations

`SET_VALUE`, `REMOVE_ELEMENT`, `SET_EMPTY`, `SET_NIL`, `ADD_ELEMENT`, `SET_INVALID_VALUE`; `DUPLICATE_ELEMENT` only if interface behavior warrants testing.

Never treat missing as empty or numeric zero. Manipulate XML elements, namespaces and ordering using XML-aware code rather than brittle string replacements.

## Rule-driven test patterns

| Group | Scenario examples |
|---|---|
| Boundary | just below, exactly at, just above threshold, respecting policy precision |
| Missing | absent element, empty text, nil, zero where separately meaningful |
| Invalid | wrong type, invalid enum, negative value, out-of-range value where applicable |
| Logic | each significant decision branch and non-applicable case |
| Interactions | two rules active, overlapping subpopulation, cap/override/precedence, dependent fields |
| Advanced (optional) | constrained pairwise, approved metamorphic relationships, property-based tests |

Fictional demo: income threshold = 30,000; create 29,999 / 30,000 / 30,001 *only if integer-unit precision is correct*. This is not a real policy threshold.

**Keep invalid handling explicit**: Is a rejected request expected, an error response, a default, or an ordinary decision? Do not assert PASS based only on returning an XML response.

## Avoid explosion

Prioritise (1) one-variable-at-a-time from a frozen valid baseline, (2) known rule precedence and shared dependency interactions, (3) pairwise only for gaps. Do not generate full Cartesian products. If team execution is manual, start with approximately ten reviewed cases, then expand based on uncovered rules and defects.

Measure rule/branch/boundary/error-handling coverage, not raw testcase volume. De-duplicate semantically equivalent scenarios. Keep generated scenarios reproducible via baseline and manifest hashes.

## Oracle independence

Scenario definitions describe input changes and targeted rules. Approved reference specifications or independent calculators produce expected values. Never set expected equal to the actual response observed from the same run.

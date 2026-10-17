# Validation reporting, evidence and quality

## Primary deliverable: Excel

Use existing report capabilities if they are sound. First target: four worksheets.

| Worksheet | Essential information |
|---|---|
| Summary | run ID/time, engine and policy versions, case counts, assertion counts, status by module, important failures |
| Validation Details | case ID, module, rule ID, expected/actual, status, reason, input evidence, source file references, dependency trace |
| Scenario List | scenario purpose, baseline ID, mutations, execution state, response match, expected handling |
| Rule Coverage | rule/version, branches/thresholds, test types, case IDs, covered/not covered |

Add frozen headers, AutoFilter, suitable conditional formatting, and direct references to request/response XML paths. Keep raw logs in authorised private storage and do not paste whole XML into Excel cells. **No Subpopulation PASS/FAIL rows or separate Subpopulation worksheet:** the PCO response has no actual classification. Expected subpopulation may appear only as optional explanatory context for a related component.

**Count both cases and validation assertions explicitly**: one case may trigger multiple independent assertions; the two totals must not be confused. Retain JSON or CSV machine-readable results as a reproducible source for Excel. Jupyter may be used for debugging but is not the primary user interface.

## Status definitions

| Status | Meaning |
|---|---|
| PASS | applicable expected result agrees with actual |
| FAIL | independently established mismatch |
| NOT_VERIFIABLE | required rule/input/version or evidence unavailable, or response pairing ambiguous |
| NOT_APPLICABLE | rule does not apply |
| NOT_RUN | no corresponding confirmed engine response |
| INVALID_TEST_SETUP | conflicting or unintentionally malformed scenario setup |

Missing data or unknown prerequisite must not become PASS. If a target request is intentionally malformed, compare to the **documented expected error handling**, not a normal decision.

## Independent correctness checks

- Golden cases with expected outcomes manually confirmed from approved rules. Where needed, unit-test the shared subpopulation calculation separately from PCO UAT assertion results.
- Known-bad cases created by deliberately changing response fields must FAIL.
- Parser covers absent/empty/nil/zero/invalid with correct distinction.
- Scenario generator changes only intended fields; baseline immutable.
- Missing/ambiguous response statuses work.
- Rule dependency failures preserve root-cause trace and do not imply downstream passes.
- Excel counts equal raw structured records; open workbook and inspect representative rows.
- Repeated runs with same inputs/config/versions produce same semantic results.
- Versioned policy, engine release and test tool version recorded in private execution records.

## Usability principle

Prefer a simple command line / approved launcher plus Excel over an unnecessary dashboard. If a current local UI is already useful and maintainable, do **not** remove it merely to follow this document.

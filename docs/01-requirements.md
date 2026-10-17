# Requirements and scope

## E2E UAT

- Consume target-engine XML request/response log pairs from actual UAT execution.
- Apply independent business-rule validators.
- Test input interpretation, output decisions and rule consequences when needed source facts are present.
- Do not claim upstream data mapping was independently verified if only the engine-boundary XML was examined.

## Standalone UAT

- Define controlled scenarios against a valid target XML baseline or approved target UAT request.
- Testers can alter any input variable, omit elements, set nil/empty values, and deliberately submit invalid values.
- Produce reviewable plans, generated XML requests and a manifest with stable Case IDs.
- A separate UAT team executes these requests in the target engine and returns response XML.
- Match response to request with a trustworthy Case ID / execution reference or auditable manifest. **Never match by file order alone.**
- No returned response: `NOT_RUN`; ambiguous matching: `NOT_VERIFIABLE`.

## Business validation

**UAT validation targets are observable component outputs**: assessment type, document requirements, scorecard selection/calculation, SMV, policy caps, final limits and other proven needs. Shared business functions may include subpopulation classification and derived variables **only where component validators need them**.

Expected results come from approved, independent policy requirements and source inputs. **The PCO response XML does not contain subpopulation classification.** Therefore do not create a separate subpopulation PCO validation target or PASS/FAIL assertion. Verify shared subpopulation calculation by local unit tests against independently checked rules; it can be shown as supporting context for component failures. Cross-response consistency is a separate validation category.

## Migration context

- Legacy engine logs: JSON; target engine logs: XML; both requests and responses can differ in schema and meaning.
- Some logic intentionally changed and more calculations moved into the target engine from upstream sources.
- Legacy actual results are not the automatic expected result for the target.
- Historical conversion requires mapping, provenance, and often unavailable input reconstruction; **defer** it.
- If later added, classify rules as unchanged, modified, new or retired before semantic parity checks.

## Non-goals by default

- Full recreation of the target engine, proprietary model validation, automatic target execution or production deployment.
- Broad legacy replay/parity in initial release.
- A mandated new web app, database, orchestration framework, generic rules platform, or standalone subpopulation validator.
- A prescribed rewrite: the existing workbench must be examined first.

## Acceptance principles

Correctness, explainable evidence, repeatability, readable reports, minimal maintenance burden, and independent test fixtures outweigh the number of generated scenarios or lines of code.

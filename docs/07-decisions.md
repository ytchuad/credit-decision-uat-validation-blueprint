# Decision log

Design discussion updated 2026-10-17. These are **generic constraints and provisional choices**, not claims about the actual private workbench.

| ID | Decision / observation | Status |
|---|---|---|
| D-001 | E2E and standalone should share independent validation logic where sensible. | Agreed design goal |
| D-002 | Target request and response logs are XML; requests differ by case and can omit fields. | Confirmed |
| D-003 | Legacy logs are JSON; conversion of historical legacy data to target XML is deferred. | Confirmed / deferred |
| D-004 | Target outputs can intentionally differ from legacy due to changed policy and upstream/engine calculation boundaries. | Confirmed |
| D-005 | Subpopulation and other reused business functions should be modular **when actually reused**; no separate Subpopulation PCO UAT Validator because classification is absent from response XML. Verify helper logic with independent unit tests. | Confirmed |
| D-006 | Validators should be independently maintainable (assessment, documents, scorecard/SMV, caps/limits). | Agreed |
| D-007 | Expected outcomes must have approved, independent rule provenance rather than copying actual engine outputs. | Required |
| D-008 | Standalone scenario requests can set any target input variables; a separate team executes them. | Confirmed |
| D-009 | Start scenario coverage with targeted, reviewed deterministic boundaries, missing/invalid and rule interactions. | Proposed |
| D-010 | Scenario generation and expected-result validation should be distinct responsibilities. | Proposed |
| D-011 | Excel is the preferred primary reviewer output, with structured machine-readable evidence. | Preferred |
| D-012 | Jupyter/dashboard are not required initial UI components. | Preferred |
| D-013 | **Existing workbench exists but architecture choice is open:** Copilot must audit it and decide whether to improve, refactor or rebuild based on evidence and trade-offs. | Updated per owner |
| D-014 | Public repo contains generic design and fictional examples only, no proprietary implementation. | Required |
| D-015 | Specific folder structure, Python modules and phased milestones are suggestions, not instructions to replace working facilities. | Clarified |
| D-016 | UAT PASS/FAIL applies to **observable component results**; expected subpopulation is optional explanatory context, not an observable PCO actual. | Confirmed |
| D-017 | Avoid overengineering: no separate subpopulation reporting, extra frameworks or large speculative change lists. Prefer the simplest evidenced next improvement. | Confirmed |

## Deferred

- Historical legacy JSON conversion and semantic equivalence mapping.
- Legacy/target parity restricted to independently established unchanged rules.
- Full target-engine source recreation, unnecessary dashboard or database, broad randomized testing.

## Open questions to resolve privately from real code

- What components already work, have tests, and deserve retention?
- Which versioned policy/specification is the authoritative oracle?
- How are responses reliably matched to requests today?
- Which rule dependencies are real and which are hypothetical?
- What external/enriched inputs are needed by validators?
- What is an appropriate architecture choice after benchmarking the workbench?

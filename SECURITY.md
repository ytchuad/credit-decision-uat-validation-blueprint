# Security and public-repository boundary

This repository is publicly readable. It contains **general design notes only**. It is not an approved location for enterprise credit decision workbench code or tests.

## Never upload

- Actual customer data, identifiers, PII, exposures, transaction data, or customer-derived examples.
- Real request/response XML or legacy JSON logs, screenshots, defect reports or test results.
- Proprietary policy thresholds, rule matrices, scorecard/SMV parameters, business classifications, non-public schemas, internal architecture or business documentation.
- Internal implementation source code, API/endpoint details, credentials, tokens, certificates or connection strings.

Use fictional examples. Obtain internal approval before sharing company-related information externally. Keep workbench, rules, live test data and outputs within bank-authorised systems. A publicly readable GitHub repository does **not** make the upload of internal data permissible.

## Safe practices

- Maintain a separate private working directory/repository for internal code and data.
- Review staged diffs and run secret/data scanning before any public commit.
- Keep generated XML/JSON/Excel artifacts outside this public repository.
- Disable external entity expansion and network access in XML parsing.
- Mask identifiers in reports as required by institutional policy.
- Track engine/policy/tool version in private run evidence.

Removing an accidentally published file in a later Git commit does not erase it from prior Git history. Follow incident/security procedures if a disclosure occurs.

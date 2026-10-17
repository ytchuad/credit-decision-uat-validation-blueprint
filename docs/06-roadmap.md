# Incremental delivery roadmap (subject to workbench audit)

**This roadmap is illustrative, not a mandated redesign or implementation sequence.** Copilot should assess the existing workbench first, choose improve/refactor/rebuild from evidence, then make the smallest justified change. Do not implement every stage or new layer automatically.

## Stage 0 — Existing-workbench audit and architecture decision

Output: verified current-state inventory, existing tests/results, gaps/defects, three-option comparison (improve, targeted refactor, rebuild), recommended approach, migration/regression risks, exact proposed edit scope.

No code changes until initial audit/recommendation is reviewed in the local work workflow.

## Stage 1 — Working validation vertical slice

Demonstrate a representative target XML request/response pair parsed correctly, independent assessment-type validation, case/response reconciliation and structured result records. **Use an independently unit-tested shared subpopulation calculation only if needed** for that component; PCO does not return actual subpopulation, so do not add a standalone UAT validator. Prefer existing working functions.

Acceptance: independently verified known-good passes; deliberate wrong response fails; missing prerequisites are explicitly not verifiable; absent response is not run; traces identify rules, inputs, engine/policy versions and files.

## Stage 2 — Controlled standalone scenario generation

Produce reviewable Excel scenario matrix, valid baseline XML mutations, boundary/missing/invalid scenarios and immutable case manifest. Requests executed by the separate UAT team; responses reconciled and validated by the common engine.

Acceptance: small approved batch (around ten initially), original baseline intact, each mutation verified, no fabricated engine execution, identifiable outcomes.

## Stage 3 — Extend validators as needed

Document requirements, scorecard selection, score calculation only with complete model specifications, SMV, caps and limits — independently one at a time with reliable fixture coverage. Shared classifications and reusable computations should remain consistent.

## Stage 4 — Reporting and regression quality

Reviewer-friendly Excel and structured results, as much rule coverage and trace detail as demonstrably useful, consistent case-versus-assertion statistics and regression checks. **Reuse existing report tabs if sufficient; do not create Subpopulation PASS/FAIL entries or worksheets.**

## Deferred

Historical legacy JSON conversion to target XML; parity across semantically unchanged legacy/target rules; broad fuzzing, database, mandatory notebook, new dashboard, automated target execution.

## Done means

- User can repeat necessary workflows without hand-editing program source.
- Testcase purpose, expected handling and evidence are visible.
- Expected values have independent policy provenance.
- Test failures expose the actual discrepancies rather than silent PASS.
- Implementation trade-offs are documented and the chosen approach has passing regression tests.
- No confidential implementation data has entered this public repository.

# Reproduce the checks

These fixtures describe historical observations; they are not automated tests and were not rerun during packaging.

1. Recreate and reconnect the two agents and workflow using README.md. Freeze settings and record any differences.
2. Start a fresh conversation/run for each E2E fixture in test-cases.json; submit its question to Trigger.chatInput.
3. Capture the resolved trigger input, both completed node inputs/outputs, run identifier, effective model/settings and full retrieved passages with page metadata where the platform exposes them. Verify the reviewer receives actual question and draft, not unresolved expressions.
4. For FI1 only, use the reviewer playground with both `Original question:` and `Draft answer:` fields populated from the fixture. This bypasses the drafter and is not an end-to-end success. A question-only run cannot test false-draft correction.
5. Judge handoff, substantive accuracy, exact citation support, ambiguity/boundary handling and status consistency separately. Pass means the criterion is met; Partial means mixed performance; Fail means the required behavior is absent/wrong; Unverified means evidence is unavailable. Do not aggregate these four selected cases into a proven accuracy rate.
6. Compare draft and review claim by claim against the manuals. Check the freeze restriction at printed 6-3 and receipt-source procedure at printed 6-29; do not substitute section-opening pages. Verify other citations separately.
7. Save new observations separately from historical evidence. Before sharing exports, remove personal metadata, account identifiers and credentials.

Evidence consists of the recorded summaries of user-supplied outputs and supplied configuration. Raw execution/retrieval logs are not bundled. No independent retrieval behavior or effective model precedence was established. Improve citation verification, targeted clarification and status decisions, then use a broader fixed test set before making quality claims.

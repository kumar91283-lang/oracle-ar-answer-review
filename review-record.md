# Oracle Receivables Answer Review Workflow

## Current implementation

User reports SuperFlow sequence Trigger -> AI Agent using Oracle AR Guide -> reviewer node using saved agent Oracle AR Doc Auditor -> Output. Both agents use the existing two-guide Oracle Receivables knowledge base. Reviewer query explicitly includes serialized Trigger output and preceding node input. SuperFlow provides sequential orchestration; no separate autonomous coordinator agent has been demonstrated.

## Development observations

1. Initial end-to-end approval-limits question: reviewer returned status, findings, final answer, and sources. User supplied reviewer output. Review response had a numbering defect and added Primary approver content without citing printed page 4-3. Successful routing is user-reported; full run trace not captured.
2. Initial false-draft review: output corrected frozen-rule-set behavior but labelled it Supported and cited 6-2. Exact submitted input not independently captured, so attribution to prompt failure is uncertain.
3. Reviewer instructions revised to explicitly judge the original draft, require Revised for supported substantive corrections, and identify contradictions. Citation verification was strengthened without hardcoding a test page; output headings made unnumbered.
4. A subsequent Supported output was initially interpreted as a failed retest. User then clarified that only the question had been submitted. This was not a valid false-draft review test. It also failed the reviewer instruction to request a missing draft. Do not count it as evidence that the revised status rule failed with complete input.
5. Latest complete-input review: reviewer marked Revised, identified the draft's false permission to modify/delete frozen rule sets, and produced the correct prohibition. Correction and contradiction detection pass for this development case. Citation accuracy remains partial: output cites 6-1 to 6-2, but freezing validation and update/delete restriction appear on printed 6-3 of Implementation Guide E48902-05. No raw retrieval trace available. Input association is based on the interactive test sequence, not a captured request log.

## End to end test 1 frozen application rule set

Question: Can I edit or delete an application rule set after freezing it?

Captured first-agent output: completed; correctly answered that a frozen rule set cannot be updated or deleted, cited Implementation Guide printed 6-2.

Captured reviewer output: completed; explicitly assessed the draft, marked Supported, repeated the correct prohibition and cited 6-2. Stated no material correction was needed.

Assessment: Draft-to-reviewer handoff demonstrated by the supplied node outputs. Core answer correctness passes for both stages. Citation accuracy is partial for both: actual rule is on printed 6-3. Review did not improve the citation and its Supported status incorrectly certifies the source page. Independent evidence retrieval cannot be verified from the final node output. Possible inherited citation or chunk/page metadata issue remains a hypothesis, not an established cause. No measured overall improvement may be claimed from this single end-to-end example.

## End to end test 2 ambiguous source setup

Question: How do I set up a source in Receivables?

Captured draft: completed; explicitly identified transaction versus receipt sources and gave conditional receipt steps plus a transaction-source overview. Cited receipt steps at 6-28 and transaction sources 4-28 to 4-31. Better ambiguity acknowledgment than the original project-one Q4, but no targeted clarification question before substantive steps. This is a new run, not a replacement for the original evaluation.

Captured reviewer: completed; marked Revised, acknowledged incomplete/partially unverified citations, and returned conditional receipt steps and a transaction-source summary. Retained receipt-step citation 6-28 although the actual procedure is on 6-29. Retained transaction-source span while labelling it partially unverified. Did not request a choice of source type.

Assessment: Handoff and review format pass. Review quality is Partial: recognizes evidence limitations but does not resolve the verified receipt-page defect. Ambiguity handling is Partial: alternatives are acknowledged, but the configured Needs clarification behavior was not followed. The finding that the draft failed to distinguish the source types is overstated because it already identified both explicitly. Revised status is not evidence of an actual material correction; no confirmed substantive improvement demonstrated. No raw retrieval trace supplied, and detailed transaction-source claims have not been exhaustively checked.

## Next validation

Run an unsupported company-specific question through SuperFlow: What receipt write-off limit has our company configured in production, and who approved it? Capture both stages. Expected behavior is to acknowledge absent company evidence, avoid invented facts, and preserve that boundary through review. Keep independent fault-injection tests separate from normal end-to-end runs.

## Sources and scope

Implementation Guide: https://docs.oracle.com/cd/E79783_01/current/acrobat/122arig.pdf
Reference Guide: https://docs.oracle.com/cd/E79783_01/current/acrobat/122arrg.pdf

This is a custom second course project extending a previously submitted Q&A assistant. It is not yet packaged or submitted. Do not claim the review guarantees factual or citation correctness or that overall quality improvement has been measured.

## End to end test 3 unknown production configuration

Question: What receipt write-off limit has our company configured in production, and who approved it?

Evidence provenance: user supplied both completed node outputs. This entry summarizes those observations; it is not a raw execution log or an additional rerun.

Draft: correctly declined to invent company-specific values or approvers. Gave generic system-options and approval-limits guidance and recommended checking production with an administrator and internal approval records. Cited Miscellaneous System Options 2-34 to 2-35 and Approval Limits 4-1 to 4-2.

Reviewer: Needs clarification. Preserved the refusal and absence of production evidence. Narrowed guidance to approval limits by currency and lower/upper amounts, directing the administrator to live records. Cited Approval Limits 4-1 to 4-2.

Assessment: boundary handling Pass; overall Partial. The question is clear, so Needs clarification does not match the configured criteria. If material draft guidance cannot be checked, Insufficient evidence is appropriate; Supported is not mandatory without checking all material claims and citations. The reviewer incorrectly treats generic navigation as needing a company record: documentation can support generic guidance separately from actual production values and approval history. Exact navigation and cited pages in this case were not independently checked. No proven reliability gain follows from preserving an already-correct refusal.

## Packaging and evidence status

Project2 now has a separate sanitized configuration package, evaluation report and short demo script. Nothing has been published or submitted and no Project2 video exists. The earlier Next validation section records the planned test; test 3 above completes that observation. The earlier not-yet-packaged statement is historical.

Evaluation scope: three end-to-end cases and one valid reviewer-only deliberate false-draft test, plus development observations. Earlier question-only runs are invalid fault injection and are not independent successes. Only outputs and workflow configuration are available; independent retrieval traces, runtime model precedence, one-click import and broad quality gains remain unverified.

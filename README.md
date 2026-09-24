# Oracle Receivables Answer Review

Project2 is a custom sequential multiagent documentation-review prototype in Lyzr SuperFlow. It extends the previously submitted Oracle AR Guide with Oracle AR Doc Auditor. It is not a GTM system. The workflow is:

`Trigger → AI Agent (Oracle AR Guide) → Oracle AR answer reviewer (Oracle AR Doc Auditor) → Output`

SuperFlow provides orchestration. There is no independent coordinator agent, hybrid routing or human-escalation integration. Referring a user to an administrator in an answer does not execute an escalation.

## Package contents

- `agents/`: two sanitized saved-agent templates and their exact instructions.
- `workflow.template.json`: reconstructed workflow with original node settings and stable local node IDs.
- `source-documents.md`: the two official Oracle PDF links and versions.
- `evidence/`: historical evaluation record, four fixtures and reproduction criteria.

The Word report, demo script and any future recording are separate submission artifacts. No video exists yet for Project2. This package contains configuration, not an executable standalone service, deployed app or verified one-click importer.

## Setup in your account

1. Use a Lyzr account with agent, knowledge-base and SuperFlow access and an OpenAI model connection. No keys are supplied. Usage can consume account credits.
2. Download both PDFs in source-documents.md. Create a Basic knowledge base; the original setup used Qdrant [Lyzr], text-embedding-3-small, Semantic Model off, displayed default parser and OCR off. Allow all pages and confirm both documents are searchable. Chunk size, overlap and full indexing coverage were not independently recorded/audited; record your actual settings.
3. Create/save Oracle AR Guide and Oracle AR Doc Auditor. Copy each template's role, goal and instructions. Attach the same two-guide knowledge base to both. Saved-agent settings are OpenAI gpt-5.4-mini, temperature 0.7, top_p 0.9, text output, max_iterations 25, Basic retrieval top_k 10 and score_threshold 0, Cognis memory cross_session false and store_messages true. Record any unavailable settings or model substitutions.
4. Map YOUR_KNOWLEDGE_BASE_ID and YOUR_MODEL_CREDENTIAL_ID to your own resources if using JSON. The templates omit export IDs, owner/access metadata, timestamps and version. They are not validated import payloads; use manual reconstruction unless your platform supports and validates this schema.
5. Build the four named nodes shown in workflow.template.json and connect them in the sequence above. Trigger defines required multiline string chatInput. Select the saved Guide in AI Agent and the saved Auditor in Oracle AR answer reviewer; replace YOUR_GUIDE_AGENT_ID and YOUR_REVIEWER_AGENT_ID. Output uses outputField output. The local node IDs are structural labels, not account agent IDs.
6. Copy the reviewer's prompt expression exactly from workflow.template.json. It serializes the Trigger JSON as the original question and the preceding node JSON as the draft. Keep the node name Trigger unchanged, or deliberately update its expression reference. Confirm a trial run resolves both values and the output displays the reviewed answer.
7. The exported workflow nodes specify gpt-4o, temperature 0.7, maxTokens 4096, maxIterations 25 and systemPrompt "You are a helpful assistant." These differ from saved-agent model gpt-5.4-mini. The package preserves this distinction; runtime precedence was not verified. Check effective runtime behavior before claiming identical reproduction.
8. Run evidence/test-cases.json using evidence/reproduction.md. Capture complete inputs/outputs and retrieval traces where available. Keep new test results separate from historical observations.

## What the evidence shows

Three end-to-end cases and one valid reviewer-only fault-injection case form a small development sample. The reviewer corrected the intentionally false freeze answer, with a remaining citation defect. In normal end-to-end runs it missed known citation errors, did not ask a targeted question for ambiguous source setup, and misclassified a clear production-information question while correctly preserving the refusal to invent company facts. No general reliability improvement or numeric confidence is established. Independent retrieval traces are absent.

## Submission

Upload this package's contents to a repository only when ready, and submit the separate Word report and recorded short demo as required by your course. Confirm acceptance of the custom project and exact course submission requirements; this package does not establish rubric completion. Nothing has been uploaded or published by the packaging process. Project1 deliverables remain unchanged.

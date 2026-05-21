# Prompt Log — Farida Shehu

**Project:** Emergency Response Coordinator System  
**Team:** --  
**My Component:** Task Assignment & Tracking  
**AI Tools Used:** GitHub Copilot, ChatGPT

---

# Entry 1 — Capstone Checkpoint 2 Audit

**Date:** 2026-05-20

## Context
I was preparing for Checkpoint 2 of our capstone project. My team is building an Emergency Response Coordinator System using Airtable, n8n, Flowise, and AI classification workflows. I needed to evaluate what parts of the pipeline were working, what gaps still existed, and whether our workflows could successfully pass data between components.

## Prompt

The capstone audit (part 2.3)

## Result
Copilot interviewed me with questions about the Airtable schema, workflow handoffs, field mismatches, test records, and current project status. It then generated a Checkpoint 2 readiness assessment with sections for working components, critical gaps, schema issues, recommended fixes, and testing concerns.

## Evaluation
The audit was useful because it helped identify real integration issues, especially field-name inconsistencies between Airtable tables and n8n workflows. It also helped organize which parts of the system were fully tested versus partially working. However, some recommendations became overly complex, such as suggesting a full Airtable schema migration, which was unnecessary for the current scope of the project. And since the workflow was already tested and working, changing field names before submission could break the integration.

## What I Changed
After the audit, I reviewed the Airtable and n8n field mappings more carefully and confirmed that some field names were inconsistent across tables. I adjusted workflow mappings where necessary, cleaned duplicate task records created during testing, added `Step_Order` values for better task organization, and improved the Airtable task views and filters for tracking tasks more clearly.

## What I Learned
I learned that AI-generated audits can help identify integration gaps much faster than manually reviewing the entire system. I also learned that AI suggestions should still be evaluated carefully because some recommendations may be technically correct but too advanced or risky for the project’s current stage.

---

# Entry 2 — Debugging Airtable and n8n Workflow

**Date:** 2026-05-20

## Context
I was working on the Task Assignment & Tracking component of the Emergency Response Coordinator System. I was connecting Airtable tables with n8n workflows to automatically generate emergency response tasks from protocol steps.

## Prompt

> Help me debug my Airtable and n8n workflow. The workflow is generating duplicate tasks and some fields like Assigned role and priority are showing as undefined.

## Result
The AI explained that the issue came from mismatched Airtable field names and repeated execution of the “Find Protocol Steps” node. It suggested checking field mappings, using the exact Airtable field names, adding proper `Step_Order` values, and enabling “Execute Once” for the search node.

## Evaluation
The suggestions were mostly accurate and helped fix several workflow issues. The workflow successfully began generating tasks with assigned roles, priorities, due times, and statuses. However, some suggestions became more complicated than necessary for the checkpoint requirements.

## What I Changed
I updated several Airtable field mappings in n8n, added `Step_Order` values to protocol steps, cleaned duplicate task records, and reorganized the Airtable task views for better readability.

## What I Learned
I learned that small Airtable naming inconsistencies can break workflow automation very easily. I also learned the importance of testing workflows step-by-step instead of trying to debug the entire pipeline at once.

---

# Entry 3 — Organizing Airtable Kanban Views

**Date:** 2026-05-20

## Context
After generating tasks successfully, the Airtable Kanban board became cluttered with empty records and duplicate testing data, making it difficult to track active emergency tasks.

## Prompt

> How can I organize my Airtable task views so only active emergency tasks appear?

## Result
The AI suggested creating filtered Airtable views using `Incident_Id` and `Status` filters, sorting tasks by `Step_Order`, and customizing Kanban cards to display task names, assigned roles, priorities, and statuses.

## Evaluation
The suggestions improved the readability of the dashboard and made the workflow easier to demonstrate during testing.

## What I Changed
I created an “Active Tasks” view, added filters for active records, sorted tasks using `Step_Order`, and customized the Kanban cards to display more useful task information.

## What I Learned
I learned that dashboard organization is important for usability, especially when workflows generate many records during testing.

---

# Entry 4 — Testing Workflow Handoffs

**Date:** 2026-05-20

## Context
I needed to verify that incidents created by the AI classifier workflow could successfully trigger the task assignment workflow without manual data entry.

## Prompt

> How do I test whether my AI Core workflow is successfully handing off records to my Specialist workflow?

## Result
The AI explained how to trace records across the Airtable tables and verify that a classified incident with a valid `protocol_id` was successfully creating tasks in the `Tasks` table.

## Evaluation
The explanation helped confirm that the end-to-end workflow pipeline was functioning correctly for multiple emergency protocols.

## What I Changed
I tested multiple incident records including fire, lockdown, and medical emergencies to confirm that the correct protocol steps and tasks were generated automatically.

## What I Learned
I learned how important status fields and protocol IDs are for connecting workflows together in an automation pipeline.

---

# Entry 5 — Flowise API Limit Error

**Date:** 2026-05-20

## Context
While testing the incident classification workflow repeatedly, I encountered an error in the Flowise HTTP request node.

## Prompt

> Why am I getting a “predictions limit exceeded” error in my Flowise HTTP request node?

## Result
The AI explained that the error was likely related to Flowise usage limits, such as prediction quotas or API rate limits.

## Evaluation
The explanation helped identify that the issue was not caused by Airtable or n8n workflow logic, but by the external AI service configuration.

## What I Changed
I documented the issue for the team and informed the Flowise team member so the account limits could be checked before the final demo.

## What I Learned
I learned that external APIs can become failure points even when the internal workflow logic is working correctly, so it is important to test integrations early.

---

## Entry 6 — Error Handling Workflow

**Goal:**  
Add basic error handling to the Task Assignment workflow in n8n.

**Prompt Used:**  
"How can I add an IF node in n8n to detect workflow failures and log them into Airtable?"

**AI Response Summary:**  
The AI explained how to create an IF node after the task creation step and configure a branch that routes failed tasks into an Airtable error logging node using `status = error` and `error_reason`.

**What I Changed:**  
I added an IF node after the `Create Emergency Tasks` node and created a separate error-handling branch for failed workflow actions.

**Result:**  
The workflow structure now includes a visible error-handling path for monitoring failed task processing.

---

## Entry 7 — Priority Routing Logic

**Goal:**  
Add routing logic based on task priority.

**Prompt Used:**  
"How can I use IF nodes in n8n to separate high-priority emergency tasks from standard tasks?"

**AI Response Summary:**  
The AI suggested using an IF node to check whether `priority = 1` and create separate workflow branches for high-priority and lower-priority task handling.

**What I Changed:**  
I added a Priority Routing IF node connected to a duplicate workflow branch for demonstration purposes.

**Result:**  
The workflow now demonstrates how emergency tasks could be separated based on urgency levels.

---

## Entry 8 — Airtable Dashboard Views

**Goal:**  
Create dashboard views in Airtable for workflow monitoring.

**Prompt Used:**  
"How can I organize Airtable views to monitor task progress and workflow errors?"

**AI Response Summary:**  
The AI recommended creating grouped views filtered by task status and separate error-monitoring views for failed records.

**What I Changed:**  
I created the `Pipeline Status` view grouped by `status` and the `Error Monitor` view filtered to only show error records.

**Result:**  
The Airtable dashboard now provides clearer workflow visibility for monitoring and troubleshooting.

---

## Entry 9 — API Error Troubleshooting

**Goal:**  
Diagnose Airtable API connection failures in n8n.

**Prompt Used:**  
"Why am I getting PUBLIC_API_BILLING_LIMIT_EXCEEDED errors in my Airtable nodes?"

**AI Response Summary:**  
The AI explained that the issue was likely related to Airtable API usage limits or workspace billing restrictions and suggested using a new Airtable token or duplicating the base into another workspace.

**What I Changed:**  
I tested a duplicated Airtable base and updated workflow credentials to troubleshoot the API limitation.

**Result:**  
The issue was narrowed down to Airtable API access limitations rather than workflow logic errors.

---

## Entry 10 — Protocol Step Organization

**Goal:**  

Improve the organization and readability of generated emergency response tasks.

**Prompt Used:**  

"How can I organize emergency protocol tasks in Airtable so they appear in the correct order during workflow execution?"

**AI Response Summary:**  

The AI recommended adding a `Step_Order` field to the `Protocol Steps` table and sorting Airtable task views using ascending step order values.

**What I Changed:**  

I added `Step_Order` values to emergency protocol steps and updated Airtable sorting settings.

**Result:**  

Generated emergency response tasks now appear in the correct execution sequence during workflow testing.

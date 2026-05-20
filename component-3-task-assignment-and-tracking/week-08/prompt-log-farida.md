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

> I need you to act as a capstone project advisor for a university AI integration course. I'm going to describe my group project, and I need you to interview me about its current state, then produce a structured gap analysis.

## Result
Copilot interviewed me with questions about the Airtable schema, workflow handoffs, field mismatches, test records, and current project status. It then generated a Checkpoint 2 readiness assessment with sections for working components, critical gaps, schema issues, recommended fixes, and testing concerns.

## Evaluation
The audit was useful because it helped identify real integration issues, especially field-name inconsistencies between Airtable tables and n8n workflows. It also helped organize which parts of the system were fully tested versus partially working. However, some recommendations became overly complex, such as suggesting a full Airtable schema migration, which was unnecessary for the current scope of the project.

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

> How can I organize my Airtable task views so only active emergency tasks appear in the Kanban board?

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

# Week 10 Lab 

## Part 1 — Error Handling
An error-handling branch was added to the Task Assignment workflow using IF nodes in n8n. If task processing fails, the workflow routes the record to an error path and logs the issue using status = "error" and an error_reason field in Airtable. This prevents workflow failures from being silently ignored and improves monitoring visibility. 

![Error Handling IF Node](component-3-task-assignment-and-tracking/Week-10/error-handling-if-node-screenshot.PNG)


---

## Part 2 — Routing Logic
An IF routing node was added to the workflow to demonstrate how tasks can be routed differently based on priority level. Priority level 1 was used as the threshold for identifying high-priority emergency tasks. 

[screenshot]


---

## Part 3 — Dashboard Views

### Pipeline Status View
The pipeline status view provides emergency coordinators with a detailed overview of tasks and their current workflow states for monitoring and coordination purposes. 

[screenshot]


### Error Monitor View
The error monitor view is used by administrators to track failed workflow actions and identify tasks that require troubleshooting or manual intervention. 

[screenshot]


---

## Part 4 — Prompt Log (more entries)

Prompt log updated with additional entries documenting:

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

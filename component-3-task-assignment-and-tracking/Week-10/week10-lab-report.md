# Week 10 Lab 

## Part 1 — Error Handling
An error-handling branch was added to the Task Assignment workflow using IF nodes in n8n. If task processing fails, the workflow routes the record to an error path and logs the issue using status = "error" and an error_reason field in Airtable. This prevents workflow failures from being silently ignored and improves monitoring visibility. 

[screenshot]


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

- error handling implementation

- routing logic

- dashboard monitoring

- API troubleshooting

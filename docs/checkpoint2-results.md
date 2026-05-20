# Checkpoint 2 Results

**Date:** 2026-05-20  
**Team:** --

---

# Test Record

**Test Incident:**  

"Burning smell reported throughout the entire east wing."

**Expected Path:**  

Incident_Reports → AI Incident Classifier → Incidents → Task Assignment Workflow → Tasks Table → Kanban Dashboard

**Expected Final State:**  

The incident should be classified as a fire emergency, assigned the appropriate fire protocol, and automatically generate emergency response tasks with assigned roles, priorities, due times, and statuses visible in the dashboard.

---

# End-to-End Status: PARTIAL

The workflow pipeline was successfully tested previously from ingestion through dashboard visualization. However, during final integration testing, Airtable/n8n began returning `PUBLIC_API_BILLING_LIMIT_EXCEEDED` errors, preventing additional live executions.

Existing successful workflow runs were used to document the pipeline stages and confirm that the integration logic functions correctly.

---

# Component-by-Component Results

## Ingestion

- **Status:** Working
- **What happened:**  
A new incident report was successfully added to the `Incident_Reports` table with `status = new`.

- **Screenshot:**  
![Reports Stage](component-3-task-assignment-and-tracking/screenshots/reports-stage.png.PNG)

---

## AI Core

- **Status:** Partially Working
- **What happened:**  
The AI classification workflow previously classified incidents successfully by assigning:
  - `protocol_id`
  - severity
  - confidence
  - status = classified

During final testing, the workflow was temporarily blocked by `PUBLIC_API_BILLING_LIMIT_EXCEEDED` errors related to Airtable/API limits.

- **Screenshot:**  
![AI Core Stage](component-3-task-assignment-and-tracking/screenshots/ai-core-stage.png.PNG)

---

## Specialist

- **Status:** Working
- **What happened:**  
The Task Assignment & Tracking workflow successfully generated emergency response tasks using protocol steps from Airtable. Tasks included:
  - assigned roles
  - priorities
  - due times
  - step ordering
  - statuses

- **Screenshot:**  
![Tasks Stage](component-3-task-assignment-and-tracking/screenshots/tasks-stage.png.PNG)

---

## Integration Dashboard

- **Status:** Working
- **What happened:**  
Generated tasks appeared correctly in Airtable views and Kanban dashboards. Tasks could be tracked through:
  - Pending
  - In Progress
  - Completed
  - Overdue

Task progression is currently updated manually through Airtable Kanban views.

- **Screenshot:**  
![Dashboard Stage](component-3-task-assignment-and-tracking/screenshots/dashboard-stage.png.PNG)

---

# Gaps Found

- Airtable/API request limit errors temporarily blocked workflow execution during final testing.
  - Owner: AI Core / Integration

- Field naming inconsistencies still exist across Airtable tables:
  - `Protocol ID`
  - `Protocol_Id`
  - `protocol_id`

  - Owner: Ingestion + Specialist

- Duplicate task generation can occur if workflows are repeatedly executed on the same incident.
  - Owner: Specialist

- Workflow execution is currently triggered manually during testing rather than fully automated.
  - Owner: Ingestion + AI Core

---

# Fix Plan

1. Investigate and resolve Airtable/API request limit issue before final demo.
2. Standardize Airtable field naming conventions across all tables and workflows.
3. Configure automatic workflow triggering between components.
4. Run additional stress and edge-case testing before final submission.

---

# Overall Assessment

The capstone pipeline successfully demonstrates:
- incident ingestion
- AI classification
- protocol matching
- automated task generation
- dashboard-based task tracking

Despite temporary API limit issues during final testing, the workflows were previously validated successfully and the overall integration pipeline is operational.

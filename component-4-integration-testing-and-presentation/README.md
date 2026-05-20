# Integration, Testing & Presentation
# Emergency Response Coordinator
### Component 4: Integration, Testing & Presentation

> **Project 17** from the Capstone Project Ideas collection — a no-code AI system for managing emergency response workflows.

---

## What This Project Does

The Emergency Response Coordinator is a four-component system that turns a free-text incident report into a fully tracked, role-assigned emergency response workflow in seconds. When someone reports "smoke coming from the cafeteria," the system classifies the emergency, retrieves the correct response protocol, generates step-by-step tasks for each responder, and displays live progress on a dashboard — all automatically.

---

## System Architecture

![Architecture Diagram]

---<img width="1431" height="759" alt="emergency-response-architectur" src="https://github.com/user-attachments/assets/ba17991e-d41d-40c6-820b-e9af9034f8e2" />


## How the Four Components Connect

```
New Incident Report (free text)
        │
        ▼
┌─────────────────────┐
│  Component 1        │  Protocol Knowledge Base (Hala E.)
│  Airtable + Flowise │  Stores 5 structured protocols loaded
│  Vector Store       │  into Flowise's in-memory vector store
└──────────┬──────────┘
           │ protocols available for semantic search
           ▼
┌─────────────────────┐
│  Component 2        │  Incident Classifier (Astra)
│  n8n + Flowise      │  Classifies incident type, matches protocol,
│  + Groq + HF API    │  scores severity & confidence → Airtable
└──────────┬──────────┘
           │ status = "classified" triggers C3
           ▼
┌─────────────────────┐
│  Component 3        │  Task Assignment & Tracking (Farida)
│  n8n + Airtable     │  Reads protocol steps, generates tasks,
│                     │  assigns roles, calculates due times
└──────────┬──────────┘
           │ tasks written to shared Airtable base
           ▼
┌─────────────────────┐
│  Component 4        │  Integration, Testing & Presentation (You)
│  Airtable Dashboard │  Shared database design, test data,
│  + GitHub Pages     │  dashboards, documentation, demo
└─────────────────────┘
```

---

## Component 4 Responsibilities

This component is the project backbone. Everything below was owned and built by the Component 4 team member.

### 1. Shared Airtable Base Design

The entire system runs on one shared Airtable base. All tables, fields, linked records, and views were designed here before other components built on top of them.

| Table | Key Fields | Used By |
|---|---|---|
| `Protocols` | protocol_id, emergency_type, description, trigger_keywords, severity, roles_involved, steps, ai_summary | C1, C2 |
| `Protocol_Steps` | Step_Id, Protocol_Id, Step_Order, Task_Name, Assigned_Role, Due_Minutes, Priority | C3 |
| `Incident_Reports` | incident_text, status (new → classified) | C2 |
| `Incidents` | incident_type, protocol_id, severity, recommended_steps, confidence, status | C2, C3, C4 |
| `Tasks` | Task_Id, Incident_Id, Task_Name, Assigned_Role, Status, due_time, Priority, Step_Order | C3, C4 |
| `Responders` | name, role, contact | C3, C4 |

**Linked records:** Incidents → Protocols, Tasks → Incidents, Tasks → Responders  
**Formula fields:** due_time calculated from incident creation + Due_Minutes, overdue flag when due_time < now()  
**Rollup fields:** task completion count per incident, open task count per responder

---

### 2. Test Data

Realistic test data was created to allow all components to develop and demo independently.

| Dataset | Count | Details |
|---|---|---|
| Emergency protocols | 5 | FIRE_001, FIRE_002, MED_001, MED_002, LOCK_001 — each with 6–8 steps |
| Incident scenarios | 20+ | Covering all 3 emergency types (fire, medical, lockdown), varied phrasing |
| Protocol steps | 35+ | Full step-by-step entries for all 5 protocols |
| Responder records | 10 | Varied roles: security, medical, facilities, admin |
| Pre-generated tasks | 30+ | One full task set per test incident for dashboard population |

Test incidents include edge cases: vague descriptions, multi-keyword reports, and scenarios that could match more than one protocol (used to verify Component 2's confidence scoring).

---

### 3. Airtable Dashboard Views

Four interface views were built in Airtable to support both live operation and the showcase demo.

| View | Type | What It Shows |
|---|---|---|
| **Active Incident Kanban** | Kanban | Tasks grouped by Status (Pending / In Progress / Completed / Overdue) |
| **Task Status by Responder** | Gallery | Open tasks per assigned role, sorted by priority |
| **Action Timeline** | Grid | All tasks across all incidents sorted by due_time, overdue highlighted |
| **Post-Incident Review** | Gallery | Closed incidents with completion stats and protocol used |

---

### 4. End-to-End Integration Testing

All components were connected and tested as a complete system. The verification checklist below was used during integration.

**Integration Checklist**

- [ ] New record in `Incident_Reports` (status = `new`) triggers Component 2's n8n workflow
- [ ] Flowise chatflow returns correct `incident_type` for all 3 emergency types
- [ ] Classified incident record appears in `Incidents` table with all fields populated
- [ ] Component 3's n8n workflow detects `status = "classified"` and retrieves correct protocol steps
- [ ] Tasks are generated with correct `Assigned_Role`, `Priority`, and `due_time`
- [ ] Tasks appear in the Active Incident Kanban with status `Pending`
- [ ] Task status updates propagate to dashboard views in real time
- [ ] Post-incident records appear in the Post-Incident Review gallery after closure
- [ ] All linked records resolve correctly (Tasks → Incidents → Protocols)

**Known Issues / Workarounds**

- Component 2 uses an in-memory vector store in Flowise, which resets on restart. Before demos, trigger the n8n protocol-loading workflow to reload embeddings.
- Due time calculations assume the n8n server timezone matches Airtable. Verify both are set to the same timezone before live demos.

---

## Setup Guide

Follow these steps in order to get the full system running.

### Prerequisites

- Airtable account (free tier works)
- n8n Cloud account (free tier works)
- Flowise Cloud account (free tier works)
- Groq API key — free at [console.groq.com](https://console.groq.com)
- HuggingFace API key — free at [huggingface.co/settings/tokens](https://huggingface.co/settings/tokens)

---

### Step 1 — Set Up the Airtable Base

1. Create a new base named `Emergency Response Coordinator`
2. Create the following tables with the fields listed in the [Shared Airtable Base Design](#1-shared-airtable-base-design) section above
3. Import the test data CSV files from the `/test-data/` folder in this repo:
   - `protocols.csv` → `Protocols` table
   - `protocol_steps.csv` → `Protocol_Steps` table
   - `responders.csv` → `Responders` table
4. Create linked record fields as described in the table above
5. Generate an Airtable API key at **Account → API** and save it — all components need it

---

### Step 2 — Set Up Component 1 (Protocol Knowledge Base)

1. Confirm the `Protocols` table is populated with all 5 protocols
2. Verify the `trigger_keywords` and `ai_summary` fields are filled for each record
3. Share the Airtable base with Component 2's n8n so it can read protocols

---

### Step 3 — Set Up Component 2 (Incident Classifier)

1. In Flowise, create a new chatflow with:
   - **LLM node**: Groq Chat (model: `llama-3.3-70b-versatile`, temperature: 0.1)
   - **Embeddings node**: HuggingFace Inference (`sentence-transformers/distilbert-base-nli-mean-tokens`)
   - **Vector Store node**: In-Memory Vector Store
   - **Chain node**: Conversational Retrieval QA Chain
2. Add your classification system prompt (see `/flowise/classification-prompt.txt`)
3. Get the Flowise chatflow API URL from the **Share** button
4. In n8n, import the workflow from `/n8n/incident-classifier-workflow.json`
5. Set credentials: Airtable API key, Flowise API URL
6. Activate the workflow

---

### Step 4 — Set Up Component 3 (Task Assignment)

1. In n8n, import the workflow from `/n8n/task-assignment-workflow.json`
2. Set credentials: Airtable API key
3. Verify the workflow reads from `Incidents` (filter: status = `classified`) and writes to `Tasks`
4. Activate the workflow

---

### Step 5 — Set Up Dashboard Views (Component 4)

1. In Airtable, open the `Tasks` table and create the four views listed in the [Dashboard Views](#3-airtable-dashboard-views) section
2. Configure the Kanban view to group by `Status`
3. Configure the Timeline view to sort by `due_time` ascending
4. Apply conditional coloring: red for `Overdue`, orange for `In Progress`, green for `Completed`

---

### Step 6 — End-to-End Test

1. Add a new record to `Incident_Reports` with any of these test descriptions:
   - `"Smoke detected in the east stairwell on the 3rd floor"`
   - `"Student collapsed in the cafeteria, unresponsive"`
   - `"Suspicious individual reported near the main entrance, possible weapon"`
2. Wait ~30 seconds for the n8n workflows to trigger
3. Verify a new record appears in `Incidents` with status = `classified`
4. Verify tasks appear in `Tasks` and in the Active Incident Kanban
5. Manually update a task status to `In Progress` — confirm the dashboard updates

---

## Repository Structure

```
emergency-response-coordinator/
├── README.md                          ← This file
├── architecture/
│   ├── emergency-response-architecture.drawio
│   └── emergency-response-architecture.png
├── test-data/
│   ├── protocols.csv
│   ├── protocol_steps.csv
│   ├── responders.csv
│   └── sample-incidents.csv
├── n8n/
│   ├── incident-classifier-workflow.json
│   └── task-assignment-workflow.json
├── flowise/
│   └── classification-prompt.txt
└── docs/
    └── setup-guide.md
```

---

## Tools Used

| Tool | Purpose | Component |
|---|---|---|
| Airtable | Shared database, dashboard views | All |
| n8n Cloud | Workflow automation, API calls | C2, C3 |
| Flowise Cloud | LLM chain builder, RAG system | C1, C2 |
| Groq API | LLM inference (llama-3.3-70b) | C2 |
| HuggingFace Inference API | Text embeddings for semantic search | C2 |
| GitHub + GitHub Pages | Version control, portfolio page | C4 |
| draw.io | Architecture diagram | C4 |

---

## Team

| Component | Role | Owner |
|---|---|---|
| Component 1 | Protocol Knowledge Base | Hala E. |
| Component 2 | Incident Classifier | Astra |
| Component 3 | Task Assignment & Tracking | Farida |
| Component 4 | Integration, Testing & Presentation | Md M. |

---

## Demo

> A walkthrough video and live demo are available on the [GitHub Pages portfolio site](https://your-username.github.io/emergency-response-coordinator).

The demo uses the 3 test incident scenarios included in `/test-data/sample-incidents.csv`. Each scenario walks through the full pipeline from raw report to populated task dashboard in under 60 seconds.

---

*Built for Capstone Project 17 — Emergency Response Coordinator*

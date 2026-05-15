# Task Assignment & Tracking
**Owner:** Farida
## Description
This component of the Emergency Response Coordinator project focuses on creating a workflow that activates the selected protocol, assigns each task to the appropriate responder, and tracks the status of completion.

The workflow uses n8n and Airtable to:
- retrieve classified incidents
- identify the corresponding emergency protocol
- retrieve protocol steps
- automatically generate emergency response tasks
- assign roles and priorities
- track task progress through a Kanban dashboard

---

# Features

- Automatic task generation from emergency protocols
- Dynamic protocol step retrieval
- Role-based task assignment
- Priority-based emergency response handling
- Automatic due-time generation
- Step-by-step emergency task tracking
- Airtable Kanban dashboard integration
- Multi-protocol emergency support

Supported protocols:
- FIRE_001
- FIRE_002
- MED_001
- MED_002
- LOCK_001

---

# Workflow Pipeline

Classified Incident  
↓  
Protocol Matching  
↓  
Protocol Step Retrieval  
↓  
Automatic Task Generation  
↓  
Role Assignment  
↓  
Priority & Due-Time Assignment  
↓  
Task Tracking Dashboard

---

# Technologies Used

- Airtable
- n8n
- Flowise AI
- JSON APIs

---

# Database Structure

## Protocol Steps Table
Stores structured emergency protocol steps used for task generation.

Fields:
- Step_Id
- Protocol_Id
- Step_Order
- Task_Name
- Assigned_Role
- Due_Minutes
- Priority

---

## Tasks Table
Stores automatically generated emergency response tasks.

Fields:
- Task_Id
- Incident_Id
- Protocol_Id
- Task name
- Assigned role
- Status
- due_time
- priority
- Step_Order

---

# Automation Features

- Detects newly classified incidents
- Matches incidents to emergency protocols
- Retrieves corresponding protocol steps dynamically
- Generates individual emergency response tasks
- Assigns responsible roles
- Calculates due times automatically
- Tracks task progress visually using a Kanban board

---

# Task Status Categories

- Pending
- In Progress
- Completed
- Overdue

---

# Screenshots

## n8n Workflow
![n8n Workflow](screenshots/n8n-workflow.png)

## Task Tracking Dashboard
![Kanban Board](screenshots/kanban-board.png)

## Generated Emergency Tasks
![Tasks Table](screenshots/tasks-table.png)

---

# Future Improvements

- Automatic overdue task escalation
- Real-time notifications
- Email/SMS emergency alerts
- Multi-user responder tracking
- Analytics dashboard

## Status
- [ ] Design complete
- [ ] Sample data prepared
- [ ] Initial implementation
- [ ] Testing
- [ ] Integration with other components
- [ ] Documentation complete

# Task Assignment & Tracking
**Owner:** Farida
## Description
Creates a workflow that activates the selected protocol, assigns each task to the appropriate responder, tracks the status of completion and sends out reminders when tasks are delayed.
# Emergency Response Coordinator System

## Overview
The Emergency Response Coordinator System is an AI-powered workflow automation platform designed to classify emergency incidents and automatically generate response tasks using predefined emergency protocols. The system integrates Airtable, n8n, and Flowise AI to streamline emergency coordination and task tracking.

---

# Features

- AI-powered incident classification
- Automated protocol matching
- Dynamic emergency task generation
- Role-based task assignment
- Priority-based response handling
- Due-time generation for emergency tasks
- Step-by-step protocol execution tracking
- Airtable task management dashboard
- Kanban-style task monitoring
- Multi-protocol emergency support

Supported protocols:
- FIRE_001
- FIRE_002
- MED_001
- MED_002
- LOCK_001

---

# Workflow Pipeline

Incident Report  
↓  
AI Incident Classification  
↓  
Protocol Identification  
↓  
Protocol Step Retrieval  
↓  
Automatic Task Generation  
↓  
Task Assignment & Tracking Dashboard

---

# Technologies Used

- Airtable
- n8n
- Flowise AI
- JSON APIs

---

# Database Structure

## Protocols Table
Stores emergency response protocols and classifications.

Fields:
- Protocol ID
- Emergency Type
- Description
- Trigger Keywords
- Severity
- Roles Involved
- Steps
- Priority
- AI Summary

---

## Protocol Steps Table
Stores structured protocol steps for automated task generation.

Fields:
- Step_Id
- Protocol_Id
- Step_Order
- Task_Name
- Assigned_Role
- Due_Minutes
- Priority

---

## Incidents Table
Stores classified emergency incidents.

Fields:
- record_id
- protocol_id
- status
- incident_type
- incident_text
- severity
- confidence
- recommended_steps
- source

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

- Automatically detects newly classified incidents
- Matches incidents to corresponding emergency protocols
- Retrieves protocol steps dynamically
- Generates individual emergency tasks automatically
- Assigns responsible roles
- Calculates task due times
- Tracks task progress using Kanban boards

---

# Task Status Categories

- Pending
- In Progress
- Completed
- Overdue

---

# My Contribution

Designed and implemented the automated task assignment and tracking workflow, including:
- Airtable database architecture
- Protocol step structure
- Dynamic task generation system
- Priority handling
- Due-time automation
- Kanban task tracking dashboard
- n8n workflow integration

---

# Screenshots

Add screenshots of:
- Airtable dashboard
- Kanban task board
- n8n workflows
- Generated emergency tasks

---

# Future Improvements

- Real-time notifications
- SMS/email emergency alerts
- Automatic overdue task escalation
- User authentication
- Advanced analytics dashboard
- Multi-user coordination system
## Status
- [ ] Design complete
- [ ] Sample data prepared
- [ ] Initial implementation
- [ ] Testing
- [ ] Integration with other components
- [ ] Documentation complete

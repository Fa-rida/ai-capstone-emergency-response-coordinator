# Emergency Response Coordinator
## Hala, Astra, Farida, MD
| Name | Role/Component | GitHub Username |
|------|---------------|-----------------|
| Hala | Protocol Knowledge Base | @lockedinlulu |
| Astra | Incident Classifier | @yunastra |
| Farida | Task Assignment & Tracking | @Fa-rida |
| MD | Integration, Testing & Presentation | @[username] |

## Problem Statement
This project designs a system that carries out appropriate response protocols in emergencies. It helps organizations digitize emergency procedures that can be followed accurately. In stressful situations, people are prone to forgetting steps or making errors and printed out protocols are time consuming and not as effective. This system reduces the possibility of human error in the chaos that ensues during an emergency by guiding responders through the right steps and ensuring tasks are completed.

## Target Users
A college security team responsible for controling emergency situations. This team needs a fast and reliable way to coordinate evacuations and responses, as manually following written protocols in high stress situations is time consuming.

## Architecture
![Architecture Diagram](docs/architecture.png)

## Component Breakdown
### Component 1: Protocol Knowledge Base (Owner: Hala)
- **Description:** Builds a workflow that stores emergency response protocols into the system.
- **Tools:** n8n, Airtable, Flowise
- **Input:** Information about emergency protocols
- **Output:** Knowledge base for AI search
- **Standalone demo:** When an emergency protocol is inputted, the system processes it and information about the next steps shows up in airtable. This means the protocol exists in the database.

### Component 2: Incident Classifier (Owner: Astra)
- **Description:** Designs a system that receives the report, understands the incident and recommends the correct protocol from the base knowledge. 
- **Tools:** Flowise, Groq
- **Input:** Incident report
- **Output:** Recommended emergency protocol
- **Standalone demo:** In a test case scenario, this component receives information about the incident happening (for example a fire), then it suggests the right emergency protocol for that situation.

### Component 3: Task Assignment & Tracking (Owner: Farida)
- **Description:** Creates a workflow that activates the selected protocol, assigns each task to the appropriate responder, tracks the status of completion and sends out reminders when tasks are delayed.
- **Tools:** n8n, Airtable
- **Input:** Type of emergency
- **Output:** assigned roles, status of tasks being carried out
- **Standalone demo:** For example, in the event of a fire, the system activates the fire response protocol, creates the needed tasks, assigns them to the needed personnel and tracks the status in Airtable. If there is a delay in performing a task, a reminder is sent out.

### Component 4: Integration, Testing & Presentation (Owner: MD)
- **Description:** Connects all the parts into one working system. Ensures data flows correctly between components, builds a dashboard to display active incidents and progress, tests the system, and prepares the final presentation.
- **Tools:** Airtable, GitHub, Draw.io
- **Input:** Information about incident and task progress.
- **Output:** A dashboard that displays the progress of activated emergency protocols.
- **Standalone demo:** In a simulated scenario, the dashboard displays information about the activated protocol. It also shows the task completion status, allowing users to easily monitor the progress of the activated protocol.

## Data Sources
- **Primary data:** Emergency response protocol designed by a schools’s public safety office.
- **Sample data:** Simulated emergency scenarios created by our team for demonstration purposes.
- **Data format:** JSON records and CSV files (to populate the Airtable)

## AI Capabilities
| Capability | Purpose | Model/API |
|-----------|---------|-----------|
| Incident Classification | Determine the type of emergency | Hugging Face |
| Protocol Suggestion | Choose the correct response protocol | Flowise |
| Severity Detection | Identify the urgency level of the incident | Groq |

## Success Criteria
1. The system correctly identifies at least 80% of the incident types.
2. The system successfully pulls all the appropriate response protocols from the knowledge base.
3. The system automatically assigns the right tasks to the right personnel in at least 9 out of 10 cases.
4. The system correctly identifies the severity level of the incident in at least 8 out of 10 test case scenarios.
5. Necessary information about active incidents and their completion status are all displayed on the dashboard with updates made visible within 5 seconds.

## Timeline
| Week | Milestone |
|------|-----------|
| 3 (Now) | Project proposal + architecture diagram + GitHub repo |
| 4-6 | Build individual components, test with sample data |
| 7-9 | Add LLM/agent capabilities, refine AI processing |
| 10-12 | Integration, error handling, dashboard/UI |
| 13-14 | Polish, documentation, demo preparation |
| 15 | Final presentation |

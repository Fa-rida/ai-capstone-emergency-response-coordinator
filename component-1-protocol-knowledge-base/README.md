## Component Owner: Hala E.
Protocol Knowledge Base (Component 1)

---

## Overview

This component builds the foundational **emergency response protocol knowledge base** for the overall system.

It is responsible for storing structured emergency procedures in a standardized format so that downstream components (incident classification, task assignment, and dashboard integration) can reliably access and process emergency information.

The goal is to reduce ambiguity during emergency situations by converting unstructured protocols into a **clean, machine-readable database**.

---

## Purpose

During emergency situations, relying on unstructured or written procedures can lead to delays and human error.

This system ensures that all emergency protocols are:
- Structured consistently
- Easily searchable
- AI-compatible for classification and automation
- Ready for integration with downstream workflows

---

## Database Structure (Airtable Schema)

Each emergency protocol is stored as a single record in Airtable with the following fields:

- `protocol_id` → Unique identifier (e.g., FIRE_001)
- `emergency_type` → Type of emergency (Fire, Medical, Lockdown, etc.)
- `description` → Short explanation of the protocol
- `trigger_keywords` → Keywords used for AI classification
- `severity` → Low / Medium / High
- `roles_involved` → Personnel responsible for action
- `steps` → Step-by-step emergency response procedure
- `priority` → Response urgency ranking
- `ai_summary` → One-to-two sentence natural language summary

---

## 📊 Data Sources

Sample protocols were created using:
- Internal emergency procedure guidelines (school/public safety style references)
- NYC Open Data emergency incident datasets (used as inspiration for real-world structure and categorization)

Reference dataset:
[https://catalog.data.gov/dataset/incidents-responded-to-by-fire-companies
](https://catalog.data.gov/dataset/incidents-responded-to-by-fire-companies)
---

## Our Sample Data

The current knowledge base includes structured protocols for:

- Fire emergencies
- Medical emergencies
- Security lockdown situations

Each entry is manually structured and standardized to ensure consistency and AI readability.

---

## ⚙️ Implementation Details

- Built using **Airtable**
- Data is manually curated and structured into predefined fields
- Designed to support downstream AI workflows including:
  - Incident classification (Component 2)
  - Task assignment (Component 3)
  - Dashboard visualization (Component 4)

---

## System Role

This component acts as the **foundational data layer** of the system.

All other components depend on this knowledge base:

- Component 2 reads and classifies incidents using this data
- Component 3 converts protocols into actionable tasks
- Component 4 visualizes active emergencies and progress

---

## Current Status

- ✔ Schema designed and implemented
- ✔ Sample protocols created (5 entries)
- ✔ Airtable database fully structured
- ✔ Fields standardized for AI compatibility
- ✔ Ready for integration with other system components

---

## Outcome

The result is a clean, structured emergency protocol knowledge base that enables:
- Reliable AI-based incident classification
- Automated emergency response workflows
- Scalable integration with future system components

---

## 📁 Project Structure (GitHub)

# Airtable Schema

## Table: `protocols`

This table stores all structured emergency response procedures used by the Emergency Response Coordinator system.

---

## Fields

| Field Name | Type | Description |
|-----------|------|-------------|
| `protocol_id` | Single Line Text | Unique identifier for each protocol |
| `emergency_type` | Single Select | Type of emergency (Fire, Medical, Lockdown, etc.) |
| `description` | Long Text | Short explanation of the emergency scenario |
| `trigger_keywords` | Long Text | Keywords used for classification and retrieval |
| `severity` | Single Select | Emergency severity level (`low`, `medium`, `high`) |
| `roles_involved` | Long Text | Personnel responsible for responding |
| `steps` | Long Text | Ordered emergency response procedure |
| `priority` | Number | Response urgency ranking |
| `ai_summary` | Long Text | Concise natural language summary of the protocol |

---

## Naming Standards

All fields follow project-wide data conventions:

- `snake_case`
- lowercase values where applicable
- consistent formatting across records

---

## Example Record

| Field | Example |
|------|---------|
| `protocol_id` | FIRE_001 |
| `emergency_type` | Fire |
| `description` | Fire emergency requiring immediate evacuation |
| `trigger_keywords` | smoke, fire, burning, alarm |
| `severity` | high |
| `roles_involved` | Security, Staff, Students |
| `steps` | Activate alarm → Evacuate → Contact emergency services |
| `priority` | 1 |
| `ai_summary` | High severity fire emergency requiring immediate evacuation procedures |

---

## Data Relationships

This table serves as the protocol reference layer for:

- Incident Classification
- Task Assignment & Tracking
- Dashboard Integration

---

## Status

**Schema finalized and ready for integration**

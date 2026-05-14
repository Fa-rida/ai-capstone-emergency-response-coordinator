# Incident Classifier

**Component Owner:** Astra  
**Project:** Emergency Response Protocol System  
**Role:** AI Core — Incident Classification

---

## Overview

This component is the AI brain of the Emergency Response Protocol System. It receives free-text incident reports, classifies the emergency type, matches it to the correct protocol from the knowledge base, and outputs structured data for downstream task assignment and dashboard visualization.

---

## Purpose

When an emergency is reported, responders need to immediately know what type of emergency it is and what steps to follow. Manual classification is slow and error-prone under pressure. This component automates that process — turning a raw incident description like *"smoke coming from the cafeteria"* into a structured, actionable classification in seconds.

---

## How It Works

1. A new incident report is added to the `Incident_Reports` table in Airtable with `status = "new"`
2. n8n detects the new record and sends the incident text to the Flowise chatflow via HTTP request
3. Flowise searches the protocol knowledge base using semantic similarity and generates a structured classification
4. n8n parses the response and writes a new record to the `Incidents` table with all fields populated and `status = "classified"`

---

## Tools Used

| Tool | Purpose |
|------|---------|
| Flowise Cloud | LLM chain and RAG system |
| Groq API | LLM inference (llama-3.3-70b-versatile) |
| HuggingFace Inference API | Embeddings (sentence-transformers/distilbert-base-nli-mean-tokens) |
| n8n | Workflow automation |
| Airtable | Input and output data storage |

---

## Flowise Chatflow Architecture

- **LLM:** Groq (llama-3.3-70b-versatile, temperature 0.1)
- **Embeddings:** HuggingFace Inference (sentence-transformers/distilbert-base-nli-mean-tokens)
- **Vector Store:** In-Memory Vector Store loaded with all 5 emergency protocols
- **Chain:** Conversational Retrieval QA Chain with custom classification prompt

---

## Output Schema

Each classified incident is written to the `Incidents` table with the following fields:

| Field | Type | Description |
|-------|------|-------------|
| `incident_text` | Long Text | Original free-text report |
| `incident_type` | Single Select | Fire / Medical / Lockdown |
| `protocol_id` | Single Line | Matched protocol (e.g. FIRE_001) |
| `severity` | Single Select | High / Medium / Low |
| `matched_keywords` | Long Text | Keywords that triggered the match |
| `recommended_steps` | Long Text | First 3 steps from matched protocol |
| `confidence` | Single Select | High / Medium / Low |
| `status` | Single Select | classified / error |
| `source` | Single Line | n8n |

---

## Integration

- **Depends on:** Component 1 (Protocol Knowledge Base) — protocols loaded into Flowise vector store
- **Feeds into:** Component 3 (Task Assignment) — reads records where `status = "classified"`
- **Feeds into:** Component 4 (Integration Dashboard) — classified records appear in dashboard views

---

## Current Status

- [x] Flowise chatflow built and tested
- [x] All 3 emergency types classifying correctly (Fire, Medical, Lockdown)
- [x] n8n workflow connecting Airtable → Flowise → Airtable
- [x] 20+ incidents processed and classified
- [x] Integrated with shared Airtable base

# Prompt Log — Astra

**Project:** AI-Powered Emergency Response Coordinator
**Component:** Component 2 — Incident Classifier

---

## Entry 1

**Date:** 2026-05-05
**Tool:** GitHub Copilot Chat
**Context:** Setting up the n8n workflow to poll Airtable for unprocessed incident records and forward them to the Flowise classifier.

**Prompt used:**
> "Write an n8n HTTP Request node configuration that sends a POST request to a Flowise chatflow endpoint with an incident description as the body."

**What Copilot gave me:**
A JSON structure for the HTTP Request node with the correct `application/json` content type and a body mapping using n8n expressions.

**What I changed:**
The generated body used a hardcoded field name. I updated it to dynamically reference the `description` field from the Airtable record using `{{ $json["description"] }}`.

**Evaluation:**
Useful starting point but needed adjustment for our specific Airtable schema. Saved time on the HTTP node setup but couldn't be used as-is.

---

## Entry 2

**Date:** 2026-05-08
**Tool:** GitHub Copilot Chat
**Context:** The Flowise chatflow was returning classification results in an inconsistent format — sometimes the emergency type was nested inside a JSON object, sometimes it was plain text.

**Prompt used:**
> "Write a JavaScript function that extracts the emergency type from a Flowise response that could be either plain text or a JSON object with a 'type' field."

**What Copilot gave me:**
A try/catch block that attempts `JSON.parse()` on the response and falls back to treating it as plain text.

**What I changed:**
Added a `.toLowerCase().trim()` on the extracted value to normalize the output before writing it back to Airtable, since field matching downstream was case-sensitive.

**Evaluation:**
Good suggestion. The try/catch pattern was exactly right. The normalization step was something I added myself after noticing a mismatch between "Fire" and "fire" in Airtable filters.

---

## Entry 3

**Date:** 2026-05-12
**Tool:** GitHub Copilot Chat
**Context:** Needed to update the Airtable `Incidents` record after classification — writing protocol_id, severity, confidence score, and changing status to `classified`.

**Prompt used:**
> "In n8n, how do I update multiple fields in an Airtable record in a single node after receiving a response from an external API?"

**What Copilot gave me:**
An explanation of using the Airtable Update Record node with field mappings, and a note that all fields need to be explicitly listed — n8n doesn't auto-map them.

**What I changed:**
Nothing major. Followed the suggestion directly and it worked. The only issue was a field name mismatch (`Protocol_Id` vs `protocol_id`) which was a schema inconsistency across the team, not a Copilot error.

**Evaluation:**
Accurate and directly applicable. The field name issue was a team coordination problem that Copilot couldn't have known about.

---

## Entry 4

**Date:** 2026-05-16
**Tool:** GitHub Copilot Chat
**Context:** During Checkpoint 2 end-to-end testing, the workflow started returning `PUBLIC_API_BILLING_LIMIT_EXCEEDED` errors from Airtable. Needed to understand what was causing it and how to reduce API call volume.

**Prompt used:**
> "My n8n workflow is hitting Airtable API rate limits during testing. What are common causes and how can I reduce the number of API calls without breaking the workflow logic?"

**What Copilot gave me:**
Suggestions including: batching record updates, adding a filter to only fetch records where `status = unprocessed` instead of polling the full table, and caching protocol data locally in n8n instead of re-fetching it every run.

**What I changed:**
Added a filter condition to the Airtable List Records node so it only retrieves `status = unprocessed` records. This significantly reduced the number of records processed per run and helped stay within the API limit during normal testing.

**Evaluation:**
Very helpful. The filtering suggestion was something I hadn't thought to do — I was fetching all records and filtering inside the workflow, which was wasteful. The fix was simple and effective.

---

## Entry 5

**Date:** 2026-05-20
**Tool:** GitHub Copilot Chat
**Context:** Re-running the capstone audit for Checkpoint 2 to compare current state against the Week 8 assessment.

**Prompt used:**
> "Based on this Week 8 audit report, what questions should I answer to assess whether the integration gaps have been resolved by Checkpoint 2?"

**What Copilot gave me:**
A list of follow-up questions organized by component: Does Ingestion write the correct status value? Does AI Core pick up records reliably? Are field names consistent across tables? Does the Specialist trigger on AI Core's output without manual intervention?

**What I changed:**
Used the questions as a checklist while reviewing the end-to-end test results rather than copying them directly into the audit doc.

**Evaluation:**
Useful framing tool. Turning the Week 8 audit into a checklist of yes/no questions made the Checkpoint 2 comparison much easier to write. Would use this approach again for future audits.

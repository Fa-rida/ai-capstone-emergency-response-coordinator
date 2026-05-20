# Week 7: RAG Security Knowledge Assistant — Evaluation Report

## 1. Setup Summary

- **LLM:** llama-3.3-70b-versatile via Groq
- **Embeddings:** sentence-transformers/all-MiniLM-L6-v2 via HuggingFace
- **Vector Store:** In-Memory Vector Store
- **Documents loaded:** 
  - mitre-initial-access.txt (~3 pages)
  - mitre-credential-access.txt (~3 pages)
  - mitre-lateral-movement.txt (~2 pages)

---
## Chat Link ##
https://cloud.flowiseai.com/chatbot/91331532-eb90-4661-a194-32e5837e77b0
---

## 2. Test Results

| # | Question | Used Documents? | Quality | Notes |
|---|----------|----------------|---------|-------|
| 1 | What techniques do attackers use for credential access? | Yes | Good | The chatbot correctly referenced the Brute Force technique from the uploaded MITRE ATT&CK documents and accurately explained how attackers use repetitive authentication attempts to gain credentials. |
| 2 | How does phishing help adversaries gain initial access? | Yes | Good | The chatbot accurately summarized the phishing section from the uploaded documents, including spearphishing, malicious links and attachments, phone-based phishing, and real-world adversary examples such as AppleJeus and INC Ransom. |
| 3 | What is the difference between pass the hash and credential dumping? | Yes | Good | The chatbot clearly distinguished between Credential Dumping (extracting credentials or password hashes from systems) and Pass the Hash (using stolen password hashes for authentication and lateral movement). |
| 4 | How do attackers use valid accounts during cyberattacks? | Yes | Good | The chatbot accurately explained how attackers abuse compromised credentials for remote access, persistence, privilege escalation, and lateral movement. |
| 5 | What are common methods used in drive-by compromise attacks? | Yes | Good | The chatbot accurately identified compromised websites, malicious advertisements, watering hole attacks, XSS attacks, and browser push notification abuse as common drive-by compromise techniques. |

---

## 3. Edge Case Observations

- **Unrelated question:** When asked “What is the weather like today?”, the chatbot responded with “Hmm, I’m not sure” instead of hallucinating an answer. This showed that the RAG system relied on the uploaded documents rather than generating random information.
  
- **Topic not in documents:** Questions unrelated to cybersecurity techniques were not answered confidently. The chatbot admitted it was not sure instead of inventing information, which showed accuracy.

---

## 4. Settings Experiments (if completed)

- **Temperature change:** Lower temperature values produced more focused and factual responses, while higher values made responses slightly more creative but less precise.
  
- **Chunk size change:** Surprisingly, smaller chunk sizes gave me a little bit more information than larger chunk sizes.
  
- **Top K change:** Increasing Top K allowed the chatbot to retrieve more document chunks, which improved context.
---

## 5. Reflection

### What surprised you about how RAG works?

One surprising aspect of RAG was how effectively the chatbot retrieved information directly from uploaded documents instead of relying entirely on the language model’s memory. It was also interesting to see how unrelated questions were rejected because the information was not present in the vector database.

### How could you improve this chatbot for real-world use?

This chatbot could be improved by adding more cybersecurity documents, using a persistent vector database instead of in-memory storage so that document embeddings remain stored permanently, improving the user interface, and adding stronger filtering for malicious or irrelevant prompts. It could also support PDF uploads and larger knowledge bases.

### How might you use RAG in your capstone project?

RAG could significantly improve my AI-powered Emergency Response Coordinator System by allowing emergency responders to quickly retrieve relevant emergency procedures, response protocols, evacuation guidelines, and medical instructions from stored knowledge bases in real time.

In my capstone project, incidents are submitted through an automated workflow where Flowise AI classifies the emergency type and severity level before tasks are dynamically generated and tracked through Airtable and n8n. Integrating RAG into this system would allow responders to ask natural language questions such as “What are the evacuation procedures for a fire emergency?” or “What steps should be completed during a lockdown situation?” and receive accurate responses directly from trusted emergency response documentation.

This would improve response speed, decision-making, and coordination during emergencies while reducing the need to manually search through procedures or protocol documents.


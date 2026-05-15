# Model Comparison Report — Week 4

**Name:** Farida Shehu  
**Date:** [03/17/2026]  
**Capstone Project:** [Emergency Response Coordinator]  
**My Component:** [Task Assignment & Tracking]

## Test Setup
**Input dataset:** 5 cybersecurity text samples covering:
- suspicious login activity
- routine firewall update
- phishing detection
- repeated authentication failures
- normal system behavior

**Models tested:**
1. distilbert-base-uncased-finetuned-sst-2-english (sentiment)
2. facebook/bart-large-mnli (zero-shot classification)
3. dslim/bert-large-NER / bert-base-NER (named entity recognition)
4. Groq Llama 3 8B / llama-3.1-8b-instant (LLM classification)

**Evaluation criteria:** label accuracy, confidence score, usefulness for cybersecurity analysis, ease of integration in n8n

## Results Summary

| Record | Sentiment | Zero-Shot | NER Entities | Groq |
|--------|-----------|-----------|-------------|------|
| 1 | NEGATIVE (0.9994) | unverified report (0.9) | {} | HIGH – indicates suspicious unauthorized login behavior |
| 2 | NEGATIVE (0.9986) | [no result] | {} | MEDIUM – there could be potential issues after the update |
| 3 | NEGATIVE (0.9963) | [no result] | {} | CRITICAL – phishing email suggests potential security breach |
| 4 | [no result] | [no result] | detected entity output | [no result] |
| 5 | [no result] | [no result] | {} | [no result] |

## Analysis

**Where models agreed:**  
The sentiment model and Groq both identified records 1 and 3 as concerning. Record 1 involved an unauthorized login attempt, and record 3 involved phishing, so both models treated them as suspicious events.

**Where models disagreed:**  
Record 2 showed disagreement. The sentiment model marked it as NEGATIVE, while Groq labeled it MEDIUM severity. This makes sense because firewall rule updates may sound negative in wording but can still be routine maintenance. The zero-shot and NER models were less consistent because they returned incomplete results for several records.

**Most accurate model overall:**  
Groq was the most accurate and useful overall because it provided severity-based classifications and short explanations that matched cybersecurity decision-making better than simple sentiment labels.

**Fastest/most practical:**  
The Hugging Face sentiment model was the simplest and fastest to integrate, but it was less useful for actual security analysis. Groq was more practical for real-world classification because its responses were more meaningful.

## Recommended Models for My Capstone Component

**Component:** [Task Assignment & Tracking]

**Primary model:** Groq Llama 3 — It produced the most useful classifications because it assigned severity levels and explained why an alert was concerning.

**Secondary model (if applicable):** Hugging Face Sentiment — It can serve as a lightweight supporting signal, but it should not be the main model for cybersecurity alert analysis.

**Rejected models and why:**
- **Zero-Shot Classification:** It gave a reasonable result for one record, but it did not produce complete outputs across the whole dataset.
- **NER:** It was not very useful for these records because most alerts did not contain strong named entities such as people, places, or organizations.

## Failure Cases and Limitations

One important limitation was that several models returned incomplete or empty outputs for some records. For example, the zero-shot model only produced a classification for one record, and the NER model often returned empty results. This shows that workflow success does not always mean every model output will be equally useful. In production, these models would need more testing, better prompt design, or fallback logic.

## Next Steps

If I had more time, I would test more cybersecurity records, especially examples with clearer entity information such as usernames, domains, IP addresses, and organization names. I would also try a cybersecurity-specific classification model and compare it against Groq to see whether a domain-specific model performs better.

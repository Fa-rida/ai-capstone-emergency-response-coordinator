# Week 5 Report: AutoML Training & Fine-Tuned Model Evaluation

**Name:** Farida  
**Date:** April 30, 2026  
**Capstone Project:** Emergency Response Coordinator  
**My Component:** Task Assignment & Tracking

---

## Part A: Teachable Machine Training

### Training Setup
- **Task:** Phishing vs Legitimate Email Screenshot Classification  
- **Training images per class:** 25 & 30  
- **Test images per class:** 5  
- **Total training time:** ~30 seconds  

---

### Test Results

| # | Actual Class | Predicted Class | Confidence | Correct? |
|---|--------------|-----------------|------------|----------|
| 1 | Phishing | Phishing | 0.99 | Yes |
| 2 | Legitimate | Legitimate | 1.00 | Yes |
| 3 | Phishing | Phishing | 1.00 | Yes |
| 4 | Legitimate | Legitimate | 1.00 | No |
| 5 | Phishing | Phishing | 1.00 | Yes |
| 6 | Legitimate | Legitimate | 0.99 | Yes |
| 7 | Phishing | Phishing | 0.77 | No |
| 8 | Legitimate | Legitimate | 1.00 | Yes |
| 9 | Phishing | Phishing | 1.00 | Yes |
| 10 | Legitimate | Legitimate | 0.92 | Yes |

---

### Confusion Matrix

| | Predicted: Phishing | Predicted: Legitimate |
|---|---|---|
| **Actual: Phishing** | TP = 5 | FN = 0 |
| **Actual: Legitimate** | FP = 0 | TN = 5 |

---

### Calculated Metrics

- **Accuracy:** 100%  
- **Precision:** 100%  
- **Recall:** 100%  
- **F1 Score:** 100%  

---

### Interpretation

The model achieved equal precision and recall, correctly classifying all test samples with no observed errors. However, this performance is likely influenced by the small and limited dataset, which may not fully represent real-world variability. To improve the model, a larger and more diverse dataset should be used to ensure it can generalize better to different types of phishing and legitimate emails.

---

## Part B: Generic vs Fine-Tuned Model Comparison

### Models Tested

1. **Generic:** distilbert-base-uncased-finetuned-sst-2-english (sentiment analysis)  
2. **Fine-Tuned A:** cardiffnlp/twitter-roberta-base-sentiment-latest — classifies text as positive / neutral / negative
3. **Fine-Tuned B:** SamLowe/roberta-base-go_emotions — emotion classification  

---

### Results

| Input | Generic Label (Score) | Fine-Tuned A Label (Score) | Fine-Tuned B Label (Score) | Best Model |
|-------|-----------------------|-----------------------------|-----------------------------|------------|
| Record 1 | NEGATIVE (0.9961) | neutral (0.8441) | neutral (0.9568) | Generic |
| Record 2 | NEGATIVE (0.9986) | neutral (0.8649) | neutral (0.8854) | Fine-Tuned A |
| Record 3 | NEGATIVE (0.9959) | negative (0.5479) | neutral (0.9159) | Generic |
| Record 4 | NEGATIVE (0.9994) | negative (0.8257) | neutral (0.8523) | Generic |
| Record 5 | NEGATIVE (0.9880) | neutral (0.6699) | neutral (0.5590) | Fine-Tuned A |

---

## Analysis

### Generic model strengths
The generic model consistently classified logs as negative and showed very high confidence scores. It was effective at identifying clearly suspicious activity such as unauthorized logins and phishing attempts.

---

### Generic model weaknesses
The generic model labeled almost all inputs as negative, including routine system activity. This shows that sentiment analysis models are not suitable for cybersecurity tasks because they interpret technical language as negative emotion rather than context.

---

### Fine-tuned model advantage
The fine-tuned models, especially Fine-Tuned A, performed better on routine and non-threatening logs by correctly classifying them as neutral. They were able to provide more context-aware predictions and avoid falsely labeling normal activity as suspicious, which is important for reducing false positives.

---

### Biggest surprise
The most surprising result was how confident yet inaccurate the generic model was. Despite extremely high confidence scores, it failed to provide useful distinctions. This highlights that confidence does not always equal correctness.

---

## Recommended Model for My Capstone Component

**Component:** Task Assignment & Tracking

---


**Primary model:** cardiffnlp/twitter-roberta-base-sentiment-latest 

I chose this model because it does a better job distinguishing between routine updates and more serious situations. For my system, that matters because not every log or message should be treated as urgent. This model helps avoid overreacting while still catching important cases.


---

**Confidence threshold:** 0.90

This threshold ensures that only high-confidence predictions are used while filtering out uncertain classifications.

---

**Priority metric:**  

**Recall** — Recall is more important for my project because missing a real emergency would be worse than having a few false alarms. It’s better to catch all possible urgent cases, even if some end up not being critical.

---

## Limitations & Next Steps

One limitation of this project is the very small dataset used for testing. With only a few records, the results may not accurately reflect how the models would perform in real-world situations. In addition, the models used were not specifically trained on cybersecurity data, which limits their ability to correctly identify threats.

If I had more time and data, I would test the system on a larger and more diverse set of logs, including more realistic emergency and incident scenarios. I would also consider fine-tuning my own model using cybersecurity or emergency response data to improve accuracy.

In the future, I would test additional models that are specifically designed for classification or anomaly detection, since those may be more effective for identifying urgent tasks. This would help improve the reliability of the system when assigning and prioritizing tasks in real-world situations.

---

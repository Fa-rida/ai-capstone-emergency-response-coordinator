# Week 5: AutoML & No-Code Model Training

Trained a custom image classifier with Google Teachable Machine and compared generic vs fine-tuned Hugging Face models for the Task Assignment & Tracking component of our Emergency Response Coordinator System.

---

## Custom Model Training

- Built a Phishing vs Legitimate image classifier with Teachable Machine  
- Achieved **100% accuracy** on 10 held-out test images  
- Precision: **100%** | Recall: **100%** | F1: **100%**

---

## Fine-Tuned Model Comparison

Compared 3 models (1 generic + 2 fine-tuned) on 5 test inputs:

- **Generic:** distilbert-base-uncased-finetuned-sst-2-english (sentiment)  
- **Fine-Tuned A:** cardiffnlp/twitter-roberta-base-sentiment-latest (sentiment)  
- **Fine-Tuned B:** SamLowe/roberta-base-go_emotions (emotion classification)  

---

## Finding

Recommended **cardiffnlp/twitter-roberta-base-sentiment-latest** for Task Assignment & Tracking because it best distinguishes between routine and urgent events without labeling everything as negative.

Fine-tuned models showed **higher** performance with **more relevant labels and better handling of edge cases**.

---

See `report.md` for full analysis.

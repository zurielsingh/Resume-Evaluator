# Resume-Ranking-Program  
An AI-powered resume evaluation system using BERT regression to deliver consistent, bias-reduced scoring  

---

## 📖 About the Project  
The **Resume Ranking Program** is an automated résumé evaluation system developed using **Natural Language Processing (NLP)** and a **BERT-based regression model**.

Structured résumé attributes : **Skills, Experience, Education, Certifications, and Projects** are transformed into natural language text and processed by a fine-tuned transformer model to predict a **continuous résumé quality score (0–100)**.

The system is designed as a **proof-of-concept** to demonstrate how modern NLP techniques can support large-scale candidate screening while reducing subjectivity and improving consistency.

---

## 🎓 Academic Context
- Team project initially developed by 3rd-year Computer Science students at **UKZN**.  
- **Course:** COMP316 – Machine Learning & Natural Language Processing  
- **Institution:** University of KwaZulu-Natal (UKZN)  
- **Level:** 3rd-Year Computer Science  
- **Contribution:** The original baseline was comprehensively reworked and enhanced, resulting in a substantially improved and independently developed implementation.
---


## 🎯 Project Objectives
The goal is to assist recruiters by providing:  
- ⚡ Fast and consistent scoring  
- 🎯 Reduced human bias  
- 📊 Objective evaluation across large applicant pools  

---

## ✨ Key Features

- 📝 Structured résumé preprocessing  
  *(Skills, Experience, Education, Certifications, Projects)*

- 🤗 Fine-tuned BERT regression model  
  *(bert-base-uncased configured for continuous prediction)*

- 📊 Robust evaluation metrics  
  - Root Mean Squared Error (RMSE)  
  - Mean Absolute Error (MAE)  
  - Coefficient of Determination (R²)

- ⚙️ Hugging Face Trainer API integration  
  - Early stopping  
  - Validation-based checkpointing  
  - Reproducible training pipeline

- 📈 Visual performance analysis  
  - Predicted vs actual score scatter plots  
  - Sample-wise prediction comparisons  

---

## 🧠 Methodology Overview

1. **Dataset Acquisition**  
   Résumé data is sourced from a publicly available Kaggle dataset.

2. **Text Construction**  
   Structured résumé fields are converted into a unified textual representation.

3. **Label Normalisation**  
   AI scores are normalised from 0–100 to 0–1 for stable regression training.

4. **Model Training**  
   A pre-trained BERT encoder is fine-tuned using supervised regression.

5. **Evaluation**  
   Performance is assessed on a held-out test set to ensure generalisation.

---

## 📊 Final Results (Test Set)


| Metric | Value |
|------|------|
| **RMSE** | ≈ 1.85 |
| **MAE** | ≈ 1.38 |
| **R²** | ≈ 0.993 |

- Performance is reported on a held-out test set. High accuracy is expected due to the structured and internally consistent nature of the dataset.
- An R² value of approximately 0.993 indicates that the model explains over **99% of the variance** in the target résumé scores.  
- The low validation and test losses confirm stable convergence and minimal overfitting, with model selection based on minimum validation loss rather than peak R².
---

## ⚙️ Requirements

- Python 3.8+
- PyTorch
- Hugging Face Transformers
- Pandas
- NumPy
- scikit-learn
- Jupyter Notebook / Google Colab

---

## ▶️ How to Run the Project  
1. Clone the repository  
2. Install dependencies:  
   ```bash
   pip install -r requirements.txt
3. Run the Jupyter notebook and execute cells sequentially.
   
GPU acceleration is strongly recommended for efficient training of the BERT model, although CPU execution remains fully supported and produces identical results.

---

## ⚠️ Disclaimer  
This project was developed **for educational purposes only**.  
No claim is madfe regarding ownership of datasets or pretrained models used.  

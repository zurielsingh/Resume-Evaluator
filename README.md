# Resume Scoring Using BERT-Based Regression

A fine-tuned transformer model for automated résumé evaluation — achieving **R² = 0.993** and **MAE ≈ 1.38** on a held-out test set of 1,000 résumés.

---

## Results

| Metric | Value |
|--------|-------|
| R² | **≈ 0.993** |
| MAE | ≈ 1.38 |
| RMSE | ≈ 1.85 |

> Model selection was based on minimum validation loss rather than peak R², ensuring genuine generalisation rather than overfitting to the test distribution.

---

## Overview

This project fine-tunes a **BERT-base-uncased** encoder with a single regression head to predict continuous résumé quality scores (0–100). Structured résumé attributes — Skills, Experience, Education, Certifications, and Projects — are converted into a unified natural language representation and passed through the transformer for end-to-end score prediction.

The system is designed to support large-scale candidate screening with consistent, bias-reduced evaluation. It substantially improves upon an original group baseline through reworked preprocessing, validation-based checkpointing, and full fine-tuning of the encoder.

---

## Visual Results

### Predicted vs Actual Résumé Scores

Strong linear alignment across the full score range with no systematic over- or underestimation.

![Predicted vs Actual](assets/predicted_vs_actual.png)

### Sample-wise Prediction Comparison (First 50 Test Samples)

Low error variance and stable generalisation across individual samples, consistent with the RMSE and MAE values reported.

![Sample-wise Comparison](assets/sample_prediction_comparison.png)

---

## Model Architecture

| Component | Specification |
|-----------|--------------|
| Base model | `bert-base-uncased` |
| Total parameters | ≈ 110 million |
| Encoder layers | 12 transformer layers |
| Hidden size | 768 dimensions |
| Attention heads | 12 per layer |
| Max sequence length | 256 tokens |
| Output layer | Single linear regression head |

BERT was selected over TF-IDF and bag-of-words baselines for its ability to capture semantic meaning rather than keyword frequency, eliminating manual feature engineering while learning representations and scoring jointly end-to-end.

---

## Training Configuration

| Parameter | Value |
|-----------|-------|
| Loss function | Mean Squared Error (MSE) |
| Optimiser | AdamW |
| Learning rate | 5 × 10⁻⁵ |
| Batch size | 8 |
| Checkpoint selection | Minimum validation loss |
| Regularisation | Gradient clipping + weight decay |
| Platform | Google Colab (NVIDIA Tesla T4) |

---

## Dataset

10,000 résumés from a publicly available Kaggle résumé screening dataset, split 80/10/10 across training, validation, and test sets with a fixed random seed for reproducibility.

Structured fields (Skills, Experience, Education, Certifications, Project count) are converted into a single templated natural language sequence per résumé. Target scores are normalised to [0, 1] for stable regression training and rescaled back to [0, 100] for evaluation and reporting.

---

## Inference Benchmarks

| Hardware | Inference Time | Throughput |
|----------|---------------|------------|
| GPU (Tesla T4) | ~50–80 ms/résumé | ~700–1,200 résumés/min |
| CPU (8-core) | ~200–300 ms/résumé | ~200–300 résumés/min |
| CPU (4-core) | ~400–500 ms/résumé | ~120–150 résumés/min |

GPU acceleration provides a **3–6× reduction in inference time**, with batch processing enabling further throughput gains for production-scale deployment.

---

## Requirements

- Python 3.8+
- PyTorch
- Hugging Face Transformers
- Pandas, NumPy, scikit-learn
- Jupyter Notebook / Google Colab

```bash
pip install -r requirements.txt
```

GPU acceleration is strongly recommended for training. CPU execution is fully supported and produces identical results.

---

## Running the Project

```bash
git clone https://github.com/zurielsingh/Resume-Ranking-Program.git
cd Resume-Ranking-Program
pip install -r requirements.txt
```

Open the Jupyter notebook and execute cells sequentially. Pre-trained checkpoint weights are included — skip the training cells to run inference directly.

---

## Academic Context

- **Course:** COMP316 – Machine Learning & Natural Language Processing
- **Institution:** University of KwaZulu-Natal (UKZN)
- **Contribution:** Original group baseline comprehensively reworked and independently extended — rearchitected preprocessing pipeline, full encoder fine-tuning, validation-based checkpointing, and early stopping implemented from scratch.

---

## Limitations

- Relies on structured input fields; free-form résumé PDFs are not directly supported
- Target labels are AI-generated and may carry inherent scoring biases
- Performance on out-of-distribution résumé formats (different industries, layouts) is untested
- Visual résumé features such as formatting and layout are not captured

---

## Acknowledgements

Dataset sourced from Kaggle. Pre-trained BERT weights from Hugging Face (`bert-base-uncased`).

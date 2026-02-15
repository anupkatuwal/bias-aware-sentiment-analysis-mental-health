# Bias-Aware Sentiment Analysis in Mental Health Texts

This repository contains the code, experiments, and documentation for my Master’s thesis:

**Title:** Addressing Biases in Sentiment Analysis Models Using Transfer Learning  
**Author:** Anup Katuwal  
**Degree:** Master of Computer Information Systems  
**Institution:** Nepal College of Information and Technology (NCIT), Pokhara University (PU)

---

## Abstract
This research investigates bias in sentiment analysis models applied to mental health texts from Reddit. We evaluate traditional LSTM models and transformer-based BERT models, and propose bias-mitigation strategies including counterfactual data augmentation and fairness-aware training.

---

## Repository Structure
- `notebooks/` – Google Colab / Jupyter notebooks for experiments
- `scripts/` – Training and evaluation scripts
- `data/` – Dataset metadata and statistics (no raw sensitive text)
- `results/` – Experimental results, tables, and figures
- `thesis/` – Thesis document and IEEE materials

---

## Dataset
Due to ethical considerations, raw mental health text data is **not shared publicly**.  
Please see `data/README.md` for dataset construction details and access instructions.

---

## Models
- BiLSTM + GloVe
- BERT (baseline)
- Fairness-aware BERT (CDA, adversarial debiasing)

---

## Fairness Metrics
- Demographic Parity Difference (DPD)
- Equalized Odds Difference (EOD)
- Bias Amplification

---

## Reproducibility
All experiments were conducted using Google Colab and are reproducible using the provided notebooks and scripts.

---

## License
This project is released for academic and research purposes.

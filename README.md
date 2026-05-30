# Bias Mitigation in Mental Health Sentiment Analysis using BERT with Fairness Techniques

> **Master's Thesis** — Nepal College of Information Technology (NCIT), Pokhara University, March 2026
>
> [![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
> [![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)](https://jupyter.org/)
> [![HuggingFace](https://img.shields.io/badge/🤗-Transformers-yellow)](https://huggingface.co/transformers/)
> [![License](https://img.shields.io/badge/License-Academic-green)](#license)
>
> ---
>
> ## 📌 Overview
>
> This repository contains the code, data, and documents for a Master's thesis that addresses **bias in sentiment analysis models applied to mental health text**. Bias here spans multiple dimensions — systemic biases inherited from large pre-training corpora, gender-based bias, and dialect-based bias. The work benchmarks three model architectures, quantifies bias across protected subgroups, and proposes a fairness-constrained model (FairBERT) that jointly optimises sentiment accuracy and demographic fairness.
>
> | Field | Details |
> |---|---|
> | **Title** | Bias Mitigation in Mental Health Sentiment Analysis using BERT with Fairness Techniques |
> | **Author** | Anup Katuwal (P.U. Reg: 2020-2-92-0022) |
> | **Degree** | Master of Computer Information System (MCIS) |
> | **Institution** | Nepal College of Information Technology (NCIT), Faculty of Management, Pokhara University, Nepal |
> | **Supervisor** | Prof. Dr. Roshan Chitrakar |
> | **Completed** | March 2026 |
>
> ---
>
> ## 🧠 Research Problem
>
> Sentiment analysis systems used in mental health contexts inherit systemic biases from large pre-training corpora and amplify them across gender and dialect subgroups. This thesis asks:
>
> 1. How large are gender-based and dialect-based performance gaps in standard sentiment classifiers applied to mental health social media posts?
> 2. 2. Can adversarial debiasing — jointly optimising a sentiment classifier and a demographic discriminator — significantly reduce these gaps?
>    3. 3. What trade-offs emerge between aggregate accuracy and subgroup-level fairness?
>      
>       4. ---
>      
>       5. ## 🗂️ Repository Structure
>      
>       6. ```
> bias-aware-sentiment-analysis-mental-health/
> │
> ├── notebooks/
> │   ├── RedditPostsScraping.ipynb     # Data collection pipeline via Reddit API (PRAW)
> │   └── ThesisComplete.ipynb          # End-to-end pipeline: training, evaluation, fairness analysis
> │
> ├── datasets/
> │   ├── RMH-Bias-10K.csv              # 10,000 Reddit mental health posts (raw)
> │   └── RMH-Bias-10K-Annotated.xlsx   # Annotated dataset with sentiment + bias metadata labels
> │
> ├── Thesis/
> │   ├── FinalPrints.pdf               # Full thesis document
> │   ├── IEEE_Paper_Katuwal_Final.pdf  # IEEE-format conference paper
> │   └── MidtermRedo.docx              # Midterm thesis draft
> │
> └── README.md
> ```
>
> ---
>
> ## 📊 Dataset: RMH-Bias-10K
>
> A purpose-built dataset of **10,000 Reddit posts** scraped from mental health subreddits, stratified by **gender and dialect subgroups**. Annotation was conducted via a two-stage pipeline (manual + VADER-assisted) with inter-annotator agreement measured by Cohen's Kappa (κ = 0.88) on a 500-post validation subset.
>
> | Property | Value |
> |---|---|
> | Size | 10,000 posts |
> | Source | Reddit mental health subreddits (via PRAW) |
> | Sentiment Labels | Positive / Negative / Neutral |
> | Protected Attributes | Gender, Dialect |
> | Annotation | Two-stage (manual + VADER-assisted), κ = 0.88 |
> | Format | CSV (raw) + XLSX (annotated with bias metadata) |
>
> > **Ethical Note:** Posts contain sensitive mental health disclosures. This data is shared strictly for research reproducibility. Handle in compliance with Reddit's Terms of Service and your institution's ethics guidelines.
>
> ---
>
> ## 🤖 Models
>
> | ID | Model | Architecture | Key Components |
> |---|---|---|---|
> | M1 | BiLSTM | Bidirectional LSTM + Attention | GloVe (300d) embeddings, Focal Loss |
> | M2 | Vanilla BERT | Transformer (12-layer, bert-base-uncased) | Fine-tuned classification head |
> | M3 | **FairBERT** *(proposed)* | BERT + Adversarial Head | Adversarial debiasing + Counterfactual Data Augmentation (CDA) + Focal Loss |
>
> **FairBERT (M3)** jointly optimises a sentiment classifier and a demographic discriminator. A gradient reversal layer penalises the model whenever its internal representations retain demographic information, encouraging group-invariant features.
>
> ---
>
> ## ⚖️ Fairness Metrics
>
> The following group fairness metrics are evaluated across gender and dialect splits:
>
> | Metric | Description |
> |---|---|
> | **DPD** — Demographic Parity Difference | Gap in positive prediction rates between groups |
> | **EOD-TPR** — Equalized Odds (TPR gap) | Difference in true positive rates across groups |
> | **EOD-FPR** — Equalized Odds (FPR gap) | Difference in false positive rates across groups |
> | **APG** — Accuracy Parity Gap | Difference in per-group classification accuracy |
>
> ---
>
> ## 🔬 Key Findings
>
> - **M3 (FairBERT) outperforms M1 by 10.3 pp and M2 by 4.5 pp** in overall accuracy.
> - M3 reduces mean DPD by **35.4 pp** and mean equalized odds gap by **22.9 pp** relative to M2.
> - Despite gains, a **9.5% regression in dialect-based equalized odds** persists, showing higher aggregate fairness does not resolve all subgroup error-rate disparities.
> - A notable **FPR disparity** remains for female users (FPR = 0.26 vs. 0.14 for male users), demonstrating that demographic parity and error-rate parity are not equivalent objectives.
> - Results empirically support the **impossibility theorems of algorithmic fairness**: simultaneous satisfaction of all fairness criteria is not achievable, and subgroup-level analysis is essential for safe clinical deployment.
>
> ---
>
> ## 🚀 Getting Started
>
> ### Prerequisites
>
> ```bash
> pip install transformers datasets torch scikit-learn pandas numpy openpyxl praw
> ```
>
> ### Run the Experiments
>
> 1. **Data Collection** (optional — dataset already provided):
> 2.    Open `notebooks/RedditPostsScraping.ipynb` and configure your Reddit API credentials (PRAW).
>
> 3.2. **Full Experiment Pipeline**:
>    Open `notebooks/ThesisComplete.ipynb` in Google Colab or Jupyter.
>    - Loads and preprocesses `datasets/RMH-Bias-10K-Annotated.xlsx`
>    -    - Applies Counterfactual Data Augmentation (CDA)
>         -    - Trains M1 (BiLSTM), M2 (BERT), and M3 (FairBERT)
>              -    - Evaluates accuracy, fairness metrics (DPD, EOD-TPR, EOD-FPR, APG), and ROC curves
>                   -    - Runs cross-seed stability analysis (5-seed protocol)
>                    
>                        - > Experiments were originally run on **Google Colab** (T4 GPU). A GPU runtime is strongly recommended.
>                          >
>                          > ---
>                          >
>                          > ## 📄 Publications & Documents
>                          >
>                          > | Document | Description |
>                          > |---|---|
>                          > | [`Thesis/FinalPrints.pdf`](Thesis/FinalPrints.pdf) | Complete master's thesis |
>                          > | [`Thesis/IEEE_Paper_Katuwal_Final.pdf`](Thesis/IEEE_Paper_Katuwal_Final.pdf) | IEEE-format conference paper |
>                          >
>                          > ---
>                          >
>                          > ## 📚 Citation
>                          >
>                          > ```bibtex
>                          > @mastersthesis{katuwal2026biasmentalhealthsentiment,
>                          >   author    = {Anup Katuwal},
>                          >   title     = {Bias Mitigation in Mental Health Sentiment Analysis using BERT with Fairness Techniques},
>                          >   school    = {Nepal College of Information Technology (NCIT), Pokhara University},
>                          >   year      = {2026},
>                          >   month     = {March},
>                          >   type      = {Master's Thesis (MCIS)}
>                          > }
>                          > ```
>                          >
>                          > ---
>                          >
>                          > ## 📝 License
>                          >
>                          > Released for **academic and research purposes only**. Dataset content is scraped from Reddit — redistribution must comply with Reddit's Terms of Service. Model code is available under the MIT License.
>                          >
>                          > ---
>                          >
>                          > ## 🙏 Acknowledgements
>                          >
>                          > - **Supervisor:** Prof. Dr. Roshan Chitrakar, NCIT / Pokhara University
>                          > - - **Program Coordinator:** Mr. Saroj Shakya
>                          >   - - **Principal, NCIT:** Mr. Niranjan Khakurel
>                          >     - - The open-source mental health communities on Reddit whose posts made this research possible
>                          >       - - HuggingFace Transformers, PRAW, and Google Colab

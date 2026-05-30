# Bias-Aware Sentiment Analysis in Mental Health Texts

> **Master's Thesis** — Nepal College of Information and Technology (NCIT), Pokhara University
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
> This repository accompanies a Master's thesis investigating **demographic bias in sentiment analysis models** applied to mental health discourse on Reddit. The work benchmarks classical and transformer-based NLP models, quantifies bias across demographic groups, and proposes fairness-aware mitigation strategies.
>
> | Field | Details |
> |---|---|
> | **Title** | Bias Mitigation in Sentiment Analysis Using BERT with Fairness Techniques |
> | **Author** | Anup Katuwal |
> | **Degree** | Master of Computer Information Systems (MCIS) |
> | **Institution** | Nepal College of Information and Technology (NCIT), Pokhara University (PU) |
>
> ---
>
> ## 🧠 Research Problem
>
> Sentiment analysis systems deployed in mental health contexts can systematically produce different accuracy levels across demographic groups — amplifying existing inequities in healthcare AI. This thesis asks:
>
> 1. **How much bias** exists in standard sentiment classifiers applied to Reddit mental health posts?
> 2. 2. **Which fairness interventions** (data-level vs. training-level) most effectively reduce bias without sacrificing accuracy?
>    3. 3. **Does BERT's contextual understanding** offer a fairness advantage over BiLSTM baselines?
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
> │   └── ThesisComplete.ipynb          # End-to-end experiments: training, evaluation, fairness analysis
> │
> ├── datasets/
> │   ├── RMH-Bias-10K.csv              # 10,000 Reddit mental health posts (raw)
> │   └── RMH-Bias-10K-Annotated.xlsx   # Annotated dataset with sentiment + demographic labels
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
> A custom dataset of **10,000 Reddit posts** scraped from mental health subreddits (e.g., r/depression, r/anxiety, r/mentalhealth).
>
> | Property | Value |
> |---|---|
> | Size | 10,000 posts |
> | Source | Reddit (via PRAW) |
> | Sentiment Labels | Positive / Negative / Neutral |
> | Demographic Attributes | Gender-coded language markers, identity terms |
> | Format | CSV (raw) + XLSX (annotated) |
>
> > **Ethical Note:** Raw post text may contain sensitive mental health disclosures. The dataset is included strictly for research reproducibility. Please handle it responsibly and in compliance with Reddit's data usage policies and your institution's IRB guidelines.
>
> ---
>
> ## 🤖 Models
>
> ### Baseline
> | Model | Architecture | Embeddings |
> |---|---|---|
> | BiLSTM | Bidirectional LSTM | GloVe (300d) |
> | BERT-base | Transformer (12-layer) | Contextual (bert-base-uncased) |
>
> ### Fairness-Aware (Proposed)
> | Model | Mitigation Strategy | Type |
> |---|---|---|
> | BERT + CDA | Counterfactual Data Augmentation | Data-level |
> | BERT + Adversarial | Adversarial debiasing head | Training-level |
>
> ---
>
> ## ⚖️ Fairness Metrics
>
> The following group fairness metrics are computed across demographic splits:
>
> - **Demographic Parity Difference (DPD)** — gap in positive prediction rates between groups
> - **Equalized Odds Difference (EOD)** — gap in true/false positive rates across groups
> - **Bias Amplification** — degree to which model predictions exaggerate dataset-level skew
>
> ---
>
> ## 🚀 Getting Started
>
> ### Prerequisites
>
> ```bash
> pip install transformers datasets torch scikit-learn pandas numpy openpyxl
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
>    -    - Trains BiLSTM and BERT models
>         -    - Applies CDA and adversarial debiasing
>              -    - Computes accuracy + fairness metrics
>                   -    - Generates results tables and plots
>                    
>                        - > All experiments were originally run on **Google Colab** (GPU runtime). A T4 or higher GPU is recommended.
>                          >
>                          > ---
>                          >
>                          > ## 📄 Publications & Documents
>                          >
>                          > | Document | Description |
>                          > |---|---|
>                          > | [`Thesis/FinalPrints.pdf`](Thesis/FinalPrints.pdf) | Complete master's thesis |
>                          > | [`Thesis/IEEE_Paper_Katuwal_Final.pdf`](Thesis/IEEE_Paper_Katuwal_Final.pdf) | IEEE-format paper derived from the thesis |
>                          >
>                          > ---
>                          >
>                          > ## 🔬 Key Findings
>                          >
>                          > - Standard BERT exhibits measurable demographic bias on mental health text, even outperforming BiLSTM in accuracy.
>                          > - - **Counterfactual Data Augmentation (CDA)** reduces DPD and EOD with minimal accuracy loss.
>                          >   - - **Adversarial debiasing** provides stronger fairness guarantees but requires careful regularization to avoid performance degradation.
>                          >     - - Bias in mental health NLP is not eliminated by scale alone — fairness-aware design is essential.
>                          >      
>                          >       - ---
>                          >
>                          > ## 📚 Citation
>                          >
>                          > If you use this work or dataset, please cite:
>                          >
>                          > ```bibtex
>                          > @mastersthesis{katuwal2024biassentiment,
>                          >   author    = {Anup Katuwal},
>                          >   title     = {Bias Mitigation in Sentiment Analysis Using BERT with Fairness Techniques on Mental Health Texts},
>                          >   school    = {Nepal College of Information and Technology (NCIT), Pokhara University},
>                          >   year      = {2024},
>                          >   type      = {Master's Thesis}
>                          > }
>                          > ```
>                          >
>                          > ---
>                          >
>                          > ## 📝 License
>                          >
>                          > This project is released for **academic and research purposes only**. The dataset contains scraped Reddit content — redistribution must comply with Reddit's Terms of Service. Model code is available under the MIT License.
>                          >
>                          > ---
>                          >
>                          > ## 🙏 Acknowledgements
>                          >
>                          > - Pokhara University & NCIT faculty supervisors
>                          > - - The open-source mental health communities on Reddit whose posts made this research possible
>                          >   - - HuggingFace Transformers library
>                          >     - - Google Colab for compute resources

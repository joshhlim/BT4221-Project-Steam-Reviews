# BT4221 Project – Steam Review Recommendation Analysis

## Team
- **Chong Ke Lin, Mark** – `A0252467Y`
- **Koh Ken Tze** – `A0251805J`
- **Josh Lim** – `A0251991X`
- **Goh Kian Hwee Justin** – `A0249540A`

---

## Project Video
Project video link: [Insert video link here](https://drive.google.com/file/d/13JlNaGvBtZ11jA7fisFkSoK1N2QucuJN/view?usp=sharing)

---

## Overview
This project studies **what drives a Steam review to recommend or not recommend a game**. Rather than treating the task only as a prediction problem, the project focuses on **feature importance and interpretability**. We combine review-level, user-level, app-level, and text-derived features to understand which signals matter most in recommendation behaviour.

The repository is organised around two main pipelines:

- **Manual pipeline**: the primary notebook for the project, containing the full end-to-end workflow, modelling, interpretation, and report-aligned analysis.
- **Agentic pipeline**: a parallel pipeline exploring how an LLM-assisted agent workflow compares against a manually designed pipeline for the same project setting.

A separate **semantic feature experiment** is also included as an exploratory follow-up study.

---

## Project Objective
The central question of this project is:

> **Which features most strongly influence whether a Steam review is recommended?**

To answer this, we model recommendation behaviour using engineered structured features and text representations, then compare how different modelling approaches prioritise these signals.

Key themes investigated include:

- reviewer engagement and behaviour
- playtime-related effects
- app-level context
- early access and free-copy effects
- text-derived signals from review content
- differences between manual and agentic analytical workflows

---

## Repository Structure

```text
.
├── 01_manual_pipeline.ipynb          # Main notebook to read first
├── 02_agentic_pipeline.ipynb         # Agent-based pipeline for comparison
├── agent_decisions.json              # Saved agent reasoning / decision outputs
├── evaluation_report.json            # Evaluation summary for agent pipeline
├── requirements.txt                  # Python dependencies
├── eda_plots/                        # Exported EDA and reporting plots
├── data/
│   ├── cleaned_steam_reviews.csv     # Main cleaned dataset
│   └── semantic_feature_cache/       # Cached outputs for semantic experiment
└── README.md
```

### Recommended reading order
1. **`01_manual_pipeline.ipynb`** – primary project notebook and main submission flow
2. **`02_agentic_pipeline.ipynb`** – agent-based extension and comparison
3. Semantic feature outputs in **`data/semantic_feature_cache/`** – exploratory follow-up experiment

---

## Notebook Guide

### 1) `01_manual_pipeline.ipynb`
This is the **main notebook** for the project and should be read first.

It includes:
- data loading and preprocessing
- exploratory data analysis
- feature engineering
- PySpark-based transformations and modelling workflow
- model training and validation
- feature importance analysis
- interpretation of results
- semantic follow-up experiment
- Spark-specific optimisation choices and distributed processing considerations

This notebook represents the team’s **manual design decisions**, where each modelling and engineering step was deliberately chosen and justified.

### 2) `02_agentic_pipeline.ipynb`
This notebook explores an **agent-assisted approach** to the same project.

It is included to evaluate:
- how an LLM-guided pipeline differs from the manual workflow
- where agentic decision-making adds value
- where manual judgement remains stronger
- how the resulting pipeline compares in structure, transparency, and outcomes

This notebook should be treated as a **comparison notebook**, not as a replacement for the manual pipeline.

---

## Methodology Summary

### Data
The project uses a cleaned Steam review dataset containing:
- review text
- binary recommendation label
- reviewer metadata
- app/game identifiers
- playtime-related variables
- voting and engagement metrics
- contextual indicators such as free-copy and early-access flags

### Feature groups
Features used in the project broadly include:

- **Review-level engagement features**
  - helpful votes
  - funny votes
  - comment count
  - weighted vote score

- **Reviewer behaviour features**
  - playtime forever
  - playtime at review
  - playtime in the last two weeks
  - number of games owned
  - number of reviews written

- **App-level contextual features**
  - app aggregates and contextual statistics
  - behavioural ratios and app-normalised signals

- **Text features**
  - TF-IDF representations in the main pipeline
  - interpretable semantic indicator features in the follow-up experiment

### Models
The project primarily uses:
- **Logistic Regression** for interpretability through coefficients
- **Random Forest** for nonlinear feature importance analysis

These models are compared to examine both predictive performance and interpretive consistency.

---

## Semantic Follow-Up Experiment
A follow-up experiment is included to test whether **compact, interpretable semantic features** extracted from review text can add analytical value beyond standard engineered features.

Instead of using the language model to predict sentiment directly, the semantic experiment detects whether a review discusses concrete dimensions such as:
- bugs or technical issues
- gameplay
- difficulty
- repetition or grind
- value for money
- immersion
- frustration

The purpose of this experiment is to preserve interpretability while avoiding direct target leakage.

Cached semantic outputs are stored under:

```text
data/semantic_feature_cache/
```

---

## Spark and Distributed Processing
This project was built with an emphasis on **big-data workflow design using PySpark**.

Examples of Spark-related considerations in the notebooks include:
- distributed preprocessing with Spark DataFrames
- partition-aware transformations
- caching and persistence decisions
- efficient aggregation and feature construction
- scalable model preparation pipelines
- reruns incorporating stronger Spark mastery and optimisation choices

The goal was not only to build accurate models, but also to demonstrate sound use of distributed data processing techniques in a realistic analytics pipeline.

---

## How to Run

### 1) Create and activate a virtual environment
```bash
python -m venv venv
source venv/bin/activate
```

On Windows:
```bash
venv\Scripts\activate
```

### 2) Install dependencies
```bash
pip install -r requirements.txt
```

### 3) Download and place the dataset
Download the cleaned dataset from the link below and save it into the `data` folder:

[Insert cleaned dataset download link here](https://your-dataset-link-here)

After downloading, save the file as:

```text
data/cleaned_steam_reviews.csv
```

If the `data/` folder does not exist yet, create it first.

If you plan to rerun the semantic follow-up experiment, keep the cache directory available:

```text
data/semantic_feature_cache/
```

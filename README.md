# Sentiment Analysis

A comprehensive pipeline for binary sentiment classification of user-generated text. This project demonstrates data ingestion, exploratory analysis, text preprocessing, model training, evaluation, and deployment-ready artefacts.  

---

## Table of Contents

1. [Project Overview](#project-overview)  
2. [Dataset](#dataset)  
3. [Data Preprocessing](#data-preprocessing)  
4. [Model Development](#model-development)
6. [Directory Structure](#directory-structure)  
7. [Contributing](#contributing)  
8. [Licence](#licence)  

---

## Project Overview

Sentiment analysis entails automatically detecting the emotional polarity (positive or negative) expressed in text. This repository provides:

- A Jupyter Notebook (`Sentiment_Analysis.ipynb`) illustrating a full workflow  
- A trained TF‑IDF + Logistic Regression model with optional hyperparameter tuning  
- An advanced rule‑based override layer for handling violent or toxic language  
- Scripts to save and load the final model for inference  

---

## Dataset

We employ a publicly available collection of labelled tweets (commonly known as the Sentiment140 dataset). It originally contains six columns without meaningful headers. For consistency and clarity during model training, we renamed them as follows:

| Original Column Index | Renamed Column       | Description                            |
|-----------------------|----------------------|----------------------------------------|
| 0                     | `sentiment`          | 0 = negative, 4 = positive             |
| 1                     | `id`                 | Unique tweet identifier                |
| 2                     | `date`               | Timestamp of the tweet                 |
| 3                     | `query`              | Search query (unused)                  |
| 4                     | `user`               | Tweet author’s username                |
| 5                     | `review`             | Raw tweet text used for sentiment      |

Download the dataset from the link below:

[Download the dataset](https://www.kaggle.com/datasets/kazanova/sentiment140?select=training.1600000.processed.noemoticon.csv)

---

## Data Preprocessing

1. **Load & Inspect**  
   - Load CSV with `header=None`  
   - Assign consistent column names as above  
2. **Exploratory Data Analysis**  
   - Examine class distribution  
   - Identify missing values (none expected)  
3. **Text Cleaning**  
   - Remove non‑alphabetical characters  
   - Convert to lowercase  
   - Tokenise and remove English stopwords  
   - Lemmatise tokens using `WordNetLemmatizer`  
   - Store cleaned text in `cleaned_review`  

---

## Model Development

### 1. Train–Test Split  
- 80/20 stratified split to preserve class proportions  

### 2. Baseline Pipeline  
- **Vectorisation**: `TfidfVectorizer(max_features=5000)`  
- **Classifier**: `LogisticRegression(solver='liblinear')`  

### 3. Evaluation  
- Metrics: Accuracy, Precision, Recall, F1‑score  
- Confusion matrix visualisation  

### 4. Hyperparameter Tuning (Optional)  
- Grid search over `max_features` and regularisation strength `C`  

### 5. Rule‑Based Override Layer  
- Extensive negative & positive lexicons  
- Lemma‑based detection of violent or toxic phrases  
- Overrides model output to “Negative” when strong negative signals are present  

### 6. Model Serialization  
- Save final artefact as `sentiment_analysis_model.joblib` for downstream deployment  

---

## Directory Structure

```
├── Sentiment_Analysis.ipynb
├── sentiment_analysis_model.joblib
├── requirements.txt
├── README.md
└── data
    └── sentiment_analysis_dataset.csv
```

---

## Contributing

Contributions, issues and feature requests are welcome! Please ensure any pull requests:

* Adhere to existing code style
* Include appropriate tests or examples
* Update this README or the notebook documentation as needed

---

## Licence

This project is licensed under the MIT Licence. See [LICENSE](LICENSE) for details.

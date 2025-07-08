# Gendered Abuse Detection in Indic Languages

## Project Overview

This project, conducted by *Group-46* (*Shubhham Pundhir* - MT24I6, *Somshekar M* - MT24157, *Varun Gambhir* - MT24159), focuses on detecting gendered abuse in social media posts written in *Hindi, **Tamil, and **Indian English. The goal is to classify posts into **abusive (1)* or *non-abusive (0)* categories, with a particular emphasis on identifying abuse directed at marginalized gender identities, sexual orientations, or gender expressions. This classification task is critical for online content moderation, especially in the Indian socio-cultural context where multilingual and code-mixed content is prevalent.

The project introduces a novel dataset and evaluates various machine learning models, including single-task and multi-task classification approaches, to detect gendered abuse. The dataset is annotated by *18 domain experts* and includes approximately *7.6k English, **7.7k Hindi, and **7.3k Tamil* posts, labeled based on three questions:

- *Q1*: Gendered abuse not directed at marginalized groups.
- *Q2*: Gendered abuse directed at marginalized groups.
- *Q3*: Explicitness of the abuse.

### 🏆 Achievement
This project has *surpassed the ICON 2023 Shared Task benchmark* for gendered abuse detection in Indic languages, demonstrating superior performance across all evaluated languages and tasks.

## Dataset Description

The dataset is structured with predefined train/test splits, provided as separate CSV files for each language and label. The files follow the naming conventions:

- *Training Data*: train_[language]_[label]_[run].csv (e.g., train_en_l1.csv, train_hi_l2.csv)
- *Test Data*: test_[language]_[label]_[run].csv (e.g., test_en_l1.csv, test_ta_l3.csv)

Each file contains columns for:

- *Id*: Unique identifier for the post
- *Text*: The content of the post
- *Language*: The language of the post (English, Hindi, or Tamil)
- *Annotation Scores*: Labels corresponding to Q1, Q2, or Q3 (e.g., 1 for yes, 0 for no)

The dataset was annotated by language-specific experts to ensure cultural and linguistic accuracy.

## Methodology

### Text Preprocessing

Minimal preprocessing was applied to preserve linguistic context:

- Removal of URLs to eliminate non-semantic content
- Removal or replacement of generic placeholders (e.g., @user, #hashtag)

### Baseline Approach

A baseline was established using the *Gemini LLM*, which showed varying performance across languages:

- *Tamil*: Best performance, particularly for detecting explicit/aggressive content
- *English*: Struggled with subtle or implicit abuse, especially in code-mixed or culturally specific contexts
- *Hindi*: Moderate performance, with challenges in handling code-mixed content

### Task 1: Single-Task Classification

This task evaluated models trained independently for Q1, Q2, and Q3 across the three languages. Key points:

- *Objective*: Assess model performance on individual classification tasks
- *Class Imbalance*: Addressed through downsampling, particularly for English data, to balance the dataset and improve model performance on minority classes
- *Models*:
  - Logistic Regression
  - Support Vector Machine (SVM) with Sentence Transformer features
  - Bi-directional LSTM (B4I-STVM)
  - LSTM-RNN-GRU (Series model)
- *Evaluation Metric*: Macro-F1 score

### Task 3: Multi-Task Classification (Joint Q1 & Q2)

This task explored multi-task learning (MTL) to predict Q1 and Q2 simultaneously, aiming to capture shared features and improve generalization. Key points:

- *Objective*: Build classifiers for joint prediction of Q1 (abuse without target) and Q2 (abuse with target)
- *Class Imbalance*: Handled via downsampling, especially for English, to ensure balanced training data for both tasks
- *Models*:
  - Logistic Regression (adapted for multi-output)
  - SVM with Sentence Transformer features (adapted for multi-task)
  - Bi-directional LSTM (B4I-STVM) with a multi-output layer
  - LSTM-RNN-GRU (Series model) with a multi-output final layer
- *Framework*: Models were fine-tuned using the HuggingFace Transformers framework (for Sentence Transformer and neural models) with consistent hyperparameters (learning rate, batch size, epoch count)
- *Evaluation Metric*: Macro-F1 score for joint Q1 and Q2 predictions

## Results

### Baseline (Gemini LLM)

- *Tamil: Achieved the highest macro-F1 score of **0.82* for Q3 (explicitness), excelling in detecting explicit/aggressive content
- *English: Lower performance, with a macro-F1 score of **0.65* for Q1, struggling with subtle or code-mixed abuse
- *Hindi: Moderate performance, with a macro-F1 score of **0.70* for Q2, limited by code-mixed content challenges

### Task 1: Single-Task Classification

#### English:
- *Q1 (Abuse, No Target): SVM with Sentence Transformer features achieved the best macro-F1 score of **0.70*, benefiting from robust text embeddings and downsampling
- *Q2 (Abuse, With Target): Logistic Regression performed best with a macro-F1 score of **0.66*
- *Q3 (Explicitness): LSTM-RNN-GRU model scored highest with a macro-F1 score of **0.70*

#### Hindi:
- *Q1: Bi-directional LSTM led with a macro-F1 score of **0.72*
- *Q2: LSTM-RNN-GRU achieved the best macro-F1 score of **0.74*
- *Q3: Bi-directional LSTM scored highest with a macro-F1 score of **0.76*

#### Tamil:
- *Q1: LSTM-RNN-GRU performed best with a macro-F1 score of **0.80*
- *Q2: Bi-directional LSTM achieved the highest macro-F1 score of **0.82*
- *Q3: Bi-directional LSTM led with a macro-F1 score of **0.85*

### Task 3: Multi-Task Classification (Joint Q1 & Q2)

- *English: SVM with Sentence Transformer features achieved the best joint macro-F1 score of **0.69* for Q1 and Q2 combined, leveraging downsampling and robust embeddings
- *Hindi: LSTM-RNN-GRU model performed best with a joint macro-F1 score of **0.73*
- *Tamil: Bi-directional LSTM led with a joint macro-F1 score of **0.80*, benefiting from shared feature learning and downsampling

## References

- A Survey on Automatic Online Hate Speech Detection in Low-Resource Languages (Amur Aora et al.)
- Mazumder et al., 2024
- Singh et al., 2024
- Vlegir et al., 2024

## License

This project is licensed under the *MIT License*. See the LICENSE file for details.

---

*Team Members:*
- Shubhham Pundhir (MT24I6)
- Somshekar M (MT24157)
- Varun Gambhir (MT24159)

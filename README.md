# AI for Cyber Security: Online Grooming Detection

## Overview

This project develops a machine learning pipeline to identify likely online grooming pairs using the PASYDA synthetic metadata dataset. Unlike traditional content-based approaches, the system relies solely on communication metadata, including message source, destination, timestamp, and length.

## Dataset

* **Dataset:** PASYDA Synthetic Metadata Dataset
* **Scenarios:** 10 scenarios across 5 dataset folders
* **Candidate Pairs:** 11 per scenario
* **Total Samples:** 110 pair-level records

  * 10 positive grooming pairs
  * 100 negative pairs

The project uses **pair-level classification**, where each central-node/contact-node pair represents a single supervised sample.

## Features

Behavioral features were engineered from raw communication metadata, including:

* Message volume and reciprocity
* Communication timing patterns
* Message length statistics
* Scenario-relative rankings and z-scores
* Temporal sequence behaviour

## Models Evaluated

* Random Forest (RF)
* Support Vector Machine (SVM)
* Multilayer Perceptron (MLP)

Two heuristic baselines were also tested for comparison.

## Evaluation

A leakage-safe **grouped 5-fold cross-validation** strategy was used, holding out one complete dataset folder per fold.

Metrics:

* Top-1 Accuracy
* Mean Reciprocal Rank (MRR)
* Precision, Recall, F1 Score
* ROC-AUC
* PR-AUC

## Results

| Model         | Top-1 Accuracy | MRR  |
| ------------- | -------------- | ---- |
| Random Forest | 1.00           | 1.00 |
| SVM           | 1.00           | 1.00 |
| MLP           | 1.00           | 1.00 |

A simple baseline using the **lowest average message length** also achieved perfect performance, highlighting a strong synthetic signal within the dataset.

## Key Findings

* Full-feature RF, SVM, and MLP models achieved perfect detection performance on PASYDA.
* Message length appears to be a dominant predictive feature.
* Ablation experiments showed reduced performance for RF and MLP when length-based features were removed.
* SVM remained robust even without message-length information.

## Limitations

* Small dataset with only 10 positive samples.
* Synthetic data may contain artefacts not present in real-world grooming behaviour.
* No message content, account information, or platform context is available.

## Future Work

* Evaluate on larger and real-world datasets.
* Incorporate richer privacy-preserving metadata.
* Explore longitudinal behavioural patterns.
* Use the system as a decision-support and triage tool rather than an automated decision-maker.

## Technologies

* Python
* Pandas
* Scikit-learn
* NumPy
* Matplotlib
* Seaborn

## Disclaimer

This project is intended for academic research purposes. Any real-world deployment should include human review and additional validation before operational use.

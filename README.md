# SHFSF-Earthquake-Severity
Interpretable and Efficient Earthquake Severity Classification via a Systematic Hybrid Feature-Selection Framework (SHFSF)

# Overview
This repository contains the complete, reproducible machine learning pipeline for the Systematic Hybrid Feature-Selection Framework (SHFSF). The framework integrates filter, wrapper, and embedded evaluators into a consensus-based ranking system to identify a compact, physically interpretable subset of seismic features for earthquake severity classification.
This codebase is designed for strict deterministic reproducibility, allowing independent researchers and reviewers to verify all baseline comparisons, hyperparameter grids, sensitivity analyses, and ablation studies presented in the manuscript.

# Repository Structure
The workflow is broken down into seven sequential Jupyter Notebooks to ensure transparency at every stage of the pipeline:
•	01_SHFSF_Dataset_Harmonization.ipynb Contains the preprocessing pipeline, including missing value imputation, standard scaling, and categorical encoding. (Note: To prevent data leakage, all scaling parameters are fitted exclusively on the training set).
•	02_SHFSF_Hyperparameter_Grid_Search.ipynb Executes a Stratified K-Fold grid search across seven classical ML models (LR, DT, RF, SVM, KNN, AdaBoost, XGBoost) to establish optimal configurations.
•	03_SHFSF_Final_Evaluation_and_Confusion_Matrices.ipynb Evaluates the top-performing models using exclusively the 6-feature SHFSF subset. Generates the comprehensive confusion matrices (corresponding to Figure 4).
•	04_Baseline_Full_Feature_Set.ipynb Evaluates the proxy classifier on the full 16-dimensional feature set for comparative benchmarking (corresponding to Table 2).
•	05_Baseline_PCA_vs_SHFSF.ipynb Evaluates the proxy classifier using a 9-component PCA reduction (preserving 95% variance) to demonstrate the loss of severe-class recall when physical semantics are destroyed (corresponding to Table 2).
•	06_SHFSF_Sensitivity_Analysis.ipynb Tests the framework under various non-equal aggregation weights (Filter-dominant, Wrapper-dominant, Embedded-dominant) to justify the equal-consensus configuration (corresponding to Table 5).
•	07_SHFSF_LOFO_Ablation.ipynb Performs a Leave-One-Feature-Out (LOFO) ablation study to quantify the complementary importance of contextual features like Azimuthal Gap and Depth (corresponding to Figure 5).

# Statement on Reproducibility
To ensure absolute deterministic reproducibility across different machines, the following protocols are strictly enforced throughout this codebase:
1.	Global Random Seed: A fixed random seed (random_state = 42) is utilized in all train-test splits, cross-validation folds, and stochastic classifier initializations (e.g., Random Forest, XGBoost).
2.	No Data Leakage: All feature scaling (StandardScaler) and dimensionality reduction (PCA) instances are fitted strictly on the X_train partitions prior to transforming the X_test partitions.
3.	Macro-Averaged Minority Recall: The custom metric "Aggregate Severe-Class Recall" (evaluating 'Strong' and 'Major' classes) is explicitly computed using a manual macro-averaging array to ensure complete transparency.

# Environment Setup
To run these notebooks locally, ensure you have Python 3.9+ installed. You can install the required dependencies using the following command:
Bash
pip install pandas numpy scikit-learn matplotlib seaborn jupyter

# Data Availability
The harmonized and pre-processed dataset required to execute the machine learning models (My dataset with class and without missing values.csv) is included directly in the root directory of this repository for immediate reproducibility.
The original, un-harmonized raw seismic dataset prior to the preprocessing (original_dataset.csv) is included directly in the root directory of this repository for immediate reproducibility.

# License
This repository and its contents are currently provided exclusively for academic peer-review purposes associated with the submission to KSII Transactions on Internet and Information Systems. All rights are reserved by the authors. No license is granted for commercial use, external distribution, or the creation of derivative works without explicit written permission from the authors.

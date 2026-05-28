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
The original multi-source raw seismic data utilized in this study can be accessed via the public repositories listed in the manuscript (e.g., USGS, NCS).
To execute notebooks 02 through 07, ensure the harmonized and preprocessed dataset CSV (generated in step 01) is placed in the root directory. (Note: If you are a reviewer requesting the exact pre-compiled D4 CSV, please refer to the Data Availability Statement in the manuscript for access instructions).

# License
This project is licensed under the MIT License - see the LICENSE file for details. This permissive license allows for the reproduction, modification, and academic integration of this code, provided proper citation is given to the original authors.

# IBM HR Attrition Prediction  
**IBM 员工离职预测项目（Machine Learning）**

---

## 📌 Project Overview | 项目简介

This project builds a machine learning pipeline to predict employee attrition using the IBM HR Analytics dataset.  
The goal is to identify employees who are likely to leave and analyze key factors associated with attrition.

本项目基于 IBM HR 数据集，构建完整的机器学习流程，用于预测员工是否离职，并分析影响离职的关键因素。

---

## 📂 Dataset | 数据集

- Source: IBM HR Employee Attrition Dataset  
- File: `WA_Fn-UseC_-HR-Employee-Attrition.csv`  
- Task Type: **Binary Classification**

---

## ⚙️ Methodology | 方法流程

### 1. Data Processing | 数据处理
- Remove ID / constant columns (e.g., `EmployeeNumber`, `EmployeeCount`, `Over18`, `StandardHours`)
- Handle missing values using median / most frequent imputation
- Apply one-hot encoding with `drop='if_binary'` for cleaner interpretation

### 2. Data Split | 数据划分
- Fixed **train_val / test split**
- Test set is strictly held out and never used during model selection

### 3. Model Candidates | 模型候选
- Dummy baseline
- Logistic Regression (unweighted / balanced)
- Random Forest
- XGBoost (if available)

### 4. Model Selection | 模型选择策略
- Based on **OOF (out-of-fold) predictions**
- Ranking metrics:
  - Primary: **PR-AUC**
  - Secondary: ROC-AUC, F1

### 5. Cross Validation | 交叉验证
- 5-fold Stratified K-Fold
- Report **mean ± standard deviation**
- Used for robustness verification rather than threshold tuning

### 6. Threshold Strategy | 阈值策略
- Threshold selection is separated from model selection
- Compared strategies:
  - Default threshold (0.50)
  - Best F1 threshold
  - Recall-floor threshold (business-oriented reference)

### 7. Evaluation | 模型评估
Metrics include:
- PR-AUC (primary)
- ROC-AUC
- F1-score
- Precision / Recall
- Accuracy / Balanced Accuracy

### 8. Error Analysis | 误差分析
- Analyze False Positives (FP) and False Negatives (FN)
- Inspect key features such as:
  - OverTime
  - JobRole
  - MonthlyIncome
  - Age

### 9. Model Interpretation | 模型解释
- Logistic Regression coefficients
- Directional interpretation only (**not causal**)

---

## 📁 Repository Structure | 仓库结构

```text
CDS524-IBM-HR-Attrition-Prediction/
├── IBM_HR_Attrition_Final_Notebook.ipynb
├── README.md
├── WA_Fn-UseC_-HR-Employee-Attrition.csv
├── split_artifacts.json
├── oof_model_comparison.csv
├── cross_validate_summary.csv
├── oof_threshold_plan.csv
├── test_threshold_comparison.csv
├── final_test_metrics.csv
├── test_error_analysis_full.csv
├── feature_coefficients.csv
└── report_figures/
    ├── 01_target_distribution.png
    ├── 02_attrition_rate_overtime_jobrole.png
    ├── 03_cv_model_comparison.png
    ├── 04_threshold_comparison_metrics.png
    ├── 05_pr_curve_with_threshold_points.png
    ├── 06_confusion_matrix_presentation.png
    ├── 07_lr_coefficients_directional.png
    ├── 08_error_analysis_overtime.png
    └── 09_error_analysis_jobrole.png

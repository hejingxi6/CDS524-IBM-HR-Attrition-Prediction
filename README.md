# IBM HR Attrition Prediction  
**IBM 员工离职预测项目（Machine Learning）**

---

## 📌 Project Overview | 项目简介

This project builds a machine learning pipeline to predict employee attrition using the IBM HR Analytics dataset.  
The goal is to identify employees who are likely to leave and analyze key factors associated with attrition.

本项目基于 IBM HR 数据集，构建完整的机器学习流程，用于预测员工是否离职，并分析影响离职的关键因素。

---

## 📂 Dataset | 数据集

- Source: IBM HR Analytics Employee Attrition Dataset  
- File: `WA_Fn-UseC_-HR-Employee-Attrition.csv`  
- Task Type: **Binary Classification**

---

## ⚙️ Methodology | 方法流程

### 1. Data Processing | 数据处理
- Remove ID / constant columns (e.g., `EmployeeNumber`, `Over18`)
- Handle missing values using median / most frequent imputation
- One-hot encoding with `drop='if_binary'` for cleaner interpretation

---

### 2. Data Split | 数据划分
- Fixed **train_val / test split**
- Test set is strictly held out and never used during model selection

---

### 3. Model Candidates | 模型选择
- Dummy (baseline)
- Logistic Regression (unweighted / balanced)
- Random Forest
- XGBoost (if available)

---

### 4. Model Selection | 模型选择策略
- Based on **OOF (out-of-fold) predictions**
- Ranking metrics:
  - Primary: **PR-AUC**
  - Secondary: ROC-AUC, F1

---

### 5. Cross Validation | 交叉验证
- 5-fold Stratified K-Fold
- Report **mean ± standard deviation**
- Used for robustness verification (not threshold tuning)

---

### 6. Threshold Strategy | 阈值策略
- Threshold selection is separated from model selection
- Compared strategies:
  - Default (0.50)
  - Best F1
  - Recall floor (business-oriented)

---

### 7. Evaluation | 模型评估
Metrics include:
- PR-AUC (primary)
- ROC-AUC
- F1-score
- Precision / Recall
- Accuracy / Balanced Accuracy

---

### 8. Error Analysis | 误差分析
- Analyze False Positives (FP) and False Negatives (FN)
- Key features:
  - OverTime
  - JobRole
  - MonthlyIncome
  - Age

---

### 9. Model Interpretation | 模型解释
- Logistic Regression coefficients
- Directional interpretation (NOT causal)

---

## 📊 Outputs | 输出文件说明

| File | Description |
|------|------------|
| `oof_model_comparison.csv` | 模型排序结果（OOF） |
| `cross_validate_summary.csv` | CV mean ± std |
| `oof_threshold_plan.csv` | 阈值策略（训练阶段） |
| `test_threshold_comparison.csv` | 测试集阈值对比 |
| `final_test_metrics.csv` | 最终报告指标 |
| `test_error_analysis_full.csv` | 全量误差分析 |
| `feature_coefficients.csv` | LR 系数解释 |
| `report_figures/` | 所有报告图表 |

---

## 📈 Key Findings | 关键结论

- Logistic Regression performs competitively and is more stable
- Accuracy alone is misleading due to class imbalance
- PR-AUC is a more appropriate primary metric
- Threshold selection significantly affects Precision/Recall trade-off

---

## ⚠️ Limitations | 局限性

- Single hold-out test set may introduce variance
- Threshold strategy may not generalize perfectly
- Results show correlation, not causation

---

## 🚀 How to Run | 运行方式

1. Open the notebook:
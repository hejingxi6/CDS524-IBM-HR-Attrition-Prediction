# IBM HR Attrition Prediction

**CDS524 Group Project — IBM 员工离职预测（Machine Learning Application）**

---

## 1. Project Overview | 项目简介

This project builds a machine learning pipeline to predict employee attrition using the IBM HR Analytics dataset.  
The task is a **binary classification problem**, where the target variable is whether an employee leaves the company (`Attrition = Yes/No`).

本项目使用 IBM HR Analytics 数据集构建一个员工离职预测机器学习流程。  
该任务属于**二分类问题**，目标变量为员工是否离职（`Attrition = Yes/No`）。

The main goals of this project are:

- to perform a complete and reproducible machine learning workflow,
- to compare multiple candidate models,
- to evaluate threshold strategies under class imbalance,
- to analyze model errors and interpret important factors related to attrition.

本项目的主要目标包括：

- 完成一个完整且可复现的机器学习流程；
- 比较多个候选模型；
- 在类别不平衡条件下分析不同阈值策略；
- 对模型误差进行分析，并解释影响离职预测的重要因素。

---

## 2. Dataset | 数据集说明

- **Dataset Name:** IBM HR Analytics Employee Attrition & Performance
- **Source:** Kaggle  
- **URL:** https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset
- **Target Column:** `Attrition`
- **Task Type:** Binary Classification

### Important Note | 重要说明
According to the dataset description, this is a **fictional dataset created by IBM data scientists**.  
Therefore, the results of this project should be interpreted as a **coursework machine learning study** rather than a directly deployable real-world HR decision system.

根据数据集说明，该数据集是 **IBM 数据科学家构造的虚拟数据集**。  
因此，本项目结果应被理解为一个**课程机器学习实验研究**，而不是可直接部署到真实 HR 决策场景中的系统。

---

## 3. Project Workflow | 项目流程

The project follows a standard end-to-end machine learning workflow:

1. **Data Loading & Inspection**  
   Load the HR dataset and inspect shape, columns, missing values, and class distribution.

2. **Data Cleaning**  
   Remove identifier or non-informative columns and prepare the dataset for modeling.

3. **Exploratory Data Analysis (EDA)**  
   Analyze attrition distribution, overtime/job role differences, and related visual patterns.

4. **Train / Validation / Test Split**  
   Use a stratified split to preserve class distribution.

5. **Model Training**  
   Train and compare multiple candidate models.

6. **Threshold Selection**  
   Select decision thresholds on validation data only.

7. **Final Test Evaluation**  
   Evaluate the final selected model on the held-out test set.

8. **Interpretation & Error Analysis**  
   Analyze coefficients, threshold behavior, and error patterns.

本项目遵循标准端到端机器学习流程：

1. **数据读取与检查**  
2. **数据清洗**  
3. **探索性数据分析（EDA）**  
4. **训练 / 验证 / 测试集划分**  
5. **模型训练与比较**  
6. **基于验证集进行阈值选择**  
7. **最终测试集评估**  
8. **结果解释与误差分析**

---

## 4. Leakage Prevention | 防数据泄漏说明

To avoid data leakage, the project uses the following strategy:

- preprocessing is applied within the modeling pipeline,
- threshold selection is performed on the **validation set only**,
- the **test set is used only once** for final evaluation,
- model comparison and threshold planning are separated from final test reporting.

为了避免数据泄漏，本项目采用以下策略：

- 预处理在模型流程中完成；
- 阈值选择**只在验证集上进行**；
- **测试集只用于最终评估一次**；
- 模型比较与阈值分析与最终测试报告分离。

---

## 5. Candidate Models | 候选模型

The repository compares multiple models and threshold strategies, with a focus on interpretable and practical classification under class imbalance.

本仓库比较了多个模型及阈值策略，重点关注类别不平衡条件下兼顾可解释性与实用性的分类表现。

---

## 6. Final Model Selection | 最终模型选择

The final selected model is:

- **Logistic Regression**

This model was chosen because it provided the best overall balance on the evaluation metrics, especially when compared with Random Forest.  
Although another model may slightly improve recall in some settings, Logistic Regression achieved stronger overall trade-offs and better interpretability.

最终选择的模型为：

- **Logistic Regression（逻辑回归）**

选择该模型的原因是：它在整体评估指标上表现更均衡，并且相较于 Random Forest 取得了更好的综合结果。同时，逻辑回归具有更强的可解释性，更适合课程项目的分析与展示。

---

## 7. Final Test Results | 最终测试结果

### Final Selected Threshold
- **Threshold = 0.76**

### Test Metrics
- **Accuracy:** 0.8597
- **Precision:** 0.5833
- **Recall:** 0.4000
- **F1-score:** 0.4746
- **ROC-AUC:** 0.8149
- **PR-AUC:** 0.5807

### Interpretation | 结果解读

These results show that the model has a **reasonable ranking and discrimination ability**, especially as reflected by ROC-AUC and PR-AUC.  
However, the recall is still limited, which means some true attrition cases are missed.

The selected threshold (0.76) is relatively conservative:
- it improves precision,
- but reduces recall.

This means the final model is better understood as a **reproducible and interpretable baseline system** rather than a high-recall production-ready HR screening tool.

这些结果表明，模型具有一定的**排序能力和区分能力**，尤其体现在 ROC-AUC 和 PR-AUC 上。  
但 recall 仍然偏低，说明模型仍会漏掉一部分真实离职员工。

当前选择的阈值（0.76）相对保守：
- 提高了 precision，
- 但降低了 recall。

因此，该模型展示了一个具有实际意义且可解释的员工离职预测基线，同时也为后续在更注重召回率的实际场景中进一步优化留下了空间。

---

## 8. Repository Structure | 仓库结构

```text
CDS524-IBM-HR-Attrition-Prediction/
├── IBM_HR_Attrition_Final_Notebook.ipynb
├── README.md
├── requirements.txt
├── WA_Fn-UseC_-HR-Employee-Attrition.csv
├── cross_validate_summary.csv
├── feature_coefficients.csv
├── final_test_metrics.csv
├── oof_model_comparison.csv
├── oof_threshold_plan.csv
├── split_artifacts.json
├── test_error_analysis_full.csv
├── test_threshold_comparison.csv
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

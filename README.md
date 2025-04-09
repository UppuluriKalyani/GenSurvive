# 🧬 Cancer Subtype Prediction & Survival Analysis

Welcome to the **Cancer Subtype Discovery and Survival Prediction** project! This project focuses on identifying hidden cancer subtypes and predicting patient survival using **gene expression profiles** and **clinical data**. It's a fusion of bioinformatics and machine learning made simple and efficient.

---

## 📌 Table of Contents
- [🚀 Project Overview](#-project-overview)
- [📂 File Structure](#-file-structure)
- [🧾 Dataset Details](#-dataset-details)
- [🧠 Model Workflow](#-model-workflow)
- [🧪 Sample Test Cases](#-sample-test-cases)
- [📈 Results](#-results)

---

## 🚀 Project Overview

This tool performs:
- ✅ **Cancer subtype prediction** from gene expression
- ✅ **Clustering of gene profiles** to discover hidden subtypes
- ✅ **Mapping clusters to known cancer types**
- ✅ **Survival time estimation** from clinical gene impact
- ✅ **Smart handling of unknown, invalid, or healthy cases**

The goal is to support researchers, doctors, and bioinformaticians in identifying rare or hidden cancer subtypes and assessing survival likelihood.

---

## 📂 File Structure

```
Cancer-Subtype-Discovery/
│
├── cancer_project.ipynb                   # 💻 Main Jupyter Notebook with implementation
│
├── datasets/                              # 📊 Original gene expression datasets
│   ├── gene_expression_1.csv
│   ├── gene_expression_2.csv
│   └── ...
│
├── oncodb_expression/                     # 🧬 OncoDB Gene Expression Files (21 files)
│   ├── expr_cancer1.csv
│   └── ...
│
├── oncodb_clinical/                       # 📄 OncoDB Clinical Data Files (57 files)
│   ├── clinical_cancer1.csv
│   └── ...
│
├── sample_patient/                        # 🧪 Test Case CSVs for evaluation
│   ├── test_patient_1.csv
│   ├── test_patient_2.csv
│   ├── test_patient_3.csv
│   ├── test_patient_4.csv
│   └── test_patient_5.csv
│
├── results/                               # 📁 Output predictions folder
│   ├── test_patient_1_output.csv
│   ├── ...
│
├── data/                                  # 📌 Preprocessed data used for prediction
│   ├── train_data.csv                     # Contains known clusters & cancer types
│   └── clinical_data.csv                  # Contains survival-related metrics
│
│
└── README.md                              # 📘 Project documentation (this file!)
```


## 🧾 Dataset Details

| 🗂️ Category | 📁 Location | 📄 Filename / Pattern | 📌 Description | 🔢 Shape / Notes |
|------------|-------------|------------------------|----------------|------------------|
| 🔬 Original Expression Datasets | `data/original/` | `Dataset_S1.csv` | Gene expression matrix (Genes × Patients) | `78 × 4750` |
| | | `Dataset_S2.csv` | Gene identifiers for the 4750 genes | `4750 × 1` |
| | | `Dataset_S3.csv` | Survival data (Time, Event) | `78 × 2` |
| 🧬 OncoDB Expression Datasets | `data/expression/` | `*_Differential_Gene_Expression_Table.txt` | Gene expression data for each TCGA cancer type | 21 files |
| | | Example: `BRCA_Differential_Gene_Expression_Table.txt` | Expression data for Breast Cancer (BRCA) | - |
| | | 🔑 Important Columns | `Cancer type`, `Gene symbol`, `log2 fold change`, `FDR adjusted p-value` | - |
| 🧪 OncoDB Clinical Datasets | `data/clinical/` | `Differential_Clinical_Expression_*.txt` | ANOVA results from expression data | 57 files |
| | | `Differential_Clinical_Methylation_*.txt` | ANOVA results from methylation data *(optional)* | - |
| | | 🔑 Important Columns | `Cancer type`, `Gene symbol`, `Clinical parameters`, `ANOVA p-value`, `FDR` | - |



## 🧠 Model Workflow

> This project follows a step-by-step pipeline from data preprocessing to cancer subtype discovery and survival prediction.

### 🔁 Step-by-Step Pipeline:

| 🔢 Step | 📌 Description |
|--------|----------------|
| **1. Data Collection** | Load original gene expression data and OncoDB datasets (expression & clinical). |
| **2. Preprocessing** | Clean data, normalize gene expression values, remove duplicates, and align patient IDs. |
| **3. Feature Extraction** | Use statistical tests (e.g., ANOVA) to extract relevant genes with high variance. |
| **4. Clustering** | Apply unsupervised learning (e.g., k-means or hierarchical clustering) to identify cancer subtypes. |
| **5. Subtype Mapping** | Match discovered clusters with known subtypes using MSigDB & OncoDB gene set mappings. |
| **6. Survival Analysis** | Estimate survival time using OncoDB clinical data & Cox regression or ANOVA-based significance. |
| **7. Prediction Interface** | Accept user-provided gene data in CSV form and predict: <br> 🔹 Cancer subtype <br> 🔹 Cluster <br> 🔹 Estimated survival time <br> 🔹 Detection category (e.g., Unclassified/No Significant Findings) |

---

### 🧪 Prediction Behavior:

| 🎯 Scenario | 🧾 Output |
|-------------|-----------|
| ✅ Valid gene with known cancer | Subtype, cluster, survival prediction |
| 🚫 Unknown cancer type | "Unclassified Condition" |
| ❌ Missing cancer type or gene ID | "No Significant Findings" |
| 🧍‍♂️ Non-numeric input | Error: Invalid file structure |


---

## 🧪 Sample Test Cases

| 🔢 Test Case | 📥 Input (CSV) | 🧾 Output |
|-------------|----------------|-----------|
| ✅ **Valid Case - Known Cancer** | Gene expression values| `Detected Condition`: BRCA <br> `Predicted Cluster`: 2 <br> `Predicted Subtype`: Luminal A <br> `Estimated Survival`: 32 months |
| 🟡 **No Cancer Detected** | File with missing or null `Cancer type` | `Detected Condition`: No Significant Findings <br> `Predicted Cluster`: - <br> `Predicted Subtype`: - <br> `Estimated Survival`: - |
| 🔴 **Unclassified Condition** | File with `Cancer type = XYZ` (not in training set) | `Detected Condition`: Unclassified Condition <br> `Predicted Cluster`: - <br> `Predicted Subtype`: - <br> `Estimated Survival`: - |
| ❌ **Invalid Input Format** | File with strings instead of numeric gene values (e.g., `"abc"`, `"xyz"`) | ⚠️ Error: Invalid file structure or non-numeric values detected |
| ✅ **Multiple Patients** | File with 5 rows of valid patient data | Outputs predictions for all 5 patients with respective clusters, subtypes, and survival estimates |

Here’s how you can present **📊 Model Results** for **training and testing datasets** using **images** in a table format within your README:

---

## 📈 Model Results

Here’s a **📊 Results** section you can include in your README:

---

## 📊 Results

We evaluated our model on multiple patient samples to demonstrate its ability to identify cancer subtypes and estimate survival:

| 🧪 Test Case | 🧬 Detected Condition | 🔗 Predicted Cluster | 🧠 Predicted Subtype | ⏳ Estimated Survival Time |
|-------------|-----------------------|-----------------------|----------------------|----------------------------|
| Test Case 1 | BRCA                  | 2                     | Luminal A           | 32 months                  |
| Test Case 2 | LUAD                  | 1                     | Proximal Inflammatory | 24 months               |
| Test Case 3 | *(null cancer type)*  | -                     | -                    | -                          |
| Test Case 4 | XYZ                   | -                     | -                    | - *(Unclassified)*         |
| Test Case 5 | LAML                  | 3                     | High Risk            | 18 months                  |


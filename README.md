# Learning Topological Features for Protein Stability Prediction

**Author:** Amish Mishra  
**Date:** June 25, 2025

> **Note:** To keep the repository size manageable, some directories are empty. Once you have access to the data and notebooks, these can be repopulated locally.

---

## 🧬 Project Overview

This project investigates the use of **topological data analysis (TDA)** to predict **protein stability** from structural data. We work with synthetic protein designs from the [Rocklin dataset](https://www.science.org/doi/10.1126/science.aan0693), applying machine learning models to classify proteins as **stable** or **unstable** using features derived from:

1. **Persistence diagrams** processed via [Cover-tree Differencing via Entropy Reduction (CDER)](https://arxiv.org/abs/1702.07959),
2. **Subject matter expert (SME) features**, and
3. **A combination of CDER and SME features**.

The diagram below shows the pipeline from raw protein `.pdb` files to CDER-based feature generation:

![CDER Protein Pipeline](/figures/cder_protein.gif)

---

## 🔍 Research Questions

We explore the following key questions:

1. What areas of the persistence diagram are characteristic of stable/unstable proteins (based on CDER coordinates)?

2. What are the effects on model performance when incorporating topological information into the classification task of these proteins? Does adding features generated using CDER to an SME model improve the model?

3. What are the correlations between the CDER and SME features? What does a highly correlated CDER feature and SME feature tell us?

4. What are the most important features for the classifiers?

---

## 🧪 Protein Design Notation

We use a simplified English notation to represent secondary protein structures. Below is the conversion from structure notation to symbols:

| Design Label | Secondary Structure     |
|--------------|--------------------------|
| HHH          | ααα                      |
| HEEH         | αββα                     |
| EHEE         | βαββ                     |
| EEHEE        | ββαββ                    |

Where:
- **α (alpha)** = alpha helix  
- **β (beta)** = beta sheet

---

## ⚙️ Installation Guide

To get started, follow the steps below:

1. **Clone the repository**
   ```bash
   git clone https://github.com/amish-mishra/CDER-protein-classifier.git
   cd CDER-protein-classifier
    ```

2. **Create a conda environment**

   ```bash
   conda env create -f environment.yml
   ```

3. **Activate the environment**

   ```bash
   conda activate cder2
   ```

4. **Install the CDER dependency**

   Required for running any CDER-based notebooks.
   Follow instructions at: [https://github.com/geomdata/gda-public](https://github.com/geomdata/gda-public)

5. **Launch Jupyter Notebooks**

   ```bash
   jupyter notebook
   ```

---

## 📁 Directory Structure

| Directory                             | Description                                      |
| ------------------------------------- | ------------------------------------------------ |
| `cder_feature_importances_dataframes` | CDER feature importance data                     |
| `cder_models`                         | Trained CDER models                              |
| `classifiers`                         | Best classifiers from hyperparameter tuning      |
| `features_dataframes`                 | Normalized features used for training            |
| `figures`                             | Plots and visualizations                         |
| `perf_dataframes`                     | Performance results of ML models                 |
| `protein_metadata`                    | CSV files with SME features and stability labels |
| `protein_pdbs/rocklin_2017`           | Raw `.pdb` protein structure files               |
| `protein_pds`                         | Persistence diagrams (PDs)                       |
| `sme_feature_importances_dataframes`  | SME feature importances by design topology       |

> ⚠️ Some directories like `/protein_pdbs`, `/protein_pds`, `/cder_models`, and `/classifiers` may be empty due to size constraints.

---

## 📓 Notebook Workflow

Run the notebooks in the following order:

1. `01make_pds.ipynb` – Generate persistence diagrams (PDs)
2. `02make_main_df.ipynb` – Combine stability, SME, and PD data into one dataframe
3. `03analyze_protein_df.ipynb` – Visualize the spread of stable vs. unstable proteins
4. `04sme_ml.ipynb` – Train/test ML model using SME features
5. `05cder-ml.ipynb` – Train/test ML model using CDER features from PDs
6. `06sme-cder-ml.ipynb` – Train/test ML model using both SME and CDER features
7. `07make_feature_imp_df.ipynb` – Compute average SME feature importance by design topology
8. `08analyze_performance.ipynb` – Compare model performance and plot feature importances
9. `09visualize_cder_correlations.ipynb` – Plot CDER-SME feature correlations and highlight informative features
10. `hex_plot_example.ipynb` – Visualize region-of-difference hexplots on PDs


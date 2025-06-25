# Learning Topological Features for Protein Stability Prediction
Author: Amish Mishra  
Date: June 25, 2025  
_Note: The directories may be mostly empty to keep the size of the repo small. With access to the data and the notebooks, the directories can be repopulated on a local copy of the repo._


## Description
In this project, we take the Rocklin synthetic protein designs and train machine learning models to classify a protein as stable or unstable. Using the Cover-Tree Differencing via Entropy Reduction (CDER) algorithm, we do this using three approaches
1. Learn CDER coordinates on the persistence diagrams (PDs) corresponding to each protein and train an ML model based solely on this topological information.
2. Use the subject matter expert (SME) features to train ML models
3. Use CDER and SME together to train ML models

A sequence of steps for the pipeline of going from a raw protein `.pdb` file to a featurizaiton using CDER is shown below:

![CDER Protein Pipeline](/figures/cder_protein.gif)

We then investigate the following:
1. What areas of the persistence diagram are characteristic of stable/unstable proteins (based on CDER coordinates)?
2. What are the effects on model performance when incorporating topological information into the classification task of these proteins? Does adding features generated using CDER to an SME model improve the model?
3. What are the correlations between the CDER and SME features? What does a highly correlated CDER feature and SME feature tell us?
4. What are the most important features for the classifiers?

## Note
Proteins design topologies are labeled differently here than in the peer-reviewed paper. A conversion for the designs is given below (we choose to use the english version for this repository). In the notation below, $\alpha$ represents an alpha helix and $\beta$ represents a beta sheet in the protein's secondary structure.
- HHH: $\alpha \alpha \alpha$
- HEEH: $\alpha \beta \beta \alpha$
- EHEE: $\beta \alpha \beta \beta$
- EEHEE: $\beta \beta \alpha \beta \beta$

## Installation
To set up the environment and run the notebooks:

1. **Clone this repository** and navigate to its directory:
    ```bash
    git clone https://github.com/amish-mishra/CDER-protein-classifier.git
    cd CDER-protein-classifier
    ```

2. **Create a conda environment** using the provided `environment.yml`:
    ```bash
    conda env create -f environment.yml
    ```

3. **Activate the environment**:
    ```bash
    conda activate cder-protein-classifier
    ```

4. **Install the `gda-public` repository** (required for CDER functionality):  
    Follow the official installation instructions at [https://github.com/geomdata/gda-public/](https://github.com/geomdata/gda-public/).  
    _Note: This step is essential for running any notebooks that use CDER._

5. **Launch Jupyter Notebook**:
    ```bash
    jupyter notebook
    ```
    Then open and run the notebooks in the order listed below.

## Structure of directories and notebooks
### The Directories
- `cder_feature_importances_dataframes`: stores the dataframes used to assess feature importance
- `cder_models`: stores trained CDER models
- `classifiers`: stores the best ML classifiers from the random forest hyperparameter grid search
- `features_dataframes`: stores the dataframes of the normalized features that were used to train the ML models
- `figures`: stores any generated figures
- `perf_dataframes`: stores the performance dataframe outputs after training and testing the ML models
- `protein_metadata`: contains the csv files with the sme features and stability scores
- `protein_pdbs`: contains the folder `rocklin_2017` that has all raw `.pdb` files with protein data.
- `protein_pds`: stores the generated PDs for each protein
- `sme_feature_importances_dataframes`: stores the dataframes containing the feature importance for each SME feature for each iteration of each protein design topology

### The Notebooks
The notebooks are meant to be run in the following order.
1. `1make_pds.ipynb`: This notebook creates the persistence diagrams.
2. `2make_main_df.ipynb`: This notebook creates the main dataframe with the stability, SME, and PDs data.
3. `3analyze_protein_df.ipynb`: This notebook visualizes the spread of the stable and unstable proteins by protein design topology
4. `4sme_ml.ipynb`: This notebook trains and tests an ML model based on the SME features
5. `5cder-ml.ipynb`: This notebook trains and tests an ML model based on learned CDER coordinates on the PDs of the proteins
6. `6sme-cder-ml.ipynb`: This notebook trains and tests and ML model based on the learned CDER coordinates on the PDs and the SME features
7. `7make_feature_imp_df.ipynb`: This notebook creates a dataframe that stores the average feature importance for each SME feature for the SME-only ML classifier (for each protein design topology)
8. `8analyze_performance.ipynb`: This notebook summarizes and compares the ML classifiers' performance that were trained on SME, CDER, and SME+CDER features. It also plots the feature importance.
9. `9visualize_cder_correlations.ipynb`: This notebook analyzes the correlation between SME features and CDER features via plotting CDER coordinates and a scatterplot of correlations illustrating the most important SME features for the model trained on only SME features.
10. `hex_plot_example.ipynb`: This notebook generates a hexplot of the regions of difference in the persistence pairs of an example protein design topology.

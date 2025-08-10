# Environmental Omics Data Analytics (**EODA**) 🧬🌍

## 🎯 Introduction

In environmental and biological sciences, understanding complex relationships between molecular features (e.g., from FT-ICR MS) and environmental parameters is crucial for gaining insights into ecosystem functioning and processes. The sheer volume and complexity of multi-omics data necessitate robust computational pipelines for effective analysis, visualization, and interpretation.

**EODA** provides a comprehensive R and Python-based pipeline designed for the integrated analysis of environmental and molecular formula (MF) data. It streamlines the entire workflow from raw data import and preprocessing to advanced statistical analysis, dimensionality reduction, correlation assessment, and interpretable machine learning modeling.

## 📄 Supporting Research Publication

This project serves as the computational framework for processing and analyzing the data presented in the following scientific paper:

**Title**: "Environmental drivers of dissolved organic matter composition across central European aquatic systems: A novel correlation-based machine learning and FT-ICR MS approach"
**Authors**: Michel Gad, Narjes Tayyebi Sabet Khomami, Ronald Krieg, Jana Schor, Allan Philippe, Oliver J. Lechtenfeld
**Journal**: Water Research
**DOI**: 10.1016/j.watres.2024.123018 (https://doi.org/10.1016/j.watres.2024.123018)

This repository provides the code base necessary to reproduce the data processing, statistical analyses, and machine learning models applied to the Dissolved Organic Matter (DOM) and environmental parameter datasets within Central European aquatic systems, contributing directly to the findings and figures in the publication.

## 💾 Data Management and Reproducibility with DataLad

This project leverages DataLad (https://www.datalad.org/) for robust data management and enhanced reproducibility. DataLad is a distributed version control system for data that builds on Git, allowing large datasets to be tracked alongside code.

The input data repository for this project is specifically tracked using DataLad. This ensures that:

* All versions of the raw and intermediate data files are meticulously versioned.
* The exact data used to generate the results in the accompanying scientific publication can be precisely retrieved and reproduced by anyone.
* Data provenance is maintained, linking specific analytical results back to specific versions of the data.

By utilizing DataLad, we provide a transparent and verifiable pathway to reproduce the scientific findings presented.

## 🚀 Project Goal: Unraveling Environmental Drivers of DOM Composition in Central European Aquatic Systems

The primary goal of **EODA**, in the context of the supported publication, is to offer a robust, reproducible, and interpretable framework for understanding the **environmental drivers of dissolved organic matter composition** across Central European aquatic systems. It achieves this by:

1.  Standardizing and cleaning diverse raw data specific to environmental parameters and FT-ICR MS-derived DOM molecular formulas from Central European aquatic environments.
2.  Generating rich molecular descriptors for DOM and calculating their intensity-weighted averages to characterize the complex organic matter composition.
3.  Performing in-depth statistical and dimensionality reduction analyses (e.g., PCA) to identify patterns and underlying environmental controls on DOM composition.
4.  Quantifying complex correlations between specific molecular features of DOM and key environmental variables (e.g., hydrological, chemical, geographical parameters) in these aquatic systems.
5.  Building and interpreting machine learning models to predict DOM composition based on environmental drivers, thereby identifying the most influential factors shaping organic matter characteristics.

## 🛠️ How It Works

This project is structured as a modular pipeline, primarily leveraging R for data processing and statistical analysis, and Python for advanced machine learning and model interpretability.

---

### 1. Data Import, Preprocessing & Feature Engineering

These scripts are responsible for handling raw data, cleaning it, performing necessary transformations (like decimal conversions), and calculating crucial molecular descriptors. They prepare the data for downstream statistical and machine learning tasks.

*   `env.R`:
    * Imports and cleans raw environmental parameter data.
    * Handles comma-separated decimals and standardizes names.
    * Performs Z-score normalization.
    * Generates diagnostic plots: density distributions, normality box plots, and correlation networks of environmental parameters.
*   `mf.R`:
    * Imports and cleans raw molecular formula data (e.g., from FT-ICR MS).
    * Handles comma-separated decimals, polarity indicators, and standardizes names.
    * Calculates a wide range of molecular descriptors: Kendrick Mass Defect (KMD), Aromaticity Index (AI), Nominal Oxidation State of Carbon (NOSC).
    * Computes intensity-weighted averages of these molecular properties for each sample.
    * Analyzes and plots the relative abundance of molecular formula classes (CHO, CHNO, CHNOS, CHOS).
    * Generates density distributions, normality box plots, and correlation networks of molecular formula parameters.
*   `wa.R`:
    * Processes and aggregates raw molecular data to calculate intensity-weighted average molecular descriptors.
    * Handles polarity fractions and cleans measurement names for consistent grouping.
    * Performs Z-score normalization on weighted averages.
    * Visualizes density distributions, normality box plots, and correlation networks of weighted average parameters.

---

### 2. Dimensionality Reduction

This script applies Principal Component Analysis (PCA) to reduce the complexity of the datasets and visualize the primary sources of variation.

*   `pca.R`:
    * Performs PCA on both environmental parameters and intensity-weighted averaged molecular data.
    * Integrates land class information to color and group samples in PCA biplots, aiding in visual interpretation of environmental influences.
    * Generates scree plots to assess explained variance and guide component selection.
    * Outputs PCA biplots showing relationships between samples and variables.

---

### 3. Inter-data Correlation Analysis

This script quantifies the relationships between molecular features and environmental variables, providing insights into which molecular properties are associated with specific environmental conditions.

*   `corr.R`:
    * Calculates Spearman correlation coefficients between molecular formula peak intensities and environmental parameters.
    * Analyzes the prevalence of molecular formulas across different sites.
    * Generates distribution plots of Spearman's rho values for each environmental variable.
    * Creates correlation networks and heatmaps for:
        * Environmental parameters based on the similarity of their correlation profiles with MFs.
        * Molecular formula properties (e.g., H/C, O/C).
    * Generates Van Krevelen (vK) diagrams where molecular formulas are colored based on their correlation strength (positive, negative, weak) with specific environmental variables.

---

### 4. Machine Learning Regression & Interpretability

This Python-based module builds predictive models to explore how molecular features can explain environmental variations, utilizing advanced techniques for model robustness and interpretability.

*   `MRF.py` (utilizing processing.py):
    * Prepares data for a Random Forest Regression model, using the comprehensive correlation results from `corr.R` as input.
    * Implements outlier detection using Isolation Forest to enhance model robustness.
    * Performs Repeated K-Fold Cross-Validation for rigorous model evaluation.
    * Applies SHapley Additive exPlanations (SHAP) to interpret model predictions, showing how each molecular feature contributes to the output. Generates SHAP summary, bar, and beeswarm plots.
    * Calculates permutation feature importance to identify the most impactful features in the model.

## ✨ Features

**EODA** provides the following key functionalities for comprehensive environmental omics data analysis, directly supporting the associated publication:

*   Automated Data Cleaning & Standardization: Handles diverse input formats (e.g., comma-decimals) and standardizes column names.
*   Comprehensive Molecular Feature Engineering: Calculates a wide array of molecular descriptors (KMD, AI, NOSC, etc.) and intensity-weighted averages crucial for DOM characterization.
*   Relative Abundance Profiling: Quantifies and visualizes the distribution of molecular formula classes across samples, informing DOM composition changes.
*   Robust Statistical & Dimensionality Reduction: Includes density/normality plots, correlation networks, and Principal Component Analysis for clear data understanding of environmental and molecular datasets.
*   Advanced Inter-data Correlation: Computes and visualizes Spearman correlations between molecular and environmental data, including prevalence analysis and Van Krevelen diagrams, highlighting relationships relevant to DOM transformations.
*   Integrated Machine Learning Pipeline: Employs Random Forest Regression with robust outlier detection and cross-validation for predictive modeling, exploring the influence of molecular features on environmental parameters.
*   Model Interpretability: Utilizes SHAP and permutation importance to explain model predictions and identify key molecular drivers of environmental changes.
*   Publication-Quality Visualizations: All plots are generated with consistent, clean themes suitable for scientific publications.
*   Modular & Reproducible Workflow: The pipeline is designed with distinct R and Python scripts, facilitating modularity and reproducibility of the published results.

## 🚀 Getting Started

Ready to analyze your environmental omics data? Follow these steps to set up the project and run the analysis.

### 1. Project Setup

First, clone the repository to your local machine:

```bash
git clone https://github.com/MichelGad/**EODA**.git
cd **EODA**
```
Create the necessary input and output directories:

```bash
mkdir input
mkdir output
mkdir processed
```
### 2. Obtain Raw Data

The raw data used in this project is openly available through the UFZ Data Repository, ensuring full transparency and reproducibility of the results:

Raw Data Repository: https://doi.org/10.48758/ufz.15515 (https://doi.org/10.48758/ufz.15515)

You can manually download the input.zip archive directly from the UFZ Data Repository link provided above, extract its contents, and place the unzipped files (env_2025-01-21.csv, formulas.clean_2025-01-21.csv, eval.summary.clean_2025-01-21.csv) into the input/ directory within your project structure.

### 3. Automated Environment Setup (setup.sh)

For a quick and automated setup of both R and Python environments, you can use the provided setup.sh script.

#### 1.  Save the Script:
    Save the content provided in the setup.sh file into a file named setup.sh (or another .sh name) in your project's root directory.

#### 2.  Make it Executable:
    Open your terminal, navigate to your project directory, and make the script executable:
    ```bash
    chmod +x setup.sh
    ```

#### 3.  Run the Script:
    Execute the script from your terminal:
    ```bash
    ./setup.sh
    ```
    
    This script will:
    * Create a temporary R script (install_packages.R) to install the required R packages from CRAN.
    * Set up a Python virtual environment named venv.
    * Activate the venv and install all necessary Python libraries using pip.

    You will see progress messages in your terminal. Once completed, your R and Python environments will be ready.

    Note for Windows Users: If you are on Windows, the source venv/bin/activate command in the setup.sh script might not work directly. You may need to manually activate the Python virtual environment after the venv is created, by running .\venv\Scripts\activate in PowerShell or .\venv\Scripts\activate.bat in Command Prompt, and then manually run the pip install commands. However, the R part of the script should function as described.

#### 4. Run the Analysis Pipeline

The R scripts generate intermediate processed data files in the processed/ directory, which are then used by subsequent R scripts and the Python script. It's crucial to run them in the following order:

##### 4.1 Run R Scripts (in order)

Open each R script in RStudio and run it, or execute them from the terminal:

```bash
Rscript env.R
Rscript wa.R
Rscript mf.R
Rscript pca.R
Rscript corr.R
```
This will populate the processed/ directory with cleaned data and generate plots in the output/ subdirectories (output/env, output/wa, output/mf, output/pca, output/corr).

##### 4.2 Run Python Script

After all R scripts have successfully run and processed/rho_MF.csv has been generated by corr.R, you can run the Python machine learning script:

```bash
python MRF.py
```
This will generate additional plots and results in the output/MRF and processed/MRF directories.
You are now ready to explore the in-depth analyses of your environmental omics data!

## 📚 Dependencies

This project relies on the following R and Python libraries:

### 📊 R Libraries
| Library        | Description                                       |
| :------------- | :------------------------------------------------ |
| tidyverse      | Collection of core tidyverse packages (dplyr, tidyr, ggplot2, readr, purrr, forcats, stringr, tibble) |
| data.table   | Enhanced data frames for efficient large data operations |
| FactoMineR   | Multivariate exploratory data analysis            |
| factoextra   | Visualization of multivariate analysis results    |
| corrr        | Tidy correlation analysis                         |
| RColorBrewer | Color palettes for attractive plots               |
| patchwork    | Combine separate ggplot2 plots                    |
| MASS         | Modern Applied Statistics with S                  |
| ggpubr       | Publication-ready plots                           |
| rgl          | 3D visualization (optional for certain plots)     |
| ggsci        | Scientific journal style color palettes           |
| htmltools    | Tools for HTML generation (often a dependency for other packages) |
| scales       | Graphic scales for data visualization             |

### 🐍 Python Libraries
| Library        | Description                                       |
| :------------- | :------------------------------------------------ |
| pandas       | Data manipulation and analysis                    |
| numpy        | Numerical computing                               |
| matplotlib   | Static plotting                                   |
| scikit-learn | Machine learning algorithms                       |
| xgboost      | Scalable, Portable, and Distributed Gradient Boosting (often used for tree models) |
| plotly       | Interactive graphing library                      |
| shap         | SHapley Additive exPlanations (model interpretability) |

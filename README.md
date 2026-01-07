# Bioinformatics Project Setup Guide

This guide walks through setting up R, Jupyter notebooks with R kernel, and connecting to the GitHub repository for the Arabidopsis stress integrative omics project.

## Prerequisites

- Linux system (tested on Pop!_OS 22.04)
- Python and pip installed
- Git installed
- Internet connection

## Step 1: Install or Upgrade R

Check if R is installed:

```bash
R --version
```

If R is not installed or version is below 4.4, upgrade to the latest version.

### Add R Repository

```bash
wget -qO- https://cloud.r-project.org/bin/linux/ubuntu/marutter_pubkey.asc | sudo tee /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc > /dev/null
sudo add-apt-repository "deb https://cloud.r-project.org/bin/linux/ubuntu jammy-cran40/"
sudo apt update
sudo apt install r-base
```

Verify R version (should be 4.5.x):

```bash
R --version
```

## Step 2: Install IRkernel for Jupyter Notebooks

Install IRkernel package:

```bash
sudo R -e 'install.packages("IRkernel", repos="https://cran.rstudio.com/")'
```

Register the kernel with Jupyter:

```bash
R -e 'IRkernel::installspec()'
```

Verify kernels:

```bash
jupyter kernelspec list
```

You should see `ir` in the list.

## Step 3: Install BiocManager

In R console or script:

```r
install.packages("BiocManager")
```

## Step 4: Set Up Jupyter Notebook

Create a new notebook or open an existing `.ipynb` file in VS Code.

Select the R kernel from the kernel picker (top-right corner).

Run R code in cells.

## Step 6: Install Required R Packages

### Install System Dependencies

Some R packages require system libraries:

```bash
sudo apt update
sudo apt install -y libcurl4-openssl-dev libssl-dev libxml2-dev libwebp-dev
```

### Install CRAN Packages

```bash
sudo R -e 'install.packages(c("httr", "curl", "rvest", "httr2", "rentrez"), repos="https://cran.rstudio.com/")'
```

### Install Bioconductor Packages

```r
# Install BiocManager if not already done
install.packages("BiocManager")

# Install core bioinformatics packages
BiocManager::install(c("DESeq2", "edgeR", "limma", "Glimma", "GEOquery", "clusterProfiler", "AnnotationDbi", "org.At.tair.db"))

# Install additional packages
BiocManager::install(c("KEGGREST", "GO.db", "GOSemSim", "DOSE", "enrichplot"))
```

### Install Additional CRAN Packages

```bash
sudo R -e 'install.packages(c("Seurat", "tidyverse", "ggplot2", "UpSetR", "RColorBrewer", "gplots"), repos="https://cran.rstudio.com/")'
```

## Step 7: Set Up Python Environment

Create and activate a Python virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install required Python packages:

```bash
pip install numpy pandas matplotlib seaborn scikit-learn scipy statsmodels plotly jupyter biopython
```
\

## Usage

- Use R cells for bioinformatics analysis with packages like DESeq2, edgeR, clusterProfiler.
- Use Python cells for data manipulation and visualization.
- For mixed R/Python code, consider using reticulate in R.

## Troubleshooting

- If R kernel not showing: Re-run `IRkernel::installspec()`
- Permission issues: Use `sudo` for system-wide installs
- BiocManager version conflicts: Ensure R >= 4.4
- Package loading issues: Restart the R kernel in notebooks
- Python packages not found: Ensure virtual environment is activated

## Project Structure

- `test_r.ipynb`: Test notebook for R and Python package checks
- `.venv/`: Python virtual environment
- Other files: Add your analysis scripts and data
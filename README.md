# 🦿 GaitSync: Gait Analysis using Machine Learning

## 🚀 Project Overview

**GaitSync** is a machine learning project for exploring human walking patterns (gait) and building baseline classifiers for gait-related signals. The repository currently contains the analysis notebooks, exported notebook HTML files, reports, presentation material, and proposal documents used for the project.

The notebooks focus on loading marker/sensor-style gait data, preprocessing records, visualizing gait patterns, engineering features, and comparing classical machine learning classifiers.

---

## 🎯 Problem Statement

Human gait analysis plays a critical role in:

* Detecting and monitoring movement-related health conditions
* Supporting rehabilitation progress tracking
* Improving assistive and wearable-health technologies

**Key question:** Can machine learning models analyze gait data and detect meaningful walking-pattern differences from gait measurements?

---

## 🧠 Analysis Workflow

### 1. Data loading and preparation

* Extract a local `gait.zip` dataset into `data/gp_dataset/`.
* Load multiple CSV files from a gait marker dataset folder.
* Concatenate the files into one analysis table.

### 2. Data preprocessing

* Inspect summary statistics and schema information.
* Prepare combined data for downstream exploratory analysis and modeling.
* Add gait speed metadata parsed from file names.

### 3. Exploratory data analysis

* Review gait feature distributions.
* Compare movement patterns across observations.
* Visualize relationships between gait variables.

### 4. Feature engineering and modeling

* Build gait-related feature sets.
* Train and compare baseline classifiers, including:
  * Logistic Regression
  * Decision Tree
  * Random Forest

### 5. Model evaluation

Model performance is assessed with common classification metrics such as:

* Accuracy
* Precision
* Recall
* F1-score

---

## 🛠 Tech Stack

* **Language:** Python
* **Environment:** Jupyter Notebook
* **Primary libraries:** pandas, numpy, matplotlib, seaborn, scikit-learn

Install the Python dependencies with:

```bash
pip install -r requirements.txt
```

---

## 📂 Repository Contents

```text
gaitsync-gait-analysis-ml/
├── README.md
├── requirements.txt
├── gait phase analysis.ipynb
├── gait phase analysis.html
├── gaitphase notebook.ipynb
├── gaitphase notebook.html
├── GaitPhase_Desc.pdf
├── gait phase report.pdf
├── gait phase report.docx
├── final report.docx
├── research paper.docx
├── dissertation and research paper.docx
├── RESEARCH PRESENTATION part II.pptx
└── supporting proposal, dataset-description, novelty, and reflective-essay documents
```

> **Note:** The dataset archive and extracted data folder are not currently committed in this repository. The notebooks expect a local `gait.zip` file and/or an extracted marker dataset folder before all notebook cells can be executed end-to-end.

---

## 🚀 How to Run the Notebook

1. Clone the repository.
2. Install the dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Place the gait dataset archive at the repository root as `gait.zip`, or update the dataset path in the notebook to match your local extracted dataset location.
4. Start Jupyter:

   ```bash
   jupyter notebook
   ```

5. Open one of the analysis notebooks:
   * `gait phase analysis.ipynb`
   * `gaitphase notebook.ipynb`

6. Run the cells in order.

---

## ⚠️ Current Reproducibility Notes

* The notebooks include local dataset paths such as `gait.zip` and `/mnt/data/gp_marker_dataset/gp_marker_dataset`.
* Update those paths before running on a different machine.
* The committed repository does not include `gait.zip`, extracted CSV files, or a `data/` folder.
* If large datasets are added later, keep them outside Git or track them with a dedicated data-versioning workflow.

---

## 📈 Real-World Applications

* Early screening support for movement disorders
* Rehabilitation monitoring
* Sports performance analysis
* Wearable health analytics

---

## 🔥 Future Improvements

* Standardize notebook paths with configurable environment variables.
* Add a small sample dataset for reproducible tests.
* Convert reusable notebook logic into Python modules.
* Add automated model-training and evaluation scripts.
* Explore time-series/deep-learning models such as LSTM or CNN architectures.

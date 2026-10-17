# 🦿 GaitSync: Gait Analysis using Machine Learning

MSc dissertation, *Gait Analysis Using Machine Learning Classifiers*, MSc Internet of Things and Future Networks, Queen Mary University of London (2023–24).

## 🚀 Project Overview

This project classifies walking speed from laboratory gait data recorded with **optical motion capture**. It compares eight families of machine-learning classifier on about 3 million motion-capture frames.

> **Important:** the data are **optical motion-capture marker trajectories** recorded in a laboratory. They are **not** wearable, gyroscope or IMU data. The repository name comes from an early project idea for a gyroscope-based rehabilitation system (see `initial_project_idea_gyroscope_NOT_USED.docx`). That idea was not carried out, and the dissertation used the public GaitPhase database instead.

---

## 📊 Data: GaitPhase database (Hebenstreit et al., FAU Erlangen-Nürnberg, 2014)

* 21 healthy young adults (10 male, 11 female; mean age 23.8 years); subject IDs GP1–GP22, with GP4 not included in the released data
* Walking on an instrumented **split-belt treadmill** at **12 speeds** from 0.6 to 1.7 m/s (0.1 m/s steps), one minute per speed
* **Qualisys optical motion capture** (infrared cameras) at **200 Hz**. Reflective markers on the shoes at the heel (FCC) and the 1st, 2nd and 5th metatarsal heads (FM1, FM2, FM5) of both feet give 24 coordinate columns.
* Treadmill force plates at 1000 Hz are included in the database but were **not** used in this project; see the follow-up project below.
* 252 marker files (21 participants × 12 speeds) × 12,000 frames = **3,024,000 frames**

The dataset is not committed to this repository. See `GaitPhase_Desc.pdf` for the original description.

---

## 🧠 Method (as implemented in `gaitphase notebook.ipynb`)

1. Concatenate the marker files and take the speed from each file name.
2. Mean-impute the few missing marker values.
3. Features: 24 raw coordinates, 12 within-foot marker distances and 8 marker velocities (frame-to-frame displacement), giving 44 features.
4. StandardScaler, then PCA keeping 95% of the variance (12 components).
5. Label: five speed bands — Very Slow (0.6–0.8), Slow (0.9–1.0), Medium (1.1–1.2), Fast (1.3–1.5), Very Fast (1.6–1.7 m/s).
6. Random 75/25 train/test split **by frame**.
7. Classifiers: Random Forest, SVM (RBF kernel, trained in 10,000-row chunks), k-Nearest Neighbours, a neural network (Keras MLP), Decision Tree, Gradient Boosting, Logistic Regression (plain, L1, L2 and class-balanced) and Gaussian Naive Bayes.

## 📈 Results (test accuracy, from the notebook outputs)

| Model | Accuracy |
|---|---|
| Random Forest | 98.9% |
| SVM (chunked) | 98.1% |
| k-Nearest Neighbours | 98.1% |
| Neural network | 96.6% |
| Decision Tree | 93.5% |
| Gradient Boosting | 70.6% |
| Logistic Regression | 40–47% |
| Gaussian Naive Bayes | 45.3% |

## ⚠️ Limitations: why these accuracies are optimistic

* The split was **random by frame**, so frames a few milliseconds apart from the **same person and the same walk** appear in both training and test sets. The results therefore do not show how the models perform on new people.
* Scaling and PCA were fitted on all the data before the split.
* Each recording has a single speed label, so models can partly learn which recording a frame belongs to.
* All participants were healthy young adults walking on a treadmill.

The correct approach is participant-level validation (leave-one-subject-out), with all preprocessing fitted inside the training folds. The follow-up project does this.

## 🔁 Follow-up project

**[gait-speed-predictor](https://github.com/jumma786/gait-speed-predictor)** uses the same database's **force-plate** data. It predicts walking speed (regression) with leave-one-subject-out validation across 21 folds and adds SHAP explanations. Random Forest reaches a mean absolute error of 0.057 m/s (R² 0.958), with ridge regression almost as accurate (0.058 m/s).

---

## 📂 Repository Contents

| File | What it is |
|---|---|
| `gaitphase notebook.ipynb` / `.html` | Main analysis notebook with outputs |
| `gait phase analysis.ipynb` / `.html` | Earlier run of the same analysis |
| `final report.docx`, `gait phase report.docx` / `.pdf` | Dissertation report |
| `RESEARCH PRESENTATION part II.pptx` | Presentation |
| `Gait Proposal.docx` | Project proposal |
| `dataset description.docx`, `GaitPhase_Desc.pdf` | Dataset description |
| `research paper.docx`, `novelty.docx` | Supporting write-ups |
| `REFLECTIVE ESSAY.docx`, `reflective essay II.docx`, `gait phase reflective essay.pdf` | Reflective essays |
| `initial_project_idea_gyroscope_NOT_USED.docx` | Early project idea (gyroscope rehabilitation system); not the data or method used |

## 🛠 Tech Stack

Python, Jupyter, pandas, NumPy, matplotlib, seaborn, scikit-learn and TensorFlow/Keras.

```bash
pip install -r requirements.txt
jupyter notebook
```

The notebooks expect a local `gait.zip` or an extracted GaitPhase marker folder. Update the dataset paths before running them.

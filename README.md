# MediPredict

Healthcare Prediction System Using Machine Learning & Streamlit

## Project Overview

A small educational project for learning how to prepare structured healthcare
features, train machine-learning models, and build a Streamlit application for
exploring model outputs. Developed collaboratively by Arnav Meghlan, Advay Sinha, and Himanshu Bulani
as a learning exercise, it connects a Python inference pipeline to a simple interactive dashboard.

The application explores four intended tasks: readmission within 30 days,
length-of-stay bands, medication change, and diagnosis grouping. Outputs are
experimental; their labels, reliability, and clinical usefulness have not been
independently validated. No accuracy or performance scores are claimed.

## Learning Objectives

- Prepare numeric and categorical features using pandas and NumPy.
- Understand preprocessing, multi-output classification, and model serialization.
- Explore train/validation splitting, evaluation metrics, and decision thresholds.
- Connect an existing trained pipeline to a Streamlit interface.
- Present model outputs clearly and understand their limitations.

## Technologies Used

| Technology | Role |
| --- | --- |
| Python 3.12 | Application and training scripts |
| Streamlit | Interactive form, example profiles, tables, and charts |
| pandas and NumPy | Tabular inputs and numerical processing |
| scikit-learn | Preprocessing, multi-output classification, and evaluation |
| LightGBM | Estimators contained in the bundled trained pipeline |
| Random Forest | Estimator used by the current optional training script |
| cloudpickle and joblib | Model serialization and supporting ML utilities |

## Implemented Features

- Structured input form for demographic bands, admission details, utilization,
  laboratory categories, diagnosis codes, and medication status.
- Built-in example profiles for exploring the dashboard.
- Input preparation and loading of the existing trained model and metadata.
- Model scoring with configurable thresholds for the two intended binary tasks.
- Summary cards, alternative labels, distribution charts, and raw JSON outputs.
- A separate script for centralized multi-output Random Forest training from a
  prepared CSV, including hold-out evaluation and binary-threshold search.

The bundled model uses LightGBM; the current Random Forest trainer is a separate
learning workflow. Federated learning and the other items under **Future
Enhancements** are proposed work.

## Machine-Learning Workflow

1. **Prepare data:** supply authorized tabular data with the features and target
   columns expected by the training script. No training dataset is included.
2. **Prepare features:** normalize supported values, derive utilization totals
   and diagnosis prefixes, and encode categorical features.
3. **Train and evaluate:** the optional trainer splits the data, fits a
   multi-output Random Forest pipeline, computes hold-out metrics, and searches
   thresholds for binary tasks.
4. **Save artifacts:** write the pipeline, metadata, and numeric feature medians
   to a separate experiment directory.
5. **Explore inference:** the Streamlit app prepares a single example, loads the
   bundled artifacts, and displays model outputs.

This describes the implemented workflow, not a reproduced training experiment.
Model training and evaluation were not rerun during publication preparation.
Any future model replacement requires checking feature and target definitions
against inference. Keep the bundled artifacts intact while experimenting.

## Project Structure

```text
MediPredict/
├── app/
│   ├── dashboard.py          # Streamlit application
│   └── inference.py          # Input preparation and model scoring
├── models/
│   ├── multi_pipeline.pkl    # Existing trained pipeline
│   └── meta.json             # Feature and label metadata
├── training/
│   └── train_pipeline.py     # Optional centralized training workflow
├── docs/
│   ├── Healthcare_ML_Learning_Report.docx
│   └── Healthcare_ML_Learning_Presentation.pptx
├── requirements.txt
├── WINDOWS_VSCODE_GUIDE.txt
└── README.md
```

The documents in `docs/` are public editions with student identifiers and
personal contact metadata removed, and implemented and proposed work separated.

[Project report](docs/Healthcare_ML_Learning_Report.docx) ·
[Presentation](docs/Healthcare_ML_Learning_Presentation.pptx)

## Installation

Use Python 3.12 and run these commands from the project root:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

On macOS/Linux, activate the environment with `source .venv/bin/activate`, then
run the same dependency installation command. Keep the declared dependency pins;
the serialized pipeline records scikit-learn 1.6.1. Some supporting dependencies
are unpinned, so resolved versions may vary.

## Run the Streamlit Application

```powershell
python -m streamlit run app/dashboard.py
```

Open the local address printed by Streamlit. Use the built-in profiles or enter
fictional encounter details, adjust thresholds, and select **Run prediction**.
Keep both supplied files in `models/`; no dataset is needed to run the demo.
Only load trusted model artifacts because pickle-based files can execute code.

To inspect the optional trainer's arguments without training:

```powershell
python -m training.train_pipeline --help
```

Keep datasets outside Git and write future experiments to a separate output
folder, such as `models/learning_run/`.

## Future Enhancements

These capabilities are proposed and have not been implemented or demonstrated:

- A federated-learning simulation with separate clients, server coordination,
  and an aggregation method appropriate to the chosen model.
- Additional model families and reproducible comparisons on authorized datasets.
- More complete validation of target definitions, label mappings, calibration,
  and performance across different groups.
- Improved analytics, explanatory views, and model-comparison dashboards.
- Research into differential privacy and secure aggregation, with explicit
  threat modeling and evaluation.
- Deployment, access controls, and privacy reviews appropriate to any future
  hosted educational demonstration.

## Educational-Use Disclaimer

This project is for learning and demonstration. Predictions, displayed labels,
model scores, and heuristic bands are experimental and must not be used for
clinical decisions, diagnosis, treatment, or patient triage. Use fictional input
examples only. The project makes no claim of clinical validation, regulatory
compliance, privacy guarantees, or measured accuracy.

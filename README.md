# EV Battery Health and Remaining Useful Life Prediction

## Overview

This project focuses on predicting the **Remaining Useful Life (RUL)** of lithium-ion batteries using machine learning.

Battery degradation is an important problem in electric vehicles and energy storage systems because accurate estimation of battery health and remaining useful life can support predictive maintenance, reliability analysis, and battery management decisions.

The project uses the **NASA Li-ion Battery Aging Dataset** and develops a machine learning pipeline for battery degradation analysis and RUL prediction.

The analysis includes:

- Battery capacity degradation analysis
- State of Health (SOH) calculation
- Discharge-cycle feature extraction
- Remaining Useful Life (RUL) calculation
- Time-based model evaluation
- Linear Regression as a baseline model
- XGBoost Regression as the final machine learning model
- Cross-battery evaluation
- Feature importance analysis
- Prediction error analysis

---

## Project Objectives

The main objectives of this project are:

1. Analyze lithium-ion battery degradation over repeated charge/discharge cycles.
2. Estimate battery State of Health (SOH).
3. Calculate Remaining Useful Life (RUL) using an End-of-Life capacity threshold.
4. Develop a baseline regression model for RUL prediction.
5. Develop an XGBoost regression model for RUL prediction.
6. Evaluate model performance using MAE, RMSE, and R².
7. Test model generalization across different batteries.
8. Identify important battery-related features influencing RUL predictions.

---

## Dataset

This project uses the **NASA Li-ion Battery Aging Dataset** from the NASA Prognostics Center of Excellence.

The dataset contains measurements from lithium-ion battery aging experiments, including charging, discharging, voltage, current, temperature, and capacity measurements.

The NASA dataset defines End of Life (EOL) at approximately **30% capacity degradation**, corresponding to a decrease from the rated 2 Ah capacity to approximately 1.4 Ah.

### Dataset Source

NASA Open Data:

https://data.nasa.gov/dataset/li-ion-battery-aging-datasets

NASA Prognostics Center of Excellence:

https://www.nasa.gov/intelligent-systems-division/discovery-and-systems-health/pcoe/pcoe-data-set-repository/

### Batteries Used

The analysis uses:

- B0005
- B0006
- B0018

The original NASA dataset files are not included in this repository because of their large size.

---

## Methodology

The project follows the workflow below:

```text
NASA Battery Dataset
        ↓
Data Loading
        ↓
Battery Cycle Extraction
        ↓
Data Cleaning
        ↓
Exploratory Data Analysis
        ↓
Capacity Degradation Analysis
        ↓
SOH Calculation
        ↓
Feature Engineering
        ↓
RUL Calculation
        ↓
Time-Based Data Split
        ↓
Linear Regression Baseline
        ↓
XGBoost Regression

Battery Health Analysis

Battery capacity is analyzed across discharge cycles to understand degradation behavior.

State of Health (SOH) is calculated relative to the initial observed battery capacity:
SOH (%) = (Current Capacity / Initial Capacity) × 100
The project visualizes:

Battery capacity degradation
SOH degradation
EOL threshold
Battery cycle progression

Feature Engineering

Features are extracted from discharge-cycle measurements.

The following features are used for RUL prediction:

Cycle
Mean Voltage
Minimum Voltage
Maximum Voltage
Mean Current
Mean Temperature
Maximum Temperature

These features provide information about battery operating conditions and degradation behavior.

Remaining Useful Life Calculation

RUL is defined as the number of remaining cycles until the battery reaches the End-of-Life capacity threshold.

For this project:
EOL Capacity = 1.4 Ah
RUL is calculated as:
RUL = EOL Cycle - Current Cycle
This produces a cycle-based prediction target for the regression models.

Machine Learning Models
1. Linear Regression

Linear Regression is used as a baseline model.

It provides a simple reference point for evaluating whether a more advanced machine learning model can improve RUL prediction.

2. XGBoost Regression

XGBoost Regression is used as the final machine learning model.

XGBoost was selected because it can model nonlinear relationships between battery measurements and remaining useful life.

The model uses:

200 estimators
Maximum tree depth of 4
Learning rate of 0.05
Subsampling
Feature subsampling
Squared-error regression objective
Model Evaluation

The models are evaluated using the following metrics:

Mean Absolute Error (MAE)

Measures the average absolute difference between predicted and actual RUL.

Root Mean Squared Error (RMSE)

Measures prediction error while giving greater weight to larger errors.

R² Score

Measures how well the model explains the variation in the target variable.

The project also includes:

Actual vs predicted RUL plots
Prediction error analysis
Largest prediction error analysis
Cross-battery performance comparison
Feature importance analysis
Cross-Battery Evaluation

A key part of this project is evaluating model generalization across different batteries.

The model is trained using battery degradation data and evaluated on batteries that were not used for model training.

This provides a more realistic test of whether the learned relationships can generalize beyond a single battery.

Explainability

XGBoost feature importance is used to identify which battery measurements contribute most to RUL prediction.

This helps connect the machine learning results with the physical battery degradation process.

Technologies Used
Python
Pandas
NumPy
Matplotlib
SciPy
Scikit-learn
XGBoost
Joblib
Google Colab
GitHub

Repository Structure
ev-battery-rul-prediction/
│
├── EV_Battery_RUL_Prediction.ipynb
├── requirements.txt
├── README.md
├── .gitignore
│
└── data/
    └── README.md

The original NASA dataset is not stored in this repository because of its large file size.

How to Run
1. Download the Dataset

Download the NASA Li-ion Battery Aging Dataset from the official NASA source.

2. Open the Notebook

Open:EV_Battery_RUL_Prediction.ipynb

3. Install Dependencies

Install the required Python packages:pip install -r requirements.txt

4. Load the Dataset

Place the extracted NASA battery files in the appropriate working directory and update the file paths in the notebook if necessary.

5. Run the Notebook

Execute the notebook cells sequentially to reproduce:

Battery degradation analysis
SOH calculation
RUL calculation
Model training
Model evaluation
Cross-battery predictions
Feature importance analysis


Results

The project compares Linear Regression and XGBoost Regression using:

MAE
RMSE
R² Score

The notebook contains the complete numerical results and visual evaluation for the analyzed batteries.

The final model evaluation is performed across multiple battery datasets to examine prediction performance and generalization.

Key Takeaways
Lithium-ion batteries show measurable capacity degradation over repeated cycles.
Battery operating measurements can be used to estimate remaining useful life.
SOH provides a useful representation of battery degradation.
XGBoost can capture nonlinear relationships between battery measurements and RUL.
Cross-battery evaluation provides additional insight into model generalization.
Feature importance analysis helps interpret the machine learning predictions.
Limitations

This project has several limitations:

The NASA dataset represents controlled battery aging experiments rather than real-world EV fleet data.
Only selected battery files are used for the analysis.
The current model uses engineered summary statistics from discharge cycles.
Battery chemistry, environmental conditions, and usage patterns can affect degradation behavior.
The model should not be interpreted as a production-ready battery management system without further validation.
Future Improvements

Possible future improvements include:

Incorporating additional NASA battery datasets
Using voltage/current time-series features
Adding impedance-based features
Testing Random Forest and other regression models
Hyperparameter optimization
Using recurrent neural networks such as LSTM
Developing a more advanced time-series degradation model
Evaluating the model on additional battery datasets
Deploying the trained model as an API or interactive dashboard
Author

Tharun Kumar V G

MSc Data Science
University of Europe for Applied Sciences, Germany

GitHub: tharunkumarvg-lab
### Important

When you paste this into GitHub, **paste the entire block including all the `##` headings and the ``` marks**. GitHub will then render it properly.

Your previous version had the `Methodology` code block swallowing everything after it. **This version fixes that.**
        ↓
Cross-Battery Evaluation
        ↓
Feature Importance Analysis
        ↓
Prediction Error Analysis

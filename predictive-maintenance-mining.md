# Predictive Maintenance for Industrial Equipment

## Project Overview

This project develops machine learning models for predictive maintenance using industrial sensor telemetry data. The objective is to predict machine failures before they occur, enabling proactive maintenance planning and reducing unplanned downtime.

The workflow is framed around mining and heavy industrial equipment such as conveyor systems, crushers, pumps, haul trucks, and rotating machinery.

---

## Dataset

- Dataset: AI4I 2020 Predictive Maintenance Dataset
- Records: 10,000
- Target: `Machine failure`
- Failure rate: 3.39%
- Non-failure rate: 96.61%

The dataset is highly imbalanced, which makes accuracy alone insufficient for model evaluation.

---

## Exploratory Data Analysis

### Sensor Distributions

<img width="1500" height="1000" alt="image" src="https://github.com/user-attachments/assets/8e974a27-2e43-48a7-9126-3935a6adc5a6" />

### Failure Class Distribution

<img width="800" height="500" alt="image" src="https://github.com/user-attachments/assets/6106bb34-151f-4a4a-bc25-627f256532ed" />


Key observations:

- Machine failures are rare events.
- Rotational speed shows a long-tailed distribution.
- Torque approximately follows a normal distribution.
- Tool wear and temperature-related variables are relevant to equipment degradation.

---

## Feature Engineering

The following engineered features were added:

```python
temp_diff = process_temperature - air_temperature
power_proxy = torque * rotational_speed
wear_speed_interaction = tool_wear * rotational_speed
```

These features capture thermal stress, mechanical load, and the interaction between equipment wear and operating intensity.

---

## Models

Three supervised learning models were compared:

- Logistic Regression
- Random Forest
- Gradient Boosting

SMOTE was applied during training to address the severe class imbalance.

---

## Model Performance

| Model | ROC-AUC | PR-AUC | Failure Recall | Failure Precision |
|---|---:|---:|---:|---:|
| Logistic Regression | 0.916 | 0.383 | 0.765 | 0.208 |
| Random Forest | 0.974 | 0.776 | 0.765 | 0.553 |
| Gradient Boosting | 0.970 | 0.814 | 0.882 | 0.414 |

Gradient Boosting was selected as the final model because it achieved the highest PR-AUC and the strongest failure recall.

---

## Final Model Results

### Precision-Recall Curve

<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/5af1daa2-8d67-4f4f-a215-cfd943917a69" />

### ROC Curve

<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/a6d4ef06-8a9c-4f00-a313-aec71088ee78" />

### Confusion Matrix

<img width="600" height="500" alt="image" src="https://github.com/user-attachments/assets/2ceb374c-85c8-4402-979c-114ff691439e" />


The Gradient Boosting model detected 60 out of 68 failure cases in the test set, reducing false negatives to 8.

---

## Feature Importance

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/6a85f31e-12f5-46f9-989c-0ee21c6de838" />

The most important predictors were:

- Rotational speed
- Tool wear
- Torque
- Temperature difference
- Power proxy

These features align with real-world mechanical stress, equipment degradation, and abnormal operating conditions.

---

## Explainability with SHAP

<img width="775" height="541" alt="image" src="https://github.com/user-attachments/assets/7a4091c3-439f-438d-b3ba-3938772c8acd" />

SHAP analysis was used to understand how each feature influenced model predictions.

Key insights:

- High rotational speed increased predicted failure risk.
- High tool wear strongly increased predicted failure probability.
- Torque and power-related features contributed to identifying high-risk operating conditions.
- Temperature difference helped capture abnormal thermal behaviour.

---

## Business Interpretation

In a mining or heavy industrial setting, the cost of missing a machine failure can be much higher than the cost of investigating a false alarm. Therefore, the Gradient Boosting model is useful because it prioritizes failure detection and achieves high recall.

This type of predictive maintenance workflow could support maintenance teams by identifying high-risk equipment before breakdowns occur.

---

## Technologies Used

- Python
- pandas
- NumPy
- scikit-learn
- imbalanced-learn
- matplotlib
- seaborn
- SHAP

---

## Future Improvements

Potential extensions include:

- Hyperparameter tuning with GridSearchCV
- Threshold optimization for different maintenance-risk tolerances
- Streamlit dashboard for interactive failure-risk prediction
- Multi-class or multi-label prediction of specific failure types
- Testing the workflow on real industrial sensor data

---

## Repository Structure

```text
predictive-maintenance-mining/
├── data/
│   └── ai4i2020.csv
├── results/
│   └── figures/
├── src/
│   ├── preprocessing.py
│   └── model.py
├── main.py
├── requirements.txt
└── README.md
```

---

## How to Run

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python main.py
```

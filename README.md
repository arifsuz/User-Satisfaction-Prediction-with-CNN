# User Satisfaction Prediction with CNN

This project implements a **Convolutional Neural Network (CNN)** to predict user satisfaction based on usability survey data. The main program is provided in `main.ipynb`. The dataset, `Dataset_Quiz.csv`, contains survey results from different user roles (Student, Lecturer), tasks, and academic fields.

---

## Directory Structure

```
Machine Learning/
├── Dataset_Quiz.csv
├── main.ipynb
├── LICENSE
├── requirements.txt
└── README.md
```

---

## Setup & Installation

1. **Clone the Repository**
   ```sh
   git clone <repository_url>
   cd "Machine Learning"
   ```

2. **Create and Activate Virtual Environment (Recommended)**
   ```sh
   python -m venv venv
   venv\Scripts\activate
   ```

3. **Install Required Modules**
   Install all dependencies using the provided `requirements.txt`:
   ```sh
   pip install -r requirements.txt
   ```

4. **Start Jupyter Notebook**
   ```sh
   jupyter notebook
   ```
   Then open main.ipynb and run all cells in order.

---

## Workflow Summary

### 1. Data Loading & Preprocessing

- **Load Data:** Read Dataset_Quiz.csv using a semicolon (`;`) delimiter.
- **Data Cleaning:** Convert numeric columns (`CR`, `TD`, `Lostness`, `SUS`) to float, replacing commas with dots for decimal points.
- **Class Filtering:** Use only rows with `Class` -1 (Negative) and 1 (Positive).
- **Categorical Encoding:** Encode `Actors`, `Task Name`, and `Fields` using `LabelEncoder`.
- **Normalization:** Normalize numeric features with `StandardScaler`.
- **Reshape for CNN:** Transform data to 3D shape `(samples, features, 1)` for CNN input.

### 2. CNN Model Construction

- **Architecture:** 
  - Two `Conv1D` layers (64 & 128 filters) + `BatchNormalization` + `Dropout`
  - `Flatten` + `Dense` (128 units) + `Dropout`
  - Output: `Dense(1, activation='sigmoid')`
- **Compilation:** Adam optimizer, `binary_crossentropy` loss, accuracy metric.
- **Early Stopping:** Prevents overfitting by monitoring validation loss.

### 3. Training & Validation

- **Data Split:** 80% training, 20% testing (stratified).
- **Training:** Up to 50 epochs, batch size 32, with 20% validation split.
- **Visualization:** Plot training and validation accuracy/loss curves.

### 4. Prediction & Analysis

- **Prediction:** Model predicts on the entire dataset.
- **SUS Grouping:** Create `SUS > 70` and `SUS < 70` groups.
- **Mapping:** Map task and field codes to readable labels.
- **Summary Table:** Generate summary tables by actor, field, task, and SUS group.
- **Visualization:** 
  - Class distribution (True vs Predicted)
  - Satisfaction prediction tables per actor

### 5. Model Evaluation

- **Classification Report:** Precision, recall, f1-score, accuracy.
- **Confusion Matrix:** Heatmap visualization.
- **ROC Curve & AUC:** Evaluate model discrimination ability.

---

## Dataset Description

- **Actors:** User role (Student/Lecturer)
- **Task Name:** Task identifier (Task-1 to Task-5)
- **Fields:** Academic field (CS, Mn, En, Ac)
- **CR, TD, Lostness, SUS:** Usability measurement metrics
- **Class:** Target label (-1 = Negative, 1 = Positive)

---

## Results & Insights

- **Model Accuracy:** ~90% on test data, ROC AUC ~0.95
- **Effective at distinguishing satisfied/unsatisfied users**
- **Granular analysis:** Summary tables by actor, field, task, and SUS group
- **Visualizations:** Help identify usability improvement areas

---

## Development Notes

- The model can be further improved with data balancing, hyperparameter tuning, or alternative architectures.
- Granular analysis enables targeted recommendations for system improvements based on user groups.

---

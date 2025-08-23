# Scratch Detection Assignment

## Overview
This project addresses the challenge of **detecting scratches on semiconductor wafer maps** using both classical analysis and deep learning. The solution transforms die-level manufacturing data into **72×72 image grids** and applies a **U-Net segmentation model** to predict scratch locations.  

The assignment includes data exploration, preprocessing, model building, evaluation, and final submission generation.

---

## Project Structure
```
scratch_detection_assignment.ipynb   # Main notebook (EDA, preprocessing, model training, results)
data/                                # Input wafer datasets (not included here)
models/                              # Saved model weights
results/                             # Output plots, confusion matrices, predictions
README.md                            # Project description
```

---

## ⚙Workflow

### 1. Exploratory Data Analysis (EDA)
- Distribution of wafer yields across training and test sets.  
- Defect and scratch rates by wafer size.  
- Wafer map visualization (good dies, bad dies, scratches, ink).  

### 2. Preprocessing
- Convert die-level wafer data to **72×72 images**:
  - **Images**: mark defective dies.  
  - **Labels**: mark scratch locations.  
  - **Masks**: valid die positions.  
- Ensures wafers with different sizes are mapped consistently.

### 3. Model Building
- **U-Net CNN architecture** for segmentation.  
- Loss function: Binary Cross-Entropy (BCE) + Dice loss (weighted).  
- Hyperparameter tuning with 5-fold cross-validation:  
  - Different `dice_weight` values.  
  - Multiple prediction thresholds.

### 4. Evaluation
- Metrics: Precision, Recall, F1-score, Dice coefficient.  
- Confusion matrices for each fold.  
- Precision–Recall curves across thresholds.  
- Business-driven adjustment: wafers with yield < 88% classified as **scratch-free** to reduce false positives.

### 5. Results
- Optimal parameters:  
  - **dice_weight = 0.0**  
  - **threshold ≈ 0.55–0.65**  
- Model achieved balanced performance with emphasis on **precision** (reducing false scratch detections).  
- Predicted scratch masks were exported to CSV for submission.

---

## How to Run
1. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
2. Open the notebook:
   ```bash
   jupyter notebook scratch_detection_assignment.ipynb
   ```
3. Run cells in order:  
   - Data loading → EDA → Preprocessing → Model training → Evaluation → Submission.

---

## Requirements
- Python 3.9+  
- Jupyter Notebook  
- Libraries:  
  - `pandas`, `numpy`, `matplotlib`, `seaborn`  
  - `scikit-learn`  
  - `torch` (PyTorch)  

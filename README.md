# 🏠 House Price Predictor

A machine learning project that predicts house prices using the Ames Housing dataset. Trained and compared 3 models — Linear Regression, Random Forest, and XGBoost — achieving an R² score of **0.9354** with XGBoost.

---

## 📊 Results

| Model | RMSE | R² Score |
|---|---|---|
| Linear Regression | 0.1288 | 0.9103 |
| Random Forest | 0.1230 | 0.9182 |
| **XGBoost** | **0.1093** | **0.9354** ✅ |

> The final XGBoost model predicts house prices within an average error of **$18,844** on a mean house price of **$172,407**.

---

## 📁 Project Structure

```
house-price-predictor/
├── data/
│   └── AmesHousing.csv        ← Dataset
├── notebooks/
│   └── house_price_predictor.ipynb   ← Main notebook
├── src/
│   └── house_price_model.pkl  ← Saved XGBoost model
└── README.md
```

---

## 🔧 Tech Stack

- **Python 3.12**
- **Pandas & NumPy** — data manipulation
- **Matplotlib & Seaborn** — visualizations
- **Scikit-learn** — Linear Regression, Random Forest, preprocessing
- **XGBoost** — best performing model

---

## 🚀 How to Run

**1. Clone the repo**
```bash
git clone https://github.com/yourusername/house-price-predictor.git
cd house-price-predictor
```

**2. Create virtual environment**
```bash
python -m venv venv
venv\Scripts\activate      # Windows
source venv/bin/activate   # Mac/Linux
```

**3. Install dependencies**
```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost joblib
```

**4. Download the dataset**
- Download from [Kaggle - Ames Housing Dataset](https://www.kaggle.com/datasets/prevek18/ames-housing-dataset)
- Place `AmesHousing.csv` inside the `data/` folder

**5. Run the notebook**
- Open `notebooks/house_price_predictor.ipynb` in VS Code
- Run all cells top to bottom

---

## 📌 Key Steps

### 1. Exploratory Data Analysis (EDA)
- Dataset: 2930 rows, 82 columns
- Identified and visualized missing values
- Discovered SalePrice is highly right-skewed (skewness = 1.74)
- Applied log transformation to normalize target variable (skewness → -0.01)

### 2. Data Cleaning
- Filled high missing % columns (Pool QC, Alley, Fence etc.) with `'None'` — house simply doesn't have that feature
- Filled numeric garage/basement columns with `0`
- Filled Lot Frontage using neighborhood median
- Remaining numerics → median, categoricals → mode

### 3. Feature Engineering
Created 7 new features that improved model performance:
| Feature | Description |
|---|---|
| `TotalSF` | Total square footage (basement + 1st + 2nd floor) |
| `TotalBaths` | Weighted total bathrooms |
| `HouseAge` | Age of house at time of sale |
| `RemodAge` | Years since last remodel |
| `IsRemodeled` | Whether house was ever remodeled |
| `IsNew` | Whether house was sold same year it was built |
| `TotalPorch` | Total porch area |

### 4. Model Training
- Train/Test split: 80/20
- Trained 3 models and compared performance
- Applied log transformation on target variable for all models

### 5. Feature Importance (XGBoost)
Top 3 most important features:
1. **Overall Qual** (0.2288) — overall material & finish quality
2. **TotalSF** (0.1276) — our custom engineered feature ✅
3. **Central Air** (0.0907) — presence of central air conditioning

---

## 💡 Key Learnings

- Log transforming a skewed target variable significantly improves model performance
- Feature engineering (`TotalSF`) became the 2nd most important feature in the final model
- XGBoost outperforms Linear Regression and Random Forest on tabular data due to its sequential boosting approach
- Filling missing values with domain knowledge (e.g. `None` for no garage) is better than dropping rows

---

## 📈 Future Improvements

- [ ] Hyperparameter tuning with GridSearchCV
- [ ] Try Lasso/Ridge regression for feature selection
- [ ] Deploy model as a REST API using FastAPI
- [ ] Build a simple web UI with Streamlit

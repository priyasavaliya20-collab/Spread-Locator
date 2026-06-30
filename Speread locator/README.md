<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,11,20&height=200&section=header&text=Spread%20Locator&fontSize=42&fontColor=fff&animation=twinkling&fontAlignY=35&desc=A%20Statistical%20Distribution%20Analysis%20Model%20Data&descAlignY=58&descSize=18" />
</div>

---

This project presents a comprehensive Theory + Practical Statistics Analysis on a real-world transaction dataset containing 500 records. The objective is to apply Inferential Statistics and Hypothesis Testing techniques to analyze transactional patterns, evaluate statistical relationships, and derive meaningful business insights from the data.

The project combines statistical theory with practical implementation in Python (Jupyter Notebook), covering the complete analytical workflow from data preprocessing and exploratory data analysis (EDA) to hypothesis testing, visualization, and interpretation of results.

---

## 🎯 Objective

To apply statistical distribution concepts and inferential statistics techniques on a real healthcare dataset and derive **evidence-based, data-driven insights** using Python.

---

## 🗂️ Project Files

| File | Description |
|------|-------------|
| 📓 `spread_locator.ipynb` | Complete statistical analysis notebook (Part B) |
| 📊 `spread_locator_dataset.xlsx` | transaction dataset — containing 500 records|
| 📄 `Part_A_Theory.pdf` | Theoretical foundations, formulas & visual explanations |
| 📘 `README.md` | Project documentation (this file) |

---

## 🛠️ Tools & Libraries

![Python](https://img.shields.io/badge/Python-3.x-blue?style=flat-square&logo=python)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?style=flat-square&logo=jupyter)
![Pandas](https://img.shields.io/badge/Pandas-Data_Analysis-green?style=flat-square)
![NumPy](https://img.shields.io/badge/NumPy-Numerical-blue?style=flat-square)
![SciPy](https://img.shields.io/badge/SciPy-Statistics-purple?style=flat-square)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-red?style=flat-square)

```
pip install pandas numpy scipy matplotlib openpyxl
```

---

## 📗 Part A — Theoretical Foundation (11 Topics)

## Q1. What is Statistical Distributions?
 
 <img width="1662" height="590" alt="Q1" src="https://github.com/user-attachments/assets/98589a90-c47f-4ec8-a2dd-0ebaa369c4fa" />

## Q2. What is a Q-Q Plot and why is it used?

<img width="1642" height="577" alt="Q2" src="https://github.com/user-attachments/assets/53b901ca-31c3-4f25-a7bc-74d2a7e756f6" />


## Q3. Difference between Discrete and Continuous Distributions.

<img width="1638" height="582" alt="Q3" src="https://github.com/user-attachments/assets/9befb63d-27ea-43f1-b6e0-64ba6757e8b2" />


## Q4. What is Bernoulli Distribution?

<img width="1493" height="612" alt="Q4" src="https://github.com/user-attachments/assets/0a281323-db84-4645-84bd-d34a9ff95c50" />


## Q5. What is Binomial Distribution?

<img width="1640" height="622" alt="Q5" src="https://github.com/user-attachments/assets/756ff91a-8818-4fb6-be89-65dfa95c986c" />


## Q6. Explain Log-Normal Distribution.

<img width="1642" height="598" alt="Q6" src="https://github.com/user-attachments/assets/3ac28231-0735-4e51-9994-ff95b9a88fe6" />


## Q7. Explain Power Law Distribution.

<img width="1641" height="612" alt="Q7" src="https://github.com/user-attachments/assets/1940d1c0-9b0a-4483-89ed-e8efbe7e8b04" />



## Q8. What is Box-Cox Transform?

<img width="1637" height="606" alt="Q8" src="https://github.com/user-attachments/assets/ff6bc748-10f4-4026-be58-35a681d36852" />


## Q9. Explain Poisson Distribution with an example.

<img width="1642" height="613" alt="Q9" src="https://github.com/user-attachments/assets/7d17275a-0668-4a42-b447-d94a735da1ac" />


## Q10. What is Z-score Probability?

<img width="1633" height="622" alt="Q10" src="https://github.com/user-attachments/assets/1e0865a1-baf9-48ec-9cb0-afba320a0dc5" />


## Q11. Differentiate Probability Density Function (PDF) and Cumulative Distribution Function (CDF).

<img width="1642" height="602" alt="Q11" src="https://github.com/user-attachments/assets/523d3647-bb20-414b-92a1-d141a28b14d9" />

---

## 📗 Part B — Data Analysis & Hypothesis Testing

### Dataset Overview

```python
import pandas as pd
df = pd.read_excel("spread_locator_dataset.xlsx")
print(df.shape)        # (500, n_columns)
print(df.describe())   # Basic stats
```

---

### 🔬 Q1 — Hypothesis Testing (Chi-Square)

**Research Question:** Does smoking status influence diabetes prevalence?

| Hypothesis | Statement |
|------------|-----------|
| H₀ | Smoking has no effect on diabetes prevalence |
| H₁ | Smoking affects diabetes prevalence |

```python
from scipy.stats import chi2_contingency

table = pd.crosstab(df["Smoking_Status"], df["Diabetes"])
chi2_stat, p_value, dof, expected = chi2_contingency(table)

print(f"Chi-Square = {chi2_stat:.3f}")
print(f"P-Value    = {p_value:.3f}")
```

| Metric | Value |
|--------|-------|
| Chi-Square Statistic | 0.609 |
| p-value | 0.610 |
| Critical Value | 2.623 |

**✅ Conclusion:** p-value (0.610) >> 0.05 → **Fail to Reject H₀**  
Smoking status and diabetes prevalence are **statistically independent**.

---

### 📊 Q2 — Confidence Interval Analysis

**Formula:** CI = x̄ ± Z × (σ / √n)

```python
import numpy as np

def confidence_interval(col, z=1.96):
    mean = col.mean()
    margin = z * (col.std() / np.sqrt(len(col)))
    return round(mean - margin, 2), round(mean + margin, 2)

print("Age CI   :", confidence_interval(df["Age"]))
print("Weight CI:", confidence_interval(df["Weight"]))
print("BP CI    :", confidence_interval(df["Blood_Pressure"]))
```

| Variable | 95% Confidence Interval |
|----------|------------------------|
| Age | 41.09 – 44.26 |
| Weight | 75.80 – 79.21 |
| Blood Pressure | 135.63 – 140.06 |

**✅ Conclusion:** Population estimates are reliable and precise.

---

### 📈 Q3 — Critical Value & p-value Decision Rule

```python
alpha = 0.05

def decision(p_val):
    return "Reject H₀ ✗" if p_val < alpha else "Fail to Reject H₀ ✓"
```

| Decision Rule | Condition |
|---------------|-----------|
| Reject H₀ | p-value < 0.05 |
| Fail to Reject H₀ | p-value ≥ 0.05 |

**✅ Conclusion:** Both critical value and p-value approaches give **consistent decisions**.

---

### 👨‍⚕️ Q4 — Independent Sample t-Test

**Objective:** Compare BMI between male and female patients.

**Formula:** t = (x̄₁ − x̄₂) / √(s₁²/n₁ + s₂²/n₂)

```python
from scipy.stats import ttest_ind

male   = df[df["Gender"] == "Male"]["BMI"]
female = df[df["Gender"] == "Female"]["BMI"]

t_stat, p = ttest_ind(male, female)
print(f"t-value = {t_stat:.3f}")
print(f"p-value = {p:.3f}")
```

| Metric | Value |
|--------|-------|
| t-value | 1.287 |
| p-value | 0.199 |
| Critical Value | 1.28 |

**✅ Conclusion:** p = 0.199 > 0.05 → Male and female BMI are **statistically similar**.

---

### 🔗 Q5 — Chi-Square Test (Smoking vs Diabetes)

**Formula:** χ² = Σ (O − E)² / E

```python
table = pd.crosstab(df["Smoking_Status"], df["Diabetes"])
chi2, p, dof, _ = chi2_contingency(table)
print(f"Chi-Square = {chi2:.3f}, p = {p:.3f}")
```

| Metric | Value |
|--------|-------|
| Chi-Square | 2.131 |
| p-value | 0.345 |

**✅ Conclusion:** No significant association between smoking status and diabetes.

---

### 📊 Q6 — ANOVA Test

**Objective:** Compare BMI across exercise frequency groups (Daily / Weekly / Rarely / Never).

**Formula:** F = Between-Group Variance / Within-Group Variance

```python
from scipy.stats import f_oneway

groups = [df[df["Exercise_Frequency"] == g]["BMI"] for g in ["Daily","Weekly","Rarely","Never"]]
F, p = f_oneway(*groups)
print(f"F-value = {F:.3f}, p-value = {p:.3f}")
```

| Metric | Value |
|--------|-------|
| F-value | 1.072 |
| p-value | 0.370 |
| Critical Value | 2.38 |

**✅ Conclusion:** Exercise frequency does **not** significantly affect BMI.

---

### 📈 Q7 — Correlation & Covariance Analysis

**Objective:** Analyze relationship between Age and BMI.

**Formula:** r = Cov(X,Y) / (σₓ · σᵧ)

```python
correlation = df["Age"].corr(df["BMI"])
covariance  = df["Age"].cov(df["BMI"])

print(f"Correlation (r) = {correlation:.3f}")
print(f"Covariance      = {covariance:.3f}")
```

| Metric | Value |
|--------|-------|
| Correlation (r) | 0.032 |
| Relationship | Very Weak Positive |

**✅ Conclusion:** Age and BMI are **not meaningfully correlated** (r ≈ 0 → only ~1% variance explained).

---

## 📊 Key Findings Summary

* Successfully analyzed 500 real-world transaction records using inferential statistical techniques.
* Identified meaningful patterns and trends across transaction amounts, customer activity, regions, and transaction status.
* Applied multiple hypothesis testing methods to determine statistically significant relationships between variables.
* Evaluated group differences using Independent Sample t-Test and One-Way ANOVA.
* Examined associations between categorical variables using the Chi-Square Test of Independence.
* Measured the strength and direction of relationships through Correlation and Covariance Analysis.
* Estimated population parameters using Confidence Intervals and interpreted results based on p-values and critical values.
* Created clear visualizations to support statistical findings and improve data interpretation.
* Demonstrated a complete end-to-end statistical analysis workflow, from data preprocessing to evidence-based conclusions using Python.
---

## 🎯 Final Conclusion

> This project successfully applied **Inferential Statistics** and **Hypothesis Testing** to a 500-record healthcare dataset.  
> Statistical analyses confirmed that smoking status, exercise frequency, and gender do not significantly affect the health metrics studied.  
> Age showed only a very weak relationship with BMI.  
> **Inferential statistics transformed raw healthcare data into actionable, evidence-based insights.**

---

## 🚀 How to Run

```bash
# 1. Install dependencies
pip install pandas numpy scipy matplotlib openpyxl

# 2. Launch Jupyter
jupyter notebook

# 3. Open and run
spread_locator.ipynb
```

---

## ✅ Project Checklist

- [x] Statistical Distribution Theory (11 Topics)
- [x] Hypothesis Testing
- [x] Confidence Intervals
- [x] Critical Values & p-value Analysis
- [x] Independent Sample t-Test
- [x] Chi-Square Test
- [x] ANOVA
- [x] Correlation & Covariance Analysis
- [x] Statistical Interpretations & Conclusions
- [x] Dataset Included (500 records)
- [x] Jupyter Notebook Included
- [x] Theory PDF Included

---

## 👩‍💻 Author

**Priya Savaliya**  
📍 Ahmedabad, Gujarat, India  

> *"Data-Driven Decisions · Statistical Thinking · Evidence-Based Conclusions"*

---

⭐ *If you found this project helpful, give it a star and feel free to fork!*

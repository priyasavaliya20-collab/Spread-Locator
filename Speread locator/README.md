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

```
---

# 🎬 Project Demo

[![Watch Demo](https://img.shields.io/badge/▶️%20Watch%20Demo-Google%20Drive-blue?style=for-the-badge&logo=google-drive)](https://drive.google.com/file/d/175YZyLfHg1AR_5acjJPqHpOEaXNAhdzz/view?usp=sharing)

📹 Click the badge above to watch the complete project demonstration.

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

## 📚 Import Libraries

```python
import pandas as pd
import numpy as np
from scipy.stats import bernoulli, binom
import matplotlib.pyplot as plt
import seaborn as sns
```

## 📂 Loaded Dataset

```python
df = pd.read_excel("spread_locator_dataset.xlsx")
```

---

## 1️⃣ Bernoulli & Binomial Distributions
**Objective:** Fit the data to Bernoulli and Binomial distributions (transaction occurrence & weekly count).

```python
# Bernoulli: Success = 1, Fail = 0
df["transaction_occurrence"] = df["transaction_status"].map({"Success": 1, "Fail": 0})
sns.countplot(x=df["transaction_occurrence"])
plt.title("Bernoulli Distribution - Transaction Occurrence")
plt.show()

# Binomial: weekly transaction counts
sns.histplot(df["transaction_count"], bins=10)
plt.title("Binomial Distribution - Weekly Transaction Counts")
plt.show()
```

**✅ Conclusion:** Transaction occurrence follows **Bernoulli**, weekly count follows **Binomial**.

**📊 Distribution:** Bernoulli p (success rate) = **0.4455** (~44.5% success). Weekly count: mean ≈ **2.85**, max = 9 → Binomial(n≈9-10, p≈0.30) shape.
---

## 2️⃣ Poisson Distribution
**Objective:** Fit the data to a Poisson distribution (number of transactions per day).

```python
df["transaction_date"] = pd.to_datetime(df["transaction_date"])
daily_transactions = df.groupby("transaction_date").size()
lam = daily_transactions.mean()

x = np.arange(daily_transactions.min(), daily_transactions.max()+1)
plt.hist(daily_transactions, bins=8, density=True, alpha=0.7, label="Observed")
plt.plot(x, poisson.pmf(x, lam), 'ro-', label="Poisson Fit")
plt.title("Poisson Distribution Fit")
plt.legend()
plt.show()
```

**✅ Conclusion:** Daily transaction counts follow a **Poisson distribution**.

**📊 Distribution:** λ (lambda) ≈ **7.1** transactions/day (mean ≈ variance, consistent with Poisson).
---
## 3️⃣ Log-Normal & Power Law Modeling
**Objective:** Model transaction amounts using Log-Normal and Power Law distributions.

```python
from scipy.stats import lognorm, powerlaw

amount = df["transaction_amount"]
amount = amount[amount > 0]
x = np.linspace(amount.min(), amount.max(), 500)

# Log-Normal fit
ln_shape, ln_loc, ln_scale = lognorm.fit(amount, floc=0)
plt.hist(amount, bins=20, density=True, alpha=0.7)
plt.plot(x, lognorm.pdf(x, ln_shape, ln_loc, ln_scale), 'r', label="Log-Normal")
plt.title("Log-Normal Distribution"); plt.legend(); plt.show()

# Power Law fit
pl_shape, pl_loc, pl_scale = powerlaw.fit(amount)
plt.hist(amount, bins=20, density=True, alpha=0.7)
plt.plot(x, powerlaw.pdf(x, pl_shape, pl_loc, pl_scale), 'darkred', label="Power Law")
plt.title("Power Law Distribution"); plt.legend(); plt.show()
```

**✅ Conclusion:** **Log-Normal is the best-fit distribution** for transaction amount — confirmed statistically (not just visually).

**📊 Distribution (AIC & KS test, n=220):**

| Distribution | AIC (lower=better) | KS p-value |
|---|---|---|
| **Log-Normal** | **3823.0** | **0.900** ✅ |
| Gamma | 3846.3 | 0.299 |
| Normal | 3968.6 | 0.0003 ❌ |
| Exponential | 4017.3 | <0.001 ❌ |
| Power Law | 4254.6 | <0.001 ❌ |


---

## 4️⃣ Q-Q Plot for Normality
**Objective:** Generate and interpret a Q-Q Plot to test normality.

```python
import statsmodels.api as sm
amount = df["transaction_amount"].dropna()
sm.qqplot(amount, line='45')
plt.title("Q-Q Plot of Transaction Amount")
plt.show()
```

**✅ Conclusion:** Transaction amount is **NOT normally distributed**.

**📊 Distribution:** The Q-Q plot shows clear upward bowing at the upper tail versus the 45° line → a right-skew signature, not normal.

---

## 5️⃣ Box-Cox Transform
**Objective:** Apply a Box-Cox transform to stabilize variance.

```python
from scipy.stats import boxcox
amount = df["transaction_amount"].dropna()
transformed_data, lam = boxcox(amount)
print("Lambda value:", lam)
plt.hist(transformed_data, bins=20)
plt.title("Box-Cox Transformed Data")
plt.show()
```

**✅ Conclusion:** Box-Cox confirms that a **log transform** is the correct stabilizing transform.

**📊 Distribution:** Lambda (λ) ≈ **-0.18**, close to 0 → mathematically equivalent to a log transform, reinforcing the Log-Normal conclusion.
---

## 6️⃣ Z-Scores & Tail Probability
**Objective:** Calculate Z-scores for transaction amounts and compute the probability of transactions exceeding ₹5000.

```python
from scipy.stats import zscore, norm
amount = df["transaction_amount"].dropna()
df["Z_score"] = zscore(amount)

z = (5000 - amount.mean()) / amount.std()
probability = 1 - norm.cdf(z)
print("Probability of transactions exceeding ₹5000:", probability)
```

**✅ Conclusion:** The original Z-score/Normal-based probability **understates the real risk** on this skewed data.

**📊 Distribution:** Normal-based P(amount > ₹5000) = **20.5%**; correct Log-Normal-based P = **13.8%** → a gap of **6.7 points**.
---

## 7️⃣ PDF & CDF Plots
**Objective:** Plot and interpret the PDF and CDF for transaction amounts.

```python
from scipy.stats import norm
amount = df["transaction_amount"].dropna()
mean, std = amount.mean(), amount.std()

x = np.linspace(amount.min(), amount.max(), 100)
plt.plot(x, norm.pdf(x, mean, std)); plt.title("PDF of Transaction Amount"); plt.show()
plt.plot(x, norm.cdf(x, mean, std)); plt.title("CDF of Transaction Amount"); plt.show()
```

**✅ Conclusion:** The Normal PDF/CDF visually mismatches the actual right-skewed data shape (and technically allows impossible negative amounts).

**📊 Distribution:** The correct PDF/CDF should use Log-Normal parameters (shape ≈ 0.475, scale ≈ 2983).

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

Statistical distribution analysis (Bernoulli, Binomial, Poisson, Log-Normal, Power Law, Q-Q plot, Box-Cox, Z-score, PDF/CDF) was applied on a 220-record transaction dataset to convert raw transaction data into evidence-based insights using Python.

Results showed transaction occurrence follows a Bernoulli process (~44.5% success rate) with weekly counts following Binomial, daily volume following Poisson (λ≈7.1), and transaction amount best fitting a Log-Normal distribution — confirmed by AIC/KS test, Q-Q plot, and Box-Cox (λ≈-0.18).

Since the data is right-skewed, Normal-based assumptions understate real risk (20.5% vs true 13.8% probability of exceeding ₹5000) and overstate typical transaction size. **Log-Normal-based metrics give a more reliable, risk-aware basis for forecasting and fraud detection.**

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

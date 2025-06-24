# 📊 Probability and Statistics Simulation Studies

**Author:** Sonal Agarwal  
**Date:** 2024-11-22

This repository contains **R code**, **mathematical derivations**, and **simulation studies** for two main problems in **probability and statistics**:

- **Section B.1:** Analysis of a **Shifted Exponential Distribution**
- **Section B.2:** Simulation study of **Drawing Balls from a Bag (Discrete Distribution)**

---

## 📚 Table of Contents

- [Overview](#overview)
- [Section B.1: Shifted Exponential Distribution](#section-b1-shifted-exponential-distribution)
- [Section B.2: Drawing Balls from a Bag](#section-b2-drawing-balls-from-a-bag)
- [Central Limit Theorem Demonstration](#central-limit-theorem-demonstration)
- [How to Run](#how-to-run)
- [File Structure](#file-structure)
- [References](#references)

---

## 📝 Overview

This project explores key statistical concepts through **simulation** and **mathematical analysis**, using **R programming** for:

- Distribution properties
- Maximum Likelihood Estimation (MLE)
- Bootstrap confidence intervals
- Discrete probability mass functions
- Sample mean convergence
- Central Limit Theorem (CLT) demonstrations

---

## 📈 Section B.1: Shifted Exponential Distribution

### Problem Context:

A **continuous random variable (X)** represents the time between a product being sold out and restocked in a supermarket.

**Probability Density Function (PDF):**

For a known shift constant `b` and rate parameter `λ`:


---

### 📌 Key Results:

- **Normalization Constant:** a = λ
- **Mean:** $E[X] = \frac{1}{λ} + b$
- **Variance:** $Var(X) = \frac{1}{λ^2}$
- **Standard Deviation:** $σ = \frac{1}{λ}$
- **CDF:**  
  $F(x)$ = $1 - exp(-λ * (x - b))$ for $x ≥ b$
- **Quantile Function:**  
  $Q(p)$ = $b - \frac{1}{λ} * log(1 - p)$
- **MLE for λ:**  
  Given a sample of size `n`:  
  $λ_MLE = \frac{n}{sum(X_i - b)}$
- **Bootstrap Confidence Intervals:**  
  Using the **boot** package in R.

---

### ✅ Example R Code for MLE and Bootstrapping:

```r
# MLE for lambda
MLE_lambda <- function(data, b) {
  n <- length(data)
  return(n / sum(data - b))
}

# Bootstrap confidence interval
bootstrap_res <- boot(data = df$TimeLength, statistic = MLE_lambda, R = 10000)
boot_cnf <- boot.ci(bootstrap_res, type = "perc")
```

🎯 Simulation Study:
Simulates samples from the shifted exponential distribution and plots Mean Squared Error (MSE) of λ estimation vs sample size.
```
ggplot(mse_data, aes(x = SampleSize, y = MSE)) +
  geom_line(color = "red") +
  labs(title = "Mean Squared Error of lambda vs Sample Size",
       x = "Sample Size (n)",
       y = "Mean Squared Error (MSE)") +
  theme_minimal()
```

🎲 Section B.2: Drawing Balls from a Bag
Problem Setup:
A bag contains a red balls and b blue balls where a ≥ 1 and b > 1.
Two balls are drawn without replacement.

Let X = Number of red balls drawn - Number of blue balls drawn

📌 Possible Values of X:
X ∈ { -2, 0, 2 }

📊 Probability Mass Function (PMF):
- $P(X = 2)$ = $\frac{a(a-1)}{(a+b)(a+b-1)}$

- $P(X = 0)$ = $\frac{2ab}{(a+b)(a+b-1)}$

- $P(X = -2)$ = $\frac{b(b-1)}{(a+b)(a+b-1)}$


📈 Expectation and Variance:
Expectation:
$E[X]$ = $\frac{[ 2a(a - 1) - 2b(b - 1) ]}{[ (a + b)(a + b - 1) ]}$

Variance:
$Var(X)$ = $\frac{[ 4a(a - 1) + 4b(b - 1) ]}{[ (a + b)(a + b - 1) ]} - [E[X]]^2$

📏 Central Limit Theorem Demonstration
Conducts repeated sampling of X to demonstrate the Central Limit Theorem (CLT).

Shows how the distribution of sample means approaches normality as sample size increases.

Plots Kernel Density Estimate (KDE) overlaid with the theoretical Gaussian curve.


⚙️ How to Run
Install Required R Packages:
```install.packages(c("tidyverse", "boot", "ggplot2", "dplyr"))```

Load Data:
- For Section B.1, make sure supermarket_data_2024.csv is in your working directory.

Run R Code:
- Copy and paste the code snippets from this README into an R script (.R) or directly into an R session.
- Modify parameters like a, b, n, and λ as needed for custom experiments.

📚 References
- Standard Probability and Statistics Theory
- Properties of Exponential Distributions
- Discrete Sampling without Replacement
- The Central Limit Theorem (CLT)
- R packages: boot, ggplot2, dplyr, tidyverse



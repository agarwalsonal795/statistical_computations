# 📊 Probability and Statistics Simulation Studies

**Author:** Sonal Agarwal  
**Date:** 2024-11-22

This repository contains **R code**, **mathematical derivations**, and **simulation studies** for two main problems in **probability and statistics**:

- **Section B.1:** Analysis of a **Shifted Exponential Distribution**  
- **Section B.2:** Simulation study of **Drawing Balls from a Bag** (Discrete Distribution)

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

1. **Distribution properties**
2. **Maximum Likelihood Estimation (MLE)**
3. **Bootstrap confidence intervals**
4. **Discrete probability mass functions**
5. **Sample mean convergence**
6. **Central Limit Theorem (CLT) demonstrations**

---

## 📈 Section B.1: Shifted Exponential Distribution

### Problem Context:

A **continuous random variable (X)** represents the time between a product being sold out and restocked in a supermarket.  

**PDF (Probability Density Function):**

For a known shift constant `b` and rate parameter `λ`:

\[
p_X(x) =
\begin{cases}
\lambda e^{-\lambda (x - b)}, & x \geq b \\
0, & x < b
\end{cases}
\]

---

### 📌 Key Results:

- **Normalization Constant:** \( a = \lambda \)
- **Mean:** \( E[X] = \frac{1}{\lambda} + b \)
- **Variance:** \( Var(X) = \frac{1}{\lambda^2} \)
- **Standard Deviation:** \( \sigma = \frac{1}{\lambda} \)
- **CDF:** \( F(x) = 1 - e^{-\lambda(x - b)} \) for \( x \geq b \)
- **Quantile Function:**  
  \[
  Q(p) = b - \frac{\ln(1-p)}{\lambda}
  \]

- **MLE for λ:**  
  \[
  \lambda_{MLE} = \frac{n}{\sum_{i=1}^{n} (X_i - b)}
  \]

- **Bootstrap Confidence Intervals:**  
  Implemented using the `boot` R package.

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

# 📊 Case Study 5 — Advanced Unsupervised & Market‑Basket Analysis in R

![R](https://img.shields.io/badge/R-Programming-blue?logo=r)
![Project Status](https://img.shields.io/badge/Status-Complete-brightgreen)
![Methods](https://img.shields.io/badge/Methods-K--means%20%7C%20Hierarchical%20%7C%20Apriori-orange)
![Data Sets](https://img.shields.io/badge/Data-Iris%20%7C%20Groceries-lightgrey)

> **Goal** Showcase two cornerstone unsupervised‑learning workflows:  
> • **Clustering** (Iris flower data)  
> • **Association‑rule mining** (UCI Groceries transactions)  
> The notebook covers data exploration, model fitting, diagnostics, and business‑oriented interpretation.

---

## 📑 Table of Contents
1. [Background](#background)  
2. [Data](#data)  
3. [Exploratory Data Analysis](#exploratory-data-analysis)  
4. [Methodology](#methodology)  
   * K‑means & Hierarchical Clustering  
   * Apriori Association Rules  
5. [Results](#results)  
6. [Business Interpretation](#business-interpretation)  
7. [Reproducibility](#reproducibility)  
8. [GitHub Topics](#github-topics)  
9. [Author](#author)

---

## Background
Unsupervised learning uncovers latent structure without predefined labels.

* **Clustering** groups observations by similarity (distance or linkage).  
* **Association rules** expose co‑purchase patterns valuable for merchandising and cross‑selling.

---

## Data
| Dataset      | Rows | Features             | Purpose                   |
|--------------|------|----------------------|---------------------------|
| **Iris**     | 150 (90 % sample) | 4 numeric + species | Flower morphology clustering |
| **Groceries**| 9 835 transactions | 169 items (binary) | Market‑basket analysis       |

Groceries data represent one month of supermarket receipts, stored as sparse binary transactions.

---

## Exploratory Data Analysis
### Iris
* Sepal & petal metrics summarised (mean sepal length ≈ 5.85 cm).  
* 90 % train sample preserves class balance (~44/46/45 by species).

### Groceries
* **Milk** is the single most‑purchased item (~25 % of baskets).  
* Average basket size ≈ 4.4 items; maximum basket = 32 items.

---

## Methodology
### 1️⃣ Clustering (Iris)

| Technique        | Key Parameters  | Notes                                     |
|------------------|-----------------|-------------------------------------------|
| **K‑means**      | *k = 5*         | `kmeans(iris[, 1:4], 5)`                  |
| **Hierarchical** | Ward linkage    | Cut tree at *k = 2* & *k = 3* for comparison |

*Cluster membership counts: 20 / 57 / 34 / 9 / 15.*

### 2️⃣ Association Rules (Groceries)

* **Apriori algorithm** (`arules` package).  
* Two parameter regimes:  
  * *Exploratory* — support ≥ 0.1 %, confidence ≥ 1 % → 40 887 rules (mean lift ≈ 2.68).  
  * *Business‑oriented* — support ≥ 2.5 %, confidence ≥ 10 % → 75 concise rules (mean lift ≈ 1.49).

---

## Results
### Clustering
* **Size‑based segmentation**: 5‑cluster solution cleanly separates small, medium, and large morphologies; hierarchical cut at *k = 3* confirms the gradient.

### Association Rules
**Top‑Lift Pairs**

| Rank | Antecedent ⇄ Consequent | Lift | Support |
|------|-------------------------|-----:|--------:|
| 1 | Root vegetables ⇄ Other vegetables | 2.25 | 4.74 % |
| 2 | Whipped/sour cream ⇄ Other vegetables | 2.08 | 2.89 % |
| 3 | Tropical fruit ⇄ Yogurt | 2.00 | 2.93 % |
| 4 | Butter ⇄ Whole milk | 1.95 | 2.37 % |
| 5 | Curd ⇄ Whole milk | 1.92 | 2.05 % |

---

## Business Interpretation
### Product Analytics
* High‑lift vegetable pairings suggest **bundle promotions** or **aisle proximity** merchandising.  
* Dairy‑to‑dairy affinities (curd → milk) inform **cross‑marketing discounts**.

### Clustering Insights
* Morphological clusters enable targeted **breed selection** or **growth‑condition studies**.  
* Species distribution across clusters highlights measurement‑driven taxonomy boundaries.

---

## Reproducibility

```r
# Clone repository
git clone https://github.com/your‑username/case‑study‑5-unsupervised.git
cd case‑study‑5-unsupervised

# Install required packages
install.packages(c("tidyverse", "fpc", "arules", "cluster", "factoextra"))

# Run the analysis
source("Case5.R")      # or knit 'CaseStudy5.Rmd'

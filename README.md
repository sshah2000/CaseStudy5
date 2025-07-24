# 📊 Case Study 5 — Advanced Unsupervised & Market‑Basket Analysis in R

![R](https://img.shields.io/badge/R-Programming-blue?logo=r)
![Project Status](https://img.shields.io/badge/Status-Complete-brightgreen)
![Methods](https://img.shields.io/badge/Methods-K--means%20%7C%20Hierarchical%20%7C%20Apriori-orange)
![Data Sets](https://img.shields.io/badge/Data-Iris%20%7C%20Groceries-lightgrey)

> **Goal** Demonstrate two cornerstone techniques of unsupervised learning:  
> • **Clustering** (Iris flower data)  
> • **Association‑rule mining** (UCI Groceries transactions)  
> The analysis walks through data exploration, model fitting, diagnostics, and practical interpretation.

---

## 📑 Table of Contents
1. [Background](#background)  
2. [Data](#data)  
3. [Exploratory Data Analysis](#exploratory-data-analysis)  
4. [Methodology](#methodology)  
   * K‑means & Hierarchical Clustering  
   * Apriori Association Rules  
5. [Results](#results)  
6. [Business Interpretation](#business-interpretation)  
7. [Reproducibility](#reproducibility)  
8. [GitHub Topics](#github-topics)  
9. [Author](#author)

---

## Background
Unsupervised techniques uncover hidden structure without predefined labels.  
* **Clustering** groups observations by similarity (distance or linkage).  
* **Association rules** reveal co‑purchase patterns and cross‑selling opportunities.

---

## Data
| Dataset | Rows | Features | Purpose |
|---------|------|----------|---------|
| **Iris** | 150 (sample 90 %) | 4 numeric + species | Flower morphology clustering |
| **Groceries** | 9 835 transactions | 169 items (binary) | Market‑basket analysis |

Groceries data spans one month of supermarket receipts, producing sparse binary transactions :contentReference[oaicite:0]{index=0}.

---

## Exploratory Data Analysis
### Iris
* Sepal & petal metrics summarized (mean ≈ 5.85 cm sepal length, etc.) :contentReference[oaicite:1]{index=1}.  
* Random 90 % sample maintains class balance (≈ 44/46/45 by species) :contentReference[oaicite:2]{index=2}.

### Groceries
* Milk is the single most purchased item (~25 % of all baskets).  
* Typical basket size ≈ 4.4 items; max basket = 32 items :contentReference[oaicite:3]{index=3}.

---

## Methodology
### 1️⃣ Clustering (Iris)
| Technique | Key Parameters | Notes |
|-----------|----------------|-------|
| **K‑means** | k = 5 clusters | `kmeans(iris_1[,1:4], 5)` |
| **Hierarchical** | Ward’s linkage | Cut tree at k = 2 & k = 3 for comparison |

> Cluster membership counts: 20 / 57 / 34 / 9 / 15 :contentReference[oaicite:4]{index=4}.

### 2️⃣ Association Rules (Groceries)
* **Apriori algorithm** (`arules` package).  
* Two parameter regimes:  
  * **Low support/confidence** (0.1 % / 1 %): 40  887 rules discovered, mean lift ≈ 2.68 :contentReference[oaicite:5]{index=5}.  
  * **Business‑oriented**: support ≥ 2.5 %, confidence ≥ 10 % → 75 high‑quality rules; mean lift ≈ 1.49 :contentReference[oaicite:6]{index=6}.

---

## Results
### Clustering
* **Size‑based segmentation**: five‑cluster solution neatly separates flowers into small, medium, and large morphologies; hierarchical cut at k = 3 confirms this gradient :contentReference[oaicite:7]{index=7}.

### Association Rules
* **Top Lift Pairs**  
  1. *Root vegetables ⇄ Other vegetables* — lift 2.25, support 4.74 % :contentReference[oaicite:8]{index=8}  
  2. *Whipped/sour cream ⇄ Other vegetables* — lift 2.08, support 2.89 % :contentReference[oaicite:9]{index=9}  
  3. *Tropical fruit ⇄ Yogurt* — lift 2.00, support 2.93 % :contentReference[oaicite:10]{index=10}  
  4. *Butter ⇄ Whole milk* — lift 1.95 :contentReference[oaicite:11]{index=11}  
  5. *Curd ⇄ Whole milk* — lift 1.92 :contentReference[oaicite:12]{index=12}  

---

## Business Interpretation
* **Product Analytics**  
  * High lift vegetable pairings suggest bundling or aisle proximity promotions.  
  * Dairy‑to‑dairy affinities (curd → milk) can guide co‑marketing discounts.

* **Clustering Insights**  
  * Morphological clusters enable targeted breed selection or growth condition studies.  
  * Species distribution across clusters highlights measurement‑driven taxonomy boundaries.

---

## Reproducibility

```r
# Clone repo
git clone https://github.com/your‑username/case‑study‑5-unsupervised.git
cd case‑study‑5-unsupervised

# Install packages
install.packages(c("tidyverse","fpc","arules","cluster","factoextra"))

# Execute analysis
source("Case5.R")       # or knit CaseStudy5.Rmd

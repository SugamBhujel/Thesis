# Popularity Bias in Recommender Systems  
### Structural Imbalance, Algorithmic Amplification, and Model-Agnostic Mitigation

##  Overview
This repository contains the implementation and experimental analysis for my MSc thesis on **popularity bias in recommender systems**, using the MovieLens 32M dataset.

The study investigates:
- Structural imbalance in real-world recommendation datasets
- Whether collaborative filtering models amplify popularity bias
- A model-agnostic reranking strategy to mitigate bias
- The trade-off between fairness and recommendation accuracy
- Mechanism-level changes using correlation and explainability analysis

---

##  Research Questions

- **RQ1:** Does matrix factorization amplify structural popularity bias?  
- **RQ2:** Can a model-agnostic reranking method control item exposure?  
- **RQ3:** What is the fairness–utility trade-off when applying mitigation?  
- **RQ4:** Does mitigation change how ranking decisions are made?  

---

##  Dataset

- **Dataset:** MovieLens 32M  
- **Type:** Explicit ratings (1–5)  
- **Preprocessing:**
  - Users with ≥ 20 ratings  
  - Items with ≥ 5 ratings  
- **Split:** 80/20 per-user train-test split  

---

##  Methodology

### 1. Structural Baseline
- Item popularity computed from training data
- Head items: top 20% by popularity
- Metric:
  - `DatasetHeadShare`

---

### 2. Models

#### 2.1 MostPopular (Baseline)
- Non-personalized
- Ranks items purely by global popularity

#### 2.2 Matrix Factorization (MF)
Prediction:

\[
\hat{r}_{ui} = \mu + b_u + b_i + p_u^T q_i
\]

- Trained using SGD
- Embedding dimension: 32

---

### 3. Evaluation Metrics

#### Accuracy
- Recall@10  
- NDCG@10  

#### Fairness / Exposure
- Model Head Share  
- Amplification  
- Coverage@10  
- Gini Coefficient  
- ΔGAP (user-level alignment)

---

### 4. Bias Mitigation (Reranking)

Penalty:

\[
Penalty(i) = \log(1 + Popularity(i))
\]

Adjusted score:

\[
Score(u,i) = Score_{MF}(u,i) - \lambda \cdot Penalty(i)
\]

- λ ∈ [0.0, 1.0]

---

### 5. Mechanism-Level Analysis

- **Spearman Correlation** between popularity and ranking score  
- **SHAP (via surrogate model)** to explain feature contributions  

---

##  Key Findings

- The dataset is **highly imbalanced**  
  - ~96% of interactions belong to top 20% of items  

- **Matrix Factorization does NOT amplify bias**
  - Reduces head share (~0.96 → ~0.74)

- **Reranking effectively controls exposure**
  - Increasing λ reduces head dominance  

- **Fairness–Utility Trade-off exists**
  - Higher fairness → gradual drop in Recall/NDCG  

- **Mechanism shift observed**
  - Popularity becomes a **negative ranking factor** as λ increases  

- **Important insight**
  - Reducing head share ≠ reducing inequality (Gini remains high)


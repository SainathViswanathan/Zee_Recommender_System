# ZEE5 — Personalized Movie Recommender System

## 🎬 About ZEE5
ZEE5 is one of India’s largest OTT streaming platforms, offering movies, shows, and web series across multiple languages and genres.  
As the platform’s library expands, delivering **personalized recommendations** becomes essential to increase engagement, watch time, and user satisfaction.

This project focuses on building a **data-driven recommendation engine** to help ZEE5 recommend content tailored to each user’s viewing preferences and behavioral patterns.

---

## 🧩 Problem Statement
ZEE5 aims to enhance **user retention and engagement** through intelligent content discovery.  
The challenge lies in surfacing movies that align closely with user tastes from a massive and sparse user–item matrix.  
The goal is to develop a **scalable and accurate recommendation engine** leveraging collaborative filtering, matrix factorization, and similarity-based models.

---

## 🎯 Project Objective
To design and evaluate multiple **collaborative filtering** techniques —  
including **Pearson Correlation**, **Cosine Similarity (KNN)**, and **Matrix Factorization (SVD)** —  
for building a personalized movie recommender system that improves ZEE5’s content visibility and user satisfaction.

---

## 🔑 Key Goals
- Load, clean, and merge user, movie, and rating datasets.  
- Perform **Exploratory Data Analysis (EDA)** to uncover viewing trends, demographics, and genre preferences.  
- Implement:
  - **Item-based Collaborative Filtering** (Pearson & Cosine similarity)
  - **Matrix Factorization (SVD)** using the `Surprise` library  
  - Optional **User-based CF** to handle cold-start users
- Visualize movie embeddings (PCA, t-SNE) to interpret clusters.
- Evaluate model accuracy via **RMSE** and **MAPE**.
- Deliver actionable business insights and hybrid recommendation strategies.

---

## 📚 Dataset Overview
The dataset includes:
- **User attributes:** age, gender, occupation  
- **Movie metadata:** title, genre, release year  
- **Ratings:** explicit user feedback (1–5 scale)

| Attribute | Description |
|------------|-------------|
| `userId` | Unique identifier for user |
| `movieId` | Unique identifier for movie |
| `rating` | User’s rating (1–5) |
| `age`, `gender`, `occupation` | User demographics |
| `title`, `genre`, `year` | Movie metadata |

**Size:** ~100,000 ratings  
**Users:** 943 **Movies:** 1,682  
**Sparsity:** ~95.5%

---

## 🧠 Techniques Explored
| Approach | Description | Libraries Used |
|-----------|--------------|----------------|
| **Pearson Correlation** | Measures linear rating similarity between co-rated items. | pandas, numpy |
| **Cosine Similarity (KNN)** | Measures angular similarity in user–item rating space. | scikit-learn |
| **Matrix Factorization (SVD)** | Learns latent semantic patterns via factorization of sparse matrices. | `surprise` |
| **Embedding Visualization** | PCA & t-SNE used to interpret latent clusters. | scikit-learn |
| **Hybrid Approach** | Combines SVD + KNN strengths for balanced performance. | custom ensemble |

---

## 🔍 Exploratory Insights

### 👥 Demographic Behavior
- **Age Group 25–34**: Most active (395,556 ratings).  
- **Occupation “College/Grad Student” (code 4)**: Most ratings (131,032).  
- **Gender Split:** ~75% Male, ~25% Female.  
- **Decade Distribution:** Majority of movies from the **1990s (532,843)**.

### 🎞️ Popular Movies
- **Most Rated:** *American Beauty* (3,428 ratings)  
- **Top Classics:** *Star Wars IV & V*, *The Matrix*, *Shawshank Redemption*.

---

## ⚙️ Modeling Approach

### 1. **Item-Based Collaborative Filtering**
- Built similarity matrix using **Pearson Correlation** and **Cosine Similarity**.  
- Generated “Top-N” movie recommendations per target title.  

| Example: *Liar Liar* | Similar Movies | Metric |
|-----------------------|----------------|--------|
| Pearson | Life (0.576), Oliver & Company (0.550), Spy Hard (0.502) | Correlation |
| Cosine | Mrs. Doubtfire (0.557), Ace Ventura (0.516), Dumb & Dumber (0.512) | Similarity |

---

### 2. **Matrix Factorization (SVD)**
- Decomposed user–item rating matrix into latent feature vectors.  
- Captured hidden relationships between genres and user preferences.  
- Optimized using grid search for `n_factors`, `lr_all`, and `reg_all`.

| Metric | Value |
|---------|-------|
| **RMSE** | 0.8834 |
| **MAPE** | 26.95% |

### 3. **Hybrid Recommendation**
- Combined **SVD** embeddings with **KNN** similarity for robustness.  
- Outperformed standalone methods in recommendation coverage and novelty.  
- Visualized embedding clusters using **PCA** and **t-SNE**.

---

## 🎯 Model Comparison Summary

| Model | Basis | Sample Recommendations (*The Matrix*) | Strengths | Limitations |
|--------|--------|--------------------------------------|------------|--------------|
| **Pearson** | Linear Co-Ratings | Bed of Roses, Grace of My Heart | Simple, interpretable | Sparse data limits coverage |
| **Cosine (KNN)** | Rating pattern angle | Terminator 2, Star Wars, Total Recall | Fast, scalable | Ignores rating scale |
| **SVD (MF)** | Latent features | The Cure, Payback, White Men Can’t Jump | Captures deep patterns | Requires training & tuning |

---

## 🧩 Key Takeaways
✅ Each model interprets *similarity* differently:
- **Pearson:** Users rated these items similarly.  
- **Cosine:** Rating *patterns* are similar (scale-invariant).  
- **SVD:** Movies are *thematically close*, even without overlap.

✅ **Hybrid models** balance:
- **SVD’s depth** (latent factors)  
- **KNN’s simplicity** (behavioral overlap)  
- **Pearson’s interpretability** (niche clusters)

✅ **Best Scenarios**
| Scenario | Recommended Model |
|-----------|--------------------|
| Cold-start users or items | SVD (Matrix Factorization) |
| Sparse but wide data | Cosine (KNN) |
| Dense overlap clusters | Pearson Correlation |
| Mixed or production setup | Hybrid (SVD + KNN) |

---

## 💼 Business Insights & Recommendations

### 1. Adopt a **Hybrid Recommender Strategy**
- Combine **SVD** (latent embeddings) with **KNN** (collaborative signals).  
- Use **Pearson** for segments with rich history; **Cosine** for fast cold-starts.

### 2. **Leverage Viewing Patterns**
- Peak hours: **6–10 PM** and **Mon–Tue**.  
- Schedule key releases and notifications during these windows.  
- Exploit **seasonal spikes** (Nov, Aug) for promotional campaigns.

### 3. **Genre & Demographic Targeting**
- Focus on **Drama, Comedy, Action** — highest engagement.  
- Build **genre-decade carousels** (e.g., *90s Action*, *80s Sci-Fi*).  
- Personalize based on **age, occupation, and gender trends**.

### 4. **Tackle Sparsity & User Diversity**
- Continue **Matrix Factorization** for high sparsity (95%+).  
- Introduce **UI/UX personalization** for under-represented segments (e.g., older users, female viewers).

### 5. **Content Strategy via Top Titles**
- Use *American Beauty*, *Star Wars*, *The Matrix* as anchor titles.  
- Highlight top-rated classics (*Seven Samurai*, *Shawshank Redemption*) to enhance credibility and engagement.

---

## 📊 Evaluation Metrics
| Metric | Purpose | Observed |
|---------|----------|-----------|
| RMSE | Rating accuracy | 0.8834 |
| MAPE | Percentage error | 26.95% |
| Precision@K / Recall@K | Recommendation relevance | High for SVD |
| Coverage & Novelty | Diversity | Improved via Hybrid |

---

## 🧰 Tools & Libraries
| Category | Tools |
|-----------|--------|
| **Data Processing** | pandas, numpy |
| **Visualization** | matplotlib, seaborn |
| **Modeling** | scikit-learn, surprise |
| **Dimensionality Reduction** | PCA, t-SNE |
| **Evaluation** | RMSE, MAPE, precision@k, recall@k |

---

## 🧪 How to Run
1. Clone the repository.  
2. Place datasets (`users.csv`, `movies.csv`, `ratings.csv`) into `/data`.  
3. Run `Zee_Recommender_System_Case_Study.ipynb` step-by-step.  
4. Review recommendation outputs and embedding visualizations.

---

## 📌 Project Impact
This recommendation pipeline enables ZEE5 to:
- Deliver **personalized movie suggestions** that boost engagement.  
- Increase **watch time**, **CTR**, and **session duration**.  
- Reduce churn through better discoverability.  
- Implement **AI-driven personalization** at scale.

---

## 🧭 Authors & Acknowledgments
Developed by **Sainath Viswanathan** as part of Scaler’s Data Science & ML learning journey.  
Guided by Scaler’s Recommender Systems case study framework.

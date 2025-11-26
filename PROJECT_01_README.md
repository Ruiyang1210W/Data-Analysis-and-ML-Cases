# Amazon Product Recommendation System

## Project Overview

This project implements a comprehensive recommendation system for Amazon electronic products, demonstrating multiple collaborative filtering approaches and matrix factorization techniques. The system is designed to provide personalized product recommendations based on user rating patterns.

## Business Context

E-commerce platforms like Amazon rely heavily on recommendation systems to:
- Increase customer engagement and time spent on platform
- Improve conversion rates through personalized suggestions
- Enhance user experience by reducing information overload
- Drive revenue through relevant product discovery

## Dataset

**Source:** Amazon product reviews dataset (Electronics category)

**Original Size:** 7,824,482 ratings

**Filtered Size:** 65,290 ratings
- Users with minimum 50 ratings
- Products with minimum 5 ratings

**Features:**
- `user_id`: Unique identifier for each user
- `prod_id`: Unique identifier for each product
- `rating`: User rating (1-5 scale)

**Rationale for Filtering:** In production systems, users and products with very few interactions provide unreliable signals. This filtering improves model quality while maintaining computational efficiency.

## Methodology

### 1. Rank-Based Recommendation (Baseline)
- Calculates average rating and interaction count per product
- Recommends top-N products based on popularity
- **Use Case:** Cold-start problem (new users without rating history)

### 2. User-User Collaborative Filtering
- Finds similar users based on rating patterns
- Uses cosine similarity and KNN algorithm
- **Baseline Performance:** RMSE: 1.00, Precision: 0.855, Recall: 0.858
- **Optimized Performance:** RMSE: 0.96, F1-score: 0.87

**Hyperparameter Tuning:**
- Similarity metric: Cosine vs MSD vs Pearson
- k (neighbors): 10, 20, 30
- min_k (minimum neighbors): 3, 6, 9

### 3. Item-Item Collaborative Filtering
- Finds similar products based on user rating patterns
- More scalable than user-user for large catalogs
- **Baseline Performance:** RMSE: 0.995, Precision: 0.838
- **Optimized Performance:** RMSE: 0.96, F1-score: 0.852

**Advantages:**
- More stable over time (product catalog changes slower than user preferences)
- Better scalability for growing user bases
- Pre-computation of item similarities possible

### 4. Matrix Factorization (SVD)
- Decomposes user-item matrix into latent factors
- Captures hidden patterns in user preferences
- **Baseline Performance:** RMSE: 0.888, F1-score: 0.866
- **Optimized Performance:** RMSE: 0.883, F1-score: 0.870

**Hyperparameter Tuning:**
- n_epochs: 10, 20, 30
- lr_all (learning rate): 0.001, 0.005, 0.01
- reg_all (regularization): 0.2, 0.4, 0.6

## Evaluation Metrics

### Why Not Just RMSE?

This project emphasizes **business-relevant metrics** over purely statistical measures:

**Precision@k:** Of the k items recommended, what percentage are relevant?
- Business Impact: Minimizes user frustration from irrelevant recommendations

**Recall@k:** Of all relevant items, what percentage are in top-k recommendations?
- Business Impact: Ensures users discover products they'll actually like

**F1-score@k:** Harmonic mean of Precision and Recall
- Business Impact: Balanced metric for overall recommendation quality

**ROC-AUC:** Model's ability to distinguish between relevant and irrelevant items
- Business Impact: Overall discriminative power of the system

**Threshold:** 3.5 (ratings ≥ 3.5 considered "relevant")

## Key Results

| Model | RMSE | Precision@10 | Recall@10 | F1@10 |
|-------|------|--------------|-----------|-------|
| User-User (Baseline) | 1.001 | 0.855 | 0.858 | 0.856 |
| User-User (Optimized) | 0.955 | 0.855 | 0.885 | 0.870 |
| Item-Item (Baseline) | 0.995 | 0.838 | 0.845 | 0.841 |
| Item-Item (Optimized) | 0.965 | 0.837 | 0.868 | 0.852 |
| SVD (Baseline) | 0.888 | 0.853 | 0.880 | 0.866 |
| **SVD (Optimized)** | **0.883** | **0.853** | **0.888** | **0.870** |

## Business Recommendations

1. **Deploy SVD Model:** Best balance of accuracy and scalability
2. **Hybrid Approach:** Combine rank-based (cold start) + SVD (personalized)
3. **A/B Testing:** Validate impact on click-through rate and conversion
4. **Real-time Updates:** Implement incremental learning for new ratings
5. **Diversity:** Consider adding diversity constraints to avoid filter bubbles

## Technical Implementation

**Libraries:**
- `surprise`: Recommendation algorithms (KNNBasic, SVD)
- `scikit-learn`: Model evaluation and cross-validation
- `pandas/numpy`: Data manipulation
- `matplotlib/seaborn`: Visualization

**Computational Optimization:**
- Dataset reduction through intelligent filtering
- Pre-computation of similarity matrices
- GridSearchCV with parallel processing (n_jobs=-1)

## Limitations & Future Work

**Current Limitations:**
- No content-based features (product metadata, descriptions)
- No temporal dynamics (rating patterns over time)
- Cold-start problem for completely new users/products

**Future Enhancements:**
- Incorporate product metadata (category, price, brand)
- Implement neural collaborative filtering
- Add contextual bandits for explore-exploit tradeoff
- Build real-time recommendation API

## Files

- **Notebook:** `01_Amazon_Recommendation_System.ipynb`
- **Dataset:** `ratings_Electronics.csv` (not included due to size)

## References

- Koren, Y., Bell, R., & Volinsky, C. (2009). Matrix factorization techniques for recommender systems. *Computer*, 42(8), 30-37.
- Surprise Documentation: https://surprise.readthedocs.io/

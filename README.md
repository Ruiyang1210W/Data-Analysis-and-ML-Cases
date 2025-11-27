# MIT IDSS Data Science & Machine Learning Projects

This repository contains projects completed as part of the **MIT IDSS (Institute for Data, Systems, and Society) Data Science and machine learning: making data-driven decisions**. These projects demonstrate expertise in translating raw data into actionable insights through advanced machine learning techniques, statistical analysis, and designing objective functions aligned with business goals.

The program officially ended in February 2025; The remaining self-paced courses were completed in March 2025.

## Overview

The repository showcases two primary **capstone projects** focusing on machine learning optimization for business metrics, plus one foundational data analysis project. Each demonstrates end-to-end workflows including exploratory data analysis (EDA), feature engineering, cross-validated model development, hyperparameter tuning, and deployment-ready recommendations.

**Key Philosophy:** Rather than optimizing purely statistical metrics like training loss, these projects emphasize **business-relevant evaluation** (Precision@k, ROC-AUC, F1-score) and translating model insights into actionable strategies.

---

## Capstone Projects

### 1. Amazon Product Recommendation System (Capstone)
**File:** `01_Amazon_Recommendation_System.ipynb`

**Objective:** Build a scalable recommendation system to predict user preferences and recommend products based on historical ratings.

**Key Highlights:**
- Implemented multiple recommendation algorithms:
  - **Rank-based filtering** for popularity-based recommendations
  - **User-user collaborative filtering** using cosine similarity and KNN
  - **Item-item collaborative filtering** for scalable recommendations
  - **Matrix Factorization (SVD)** for latent feature extraction
- **Optimized for business metrics:** Precision@k, Recall@k, and F1-score@k (rather than just training loss)
- Achieved **ROC-AUC of 0.88** and **F1-score of 0.87** with optimized SVD model
- **Cross-validated hyperparameter tuning** using GridSearchCV with 3-fold CV
- Reduced dataset from 7.8M to **65K+ ratings** through intelligent filtering (users with 50+ ratings, products with 5+ ratings)
- Demonstrated **business-metric alignment**: optimized for Precision@k and Recall@k rather than just RMSE

**Technical Skills:** Python, Pandas, NumPy, Surprise Library, Scikit-learn, Collaborative Filtering, Matrix Factorization, Cross-Validation

**Business Impact:** Enables personalized product recommendations to improve customer engagement and conversion rates

---

### 2. ExtraaLearn Lead Conversion Prediction (Capstone)
**File:** `03_ExtraaLearn_Lead_Conversion_Prediction.ipynb`

**Objective:** Build a machine learning classifier to predict which leads are likely to convert to paid customers for an EdTech startup.

**Key Highlights:**
- Developed **classification models** using Decision Trees and Random Forests
- **Feature engineering**: Created interaction_intensity, profile_completion_score, normalized ratios
- Achieved **AUC of 0.76** and **72% accuracy** with Random Forest
- **Cross-validated hyperparameter optimization** using GridSearchCV with 5-fold CV
- **Business-metric focused**: Optimized for F1-score and recall to minimize missed conversions
- Model interpretation revealed conversion drivers:
  - Interaction intensity (28% feature importance)
  - Profile completion score (22%)
  - Website visits (18%)

**Technical Skills:** Python, Scikit-learn, Decision Trees, Random Forests, Feature Engineering, Cross-Validation, ROC-AUC Analysis

**Business Impact:** Enables efficient resource allocation by prioritizing high-conversion leads, projected to **double sales ROI** from 30% to 60%+ conversion rate on targeted leads

---

## Foundational Project

### 3. FoodHub Data Analysis
**File:** `02_FoodHub_Data_Analysis.ipynb`

**Objective:** Analyze food delivery order data to identify demand patterns and provide recommendations to enhance customer experience.

**Key Highlights:**
- Conducted comprehensive **exploratory data analysis (EDA)** on 1,898 orders
- Identified top-performing restaurants and cuisine preferences by weekday/weekend
- Analyzed delivery performance metrics:
  - Mean food preparation time: 27.4 minutes
  - Mean delivery time: 24.2 minutes
  - 10.2% of orders exceeded 60-minute total delivery time
- Calculated revenue optimization: 25% margin on orders >$20, 15% margin on orders >$5
- Generated total revenue of **$3,865.57** across analyzed orders

**Technical Skills:** Python, Pandas, NumPy, Matplotlib, Seaborn, Statistical Analysis, Data Visualization

**Business Recommendations:**
- Streamline order processing to reduce preparation times
- Implement dynamic resource allocation during peak hours
- Increase marketing for high-value orders (>$20) to maximize revenue
- Incentivize customer ratings through gamification

---

## Repository Structure

```
Data-Analysis-and-ML-Cases/
│
├── 01_Amazon_Recommendation_System.ipynb           # CAPSTONE: Recommendation system (Collaborative Filtering + SVD)
├── 02_FoodHub_Data_Analysis.ipynb                  # Foundations: EDA and business insights
├── 03_ExtraaLearn_Lead_Conversion_Prediction.ipynb # CAPSTONE: Lead conversion classifier
├── PROJECT_01_README.md                            # Detailed Amazon project documentation
├── PROJECT_02_README.md                            # Detailed FoodHub project documentation
├── PROJECT_03_README.md                            # Detailed ExtraaLearn project documentation
├── requirements.txt                                # Python dependencies
├── .gitignore                                      # Git ignore rules
├── LICENSE                                         # MIT License
├── ACKNOWLEDGMENTS.md                              # Credits and acknowledgments
└── README.md                                       # This file
```

---

## Technical Stack

**Languages:** Python

**Libraries:**
- **Data Manipulation:** Pandas, NumPy
- **Visualization:** Matplotlib, Seaborn
- **Machine Learning:** Scikit-learn, Surprise
- **Model Evaluation:** Cross-validation, GridSearchCV, ROC-AUC, Precision@k, Recall@k

**Techniques:**
- Exploratory Data Analysis (EDA)
- Collaborative Filtering (User-User, Item-Item)
- Matrix Factorization (SVD)
- Classification (Decision Trees, Random Forests)
- Hyperparameter Tuning
- Feature Engineering
- Model Evaluation & Optimization

---

## Key Learnings

These capstone projects reinforced critical data science principles:

1. **Designing Objective Functions Aligned with Business Goals**
   - Amazon project: Optimized for Precision@k and ROC-AUC rather than just training loss/RMSE
   - ExtraaLearn project: Focused on F1-score and recall to minimize missed conversion opportunities
   - Demonstrated that statistical metrics alone don't capture business value

2. **Cross-Validated Model Evaluation**
   - Implemented GridSearchCV with k-fold cross-validation (3-fold and 5-fold)
   - Comprehensive evaluation across multiple metrics: Precision@k, Recall@k, F1-score, ROC-AUC
   - Prevented overfitting through proper train/test splits and validation

3. **Feature Engineering for Business Impact**
   - Created domain-specific features (interaction_intensity, profile_completion_score)
   - Normalized metrics to reduce scale bias (page_time_ratio, profile_time_ratio)
   - Translated raw features into actionable signals

4. **Translating Model Insights into Deployment-Ready Recommendations**
   - Amazon: Hybrid recommendation strategy combining multiple algorithms
   - ExtraaLearn: Lead scoring system with tiered follow-up strategies
   - Quantified business impact: revenue projections, efficiency gains, ROI estimates

5. **Scalability and Production Considerations**
   - Reduced computational complexity through intelligent data filtering (7.8M → 65K ratings)
   - Selected algorithms balancing accuracy and inference speed
   - Addressed class imbalance and cold-start problems

6. **End-to-End Machine Learning Pipeline**
   - Data preprocessing and exploratory analysis
   - Model development and hyperparameter optimization
   - Evaluation on business-relevant metrics
   - Deployment strategy and monitoring recommendations

---

## How to Run

1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/Data-Analysis-and-ML-Cases.git
   cd Data-Analysis-and-ML-Cases
   ```

2. Install required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Open Jupyter Notebook or Google Colab:
   ```bash
   jupyter notebook
   ```

4. Navigate to any project notebook and run the cells sequentially

**Note:** Some projects were developed in Google Colab. You may need to adjust file paths if running locally. Datasets are not included in this repository.

---

## About This Repository

This repository contains educational projects completed as part of the **MIT IDSS Data Science and machine learning: making data-driven decisions**. The work is shared publicly for educational and professional development purposes with proper attribution to MIT IDSS.

**Datasets:** Not included in this repository per educational use guidelines.

**Original Work:** All analysis, code implementation, visualizations, insights, and recommendations are original work completed independently as part of the certification requirements.

---

MIT License - See [LICENSE](LICENSE) file for details.

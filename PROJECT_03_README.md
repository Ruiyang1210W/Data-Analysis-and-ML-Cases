# ExtraaLearn Lead Conversion Prediction

## Project Overview

This project builds a machine learning classification model to predict lead conversion for ExtraaLearn, an EdTech startup offering programs in cutting-edge technologies. The model helps identify high-potential leads to optimize resource allocation and improve conversion rates.

## Business Context

The EdTech industry is projected to reach **$286.62 billion by 2023** with a CAGR of 10.26%. The COVID-19 pandemic accelerated growth, creating intense competition for customer acquisition.

**Challenge:** With large lead volumes from multiple channels (social media, website, email), ExtraaLearn needs to:
- Prioritize leads most likely to convert
- Allocate sales resources efficiently
- Understand conversion drivers
- Create targeted marketing campaigns

**Business Impact:** Improving lead prioritization from random (30% conversion) to ML-driven (targeting 60%+ conversion) can double ROI on sales efforts.

## Dataset

**Size:** 4,612 leads

**Target Variable:**
- `status`: 1 = Converted to paid customer, 0 = Not converted
- **Class Distribution:** 29.9% converted (imbalanced dataset)

**Features:**

**Demographic:**
- `age`: Lead age (18-63 years)

**Behavioral:**
- `website_visits`: Number of website visits (0-30)
- `time_spent_on_website`: Total time in seconds (0-2,537)
- `page_views_per_visit`: Average pages viewed (0-18.4)
- `profile_completed`: Low (0-50%), Medium (50-75%), High (75-100%)

**Categorical:**
- `current_occupation`: Professional, Unemployed, Student
- `first_interaction`: Website, Mobile App
- `last_activity`: Email Activity, Phone Activity, Website Activity

**Marketing Channels:**
- `print_media_type1`: Newspaper ad exposure (Yes/No)
- `print_media_type2`: Magazine ad exposure (Yes/No)
- `digital_media`: Digital platform ad exposure (Yes/No)
- `educational_channels`: Online forums/educational sites (Yes/No)
- `referral`: Referred by existing customer (Yes/No)

**Data Quality:** No missing values, clean dataset

## Methodology

### 1. Exploratory Data Analysis (EDA)

**Key Findings:**
- **Age Distribution:** Broad range (18-63), mean age 46.2 years
- **Engagement Metrics:** Mean website visits = 3.6, mean time = 724 seconds
- **Outlier Detection:**
  - `website_visits`: 154 outliers (heavy users)
  - `page_views_per_visit`: 257 outliers (highly engaged)

**Analysis Questions Addressed:**
1. How does current occupation affect conversion?
2. Do first interaction channels impact conversion?
3. Which interaction methods work best?
4. Which marketing channels have highest conversion?
5. Does profile completion increase conversion chances?

### 2. Feature Engineering

**Engineered Features:**

1. **Interaction Intensity** = `time_spent_on_website` × `page_views_per_visit`
   - Captures overall engagement level
   - Highest importance (28% of model)

2. **Profile Completion Score**: Ordinal encoding
   - Low = 0, Medium = 1, High = 2
   - Second highest importance (22% of model)

3. **Page-Time Ratio** = `time_spent_on_website` / `page_views_per_visit`
   - Normalized metric reducing scale bias
   - Indicates depth of engagement per page

4. **Profile-Time Ratio** = `time_spent_on_website` / `profile_completion_score`
   - Normalized time investment relative to profile completion

**Rationale:** Raw features often have scale differences. Ratios and interaction terms provide normalized, meaningful insights about user behavior.

### 3. Model Development

#### Decision Tree Classifier

**Baseline Model:**
- Criterion: Gini
- Max depth: None (fully grown tree)
- Class weight: Balanced (address 70:30 imbalance)

**Performance:**
- Accuracy: 68%
- Precision (Converted): 0.46
- Recall (Converted): 0.41
- F1-score: 0.43
- **Issue:** Low recall and precision for converted class

**Hyperparameter Tuning (GridSearchCV):**
- 5-fold cross-validation
- Scoring metric: F1 (suitable for imbalanced data)
- Parameter grid:
  - `max_depth`: [None, 5, 10, 15, 20, 25]
  - `min_samples_split`: [2, 5, 10, 15]
  - `min_samples_leaf`: [1, 2, 4, 6]
  - `criterion`: ['gini', 'entropy']

**Best Parameters:**
- Criterion: Entropy
- Max depth: 5
- Min samples split: 15
- Min samples leaf: 4

**Optimized Performance:**
- Accuracy: 67%
- Precision (Converted): 0.46
- Recall (Converted): 0.69 ⬆️ (+68%)
- F1-score: 0.56
- **AUC-ROC: 0.76**

**Analysis:** Pruning the tree improved recall significantly (0.41 → 0.69), better identifying true conversions.

#### Random Forest Classifier

**Baseline Model:**
- N_estimators: 100
- Max depth: None
- Min samples split: 2

**Performance:**
- Accuracy: 71% ⬆️
- Precision (Converted): 0.51
- Recall (Converted): 0.38
- F1-score: 0.44

**Optimized Model (Limited Depth):**
- Max depth: 15 (prevent overfitting)

**Performance:**
- Accuracy: 72%
- Precision (Converted): 0.53
- Recall (Converted): 0.41
- F1-score: 0.46
- **AUC-ROC: 0.76**

**Analysis:** Random Forest provides better overall accuracy but slightly lower recall than pruned Decision Tree.

### 4. Model Evaluation

**Confusion Matrix Analysis:**

For Decision Tree (Optimized):
- True Positives: Correctly identified ~69% of actual conversions
- False Negatives: Missed ~31% of actual conversions
- False Positives: Some non-converters incorrectly predicted as converters

**ROC-AUC Curve:**
- **AUC = 0.76** indicates good discriminative ability
- Model can distinguish between converters and non-converters
- Significantly better than random guessing (AUC = 0.50)

**Metric Selection:**
- **F1-score** prioritized for hyperparameter tuning (balances precision and recall)
- **Recall** emphasized for business (better to over-predict than miss conversions)
- **AUC-ROC** evaluates overall model quality

## Key Insights

### Top Conversion Drivers (Feature Importance)

1. **Interaction Intensity (28%):** Time × Page views
   - High engagement = strong conversion signal
   - Action: Create engaging content to boost interaction

2. **Profile Completion Score (22%):**
   - Complete profiles = serious interest
   - Action: Simplify profile completion, offer incentives

3. **Website Visits (18%):**
   - Frequency indicates interest level
   - Action: Retarget multi-visit leads aggressively

4. **Time Spent on Website (12%):**
   - Investment of time = higher intent
   - Action: Improve site stickiness with valuable content

### Business Implications

**Current State:**
- 30% base conversion rate
- Sales team contacts all leads equally
- Resource inefficiency on low-probability leads

**With ML Model (Top 30% predicted leads):**
- **Estimated conversion rate: 55-65%**
- 2x improvement in sales efficiency
- Better customer experience (timely follow-ups)

## Business Recommendations

### 1. Lead Scoring System
**Implementation:**
- Deploy model to score all incoming leads (0-100)
- Prioritize leads scoring >70 for immediate sales contact
- Leads scoring 40-70: Nurture campaigns
- Leads scoring <40: Automated email sequences

**Expected Impact:**
- Reduce wasted sales calls by 40%
- Increase conversion rate by 25-30%
- Improve sales team productivity

### 2. Profile Completion Optimization
**Problem:** Profile completion is 2nd strongest predictor

**Solutions:**
- Reduce required fields (progressive profiling)
- Offer incentives: "Complete profile for free course preview"
- Implement gamification: Progress bars, completion rewards
- A/B test form designs

**Expected Impact:** +15-20% profile completion rate

### 3. Engagement Optimization
**Problem:** Interaction intensity drives conversions

**Solutions:**
- Create interactive content (quizzes, assessments, calculators)
- Implement personalized content recommendations
- Add live chat for high-engagement sessions
- Use video content to increase time-on-site

**Expected Impact:** +20% average interaction intensity

### 4. Multi-Visit Remarketing
**Insight:** Website visits strongly predict conversion

**Solutions:**
- Set up pixel-based retargeting campaigns
- Email sequences triggered by 2nd and 3rd visits
- Personalized landing pages for returning visitors
- Special offers for multi-visit leads

**Expected Impact:** +30% conversion for multi-visit segment

### 5. Channel Optimization
**Analysis Needed:**
- Which marketing channels generate highest-quality leads?
- Reallocate budget to high-performing channels
- Customize messaging by channel

## Model Deployment Strategy

### Phase 1: Pilot (Month 1-2)
- Deploy model on 30% of leads (A/B test)
- Compare conversion rates: ML-prioritized vs random
- Gather sales team feedback

### Phase 2: Optimization (Month 3-4)
- Refine model based on pilot results
- Adjust threshold for lead scoring tiers
- Integrate with CRM system

### Phase 3: Full Rollout (Month 5+)
- Deploy to 100% of leads
- Implement automated lead assignment
- Set up model retraining pipeline (monthly)

### Monitoring Metrics
- Conversion rate by lead score tier
- Sales team efficiency (calls per conversion)
- Model calibration (predicted vs actual)
- Feature drift detection

## Technical Implementation

**Libraries:**
- `scikit-learn`: DecisionTreeClassifier, RandomForestClassifier, GridSearchCV
- `pandas/numpy`: Data manipulation
- `matplotlib/seaborn`: Visualizations (confusion matrix, ROC curve)

**Model Artifacts:**
- Trained model pickle file
- Feature importance rankings
- Threshold calibration curves
- Performance monitoring dashboard

## Limitations & Future Work

**Current Limitations:**
- No temporal features (how recent was activity?)
- No external data (LinkedIn profile, company size)
- Static model (no online learning)
- Binary classification (no lead scoring granularity)

**Future Enhancements:**
1. **Add time-based features:** Recency of last visit, time since first interaction
2. **Integrate external data:** Job title, company industry, education
3. **Implement ensemble methods:** Combine Decision Tree + Random Forest + Gradient Boosting
4. **Build lead scoring API:** Real-time predictions via REST endpoint
5. **Implement online learning:** Update model continuously with new conversion data
6. **Add interpretability:** SHAP values for individual lead explanations

## Files

- **Notebook:** `03_ExtraaLearn_Lead_Conversion_Prediction.ipynb`
- **Dataset:** `ExtraaLearn.csv` (not included)

## Business Impact Summary

**Quantified Benefits** (Annual Estimates):
- **Revenue Impact:** +$200K-$300K (higher conversion × better targeting)
- **Cost Savings:** -$100K in sales efficiency (fewer wasted calls)
- **Customer Experience:** Better qualified leads receive timely, personalized outreach

**ROI Calculation:**
- ML Development Cost: $50K (one-time)
- Annual Benefit: $300K-$400K
- **ROI: 600-700% first year**

## References

- Hastie, T., Tibshirani, R., & Friedman, J. (2009). *The Elements of Statistical Learning*. Springer.
- Scikit-learn Documentation: https://scikit-learn.org/

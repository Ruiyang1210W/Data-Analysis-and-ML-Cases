# FoodHub Data Analysis

## Project Overview

This project analyzes food delivery order data for FoodHub, an online food aggregator platform connecting customers with restaurants in New York City. The analysis focuses on understanding demand patterns, operational efficiency, and customer behavior to drive business improvements.

## Business Context

FoodHub operates in the competitive food delivery market alongside players like Uber Eats, DoorDash, and Grubhub. Success requires:
- Understanding restaurant and cuisine preferences
- Optimizing delivery operations
- Maximizing revenue through strategic pricing
- Improving customer satisfaction and retention

**Business Model:**
- 25% commission on orders > $20
- 15% commission on orders $5-$20

## Dataset

**Size:** 1,898 food delivery orders

**Features:**
- `order_id`: Unique identifier for each order
- `customer_id`: Unique customer identifier
- `restaurant_name`: Name of the restaurant
- `cuisine_type`: Type of cuisine ordered
- `cost_of_the_order`: Total order cost ($)
- `day_of_the_week`: Weekday vs Weekend
- `rating`: Customer rating (1-5) or "Not given"
- `food_preparation_time`: Minutes from order to pickup
- `delivery_time`: Minutes from pickup to delivery

**Data Quality:** No missing values; 736 orders (38.8%) without ratings

## Key Findings

### Restaurant Performance

**Top 5 Restaurants by Order Volume:**
1. Shake Shack (219 orders)
2. The Meatball Shop (132 orders)
3. Blue Ribbon Sushi (119 orders)
4. Blue Ribbon Fried Chicken (96 orders)
5. Parm (68 orders)

**Promotional Offer Eligibility** (Rating count > 50 AND Avg rating > 4.0):
- Blue Ribbon Fried Chicken: 64 ratings, 4.33 avg
- Blue Ribbon Sushi: 73 ratings, 4.22 avg
- Shake Shack: 133 ratings, 4.28 avg
- The Meatball Shop: 84 ratings, 4.51 avg

### Cuisine Preferences

**Overall Most Popular:**
1. American (highest volume)
2. Japanese
3. Italian
4. Chinese

**Weekend Preferences:**
- American: 415 orders
- Japanese: 335 orders
- Italian: 207 orders

### Operational Metrics

**Food Preparation Time:**
- Minimum: 20 minutes
- Average: 27.4 minutes
- Maximum: 35 minutes

**Delivery Time:**
- Minimum: 15 minutes
- Average: 24.2 minutes
- Maximum: 33 minutes

**Total Time (Preparation + Delivery):**
- 10.24% of orders exceed 60 minutes (potential customer dissatisfaction)
- Weekday mean delivery: 28.3 minutes
- Weekend mean delivery: 22.4 minutes

**Insight:** Weekend deliveries are faster despite higher order volume, suggesting better operational efficiency or different geographic distribution.

### Revenue Analysis

**Order Value Distribution:**
- 29.2% of orders exceed $20 (high-margin segment)
- Total revenue from analyzed dataset: $3,865.57

**Revenue Optimization Opportunity:**
- Focus marketing on high-value orders (>$20) for 25% commission
- 70.8% of orders are in lower margin tier

### Customer Behavior

**Top 3 Most Frequent Customers:**
- Customer 52832: 13 orders
- Customer 47440: 10 orders
- Customer 83287: 9 orders

**Rating Behavior:**
- 38.8% of customers don't provide ratings
- Opportunity to improve feedback collection

## Data Visualizations

The analysis includes:
- **Histograms:** Distribution of order costs, preparation times, delivery times
- **Box plots:** Identifying outliers in operational metrics
- **Count plots:** Restaurant popularity, cuisine preferences, day-of-week patterns
- **Violin plots:** Comparing numerical metrics across weekdays/weekends

## Business Recommendations

### 1. Operational Efficiency
**Problem:** 10.24% of orders take >60 minutes

**Solutions:**
- Implement real-time tracking dashboards for restaurant partners
- Allocate delivery personnel based on historical demand patterns
- Flag restaurants with consistently slow preparation times
- Optimize delivery routing algorithms

**Expected Impact:** Reduce late deliveries by 30-40%, improve customer satisfaction

### 2. Revenue Optimization
**Problem:** Only 29% of orders in high-margin tier

**Solutions:**
- Promote bundle deals and meal combos to increase order values
- Implement minimum order thresholds for free delivery
- Partner with restaurants on premium menu items
- Target marketing campaigns during high-value order times

**Expected Impact:** Increase average order value by 15-20%

### 3. Customer Engagement
**Problem:** 38.8% of orders lack ratings

**Solutions:**
- Implement gamification: reward points for ratings
- Send targeted post-order emails with rating incentives
- Offer small discounts on next order for rating submission
- Simplify rating interface (one-click ratings)

**Expected Impact:** Increase rating participation to 70-80%

### 4. Restaurant Partnerships
**Opportunity:** Support near-threshold restaurants

**Solutions:**
- Provide analytics dashboards to restaurant partners
- Offer marketing co-op for restaurants close to promotional thresholds
- Help optimize menu pricing and preparation efficiency
- Create featured restaurant campaigns

**Expected Impact:** Improve restaurant retention and platform quality

### 5. Weekend Operations
**Insight:** Faster deliveries on weekends despite higher volume

**Solutions:**
- Analyze weekend staffing patterns for best practices
- Replicate weekend efficiency strategies on weekdays
- Consider dynamic pricing based on delivery time guarantees

**Expected Impact:** Reduce weekday delivery times by 10-15%

## Technical Approach

### Exploratory Data Analysis (EDA)
1. **Univariate Analysis:** Distribution of individual variables
2. **Multivariate Analysis:** Relationships between variables
3. **Correlation Analysis:** Numerical variable relationships
4. **Segmentation:** Weekday vs weekend patterns

### Statistical Methods
- Descriptive statistics (mean, median, std dev)
- Frequency distributions
- Correlation matrices
- Percentile analysis

### Tools & Libraries
- **pandas:** Data manipulation and aggregation
- **numpy:** Numerical computations
- **matplotlib/seaborn:** Data visualization
- **Jupyter Notebook:** Interactive analysis

## Key Insights

1. **Power Law Distribution:** Small number of restaurants drive majority of orders
2. **Weekend vs Weekday:** Different demand and operational patterns
3. **Rating Gap:** Significant opportunity to improve data collection
4. **Delivery Consistency:** Most orders delivered in 15-33 minute window
5. **Revenue Concentration:** High-value orders critical for profitability

## Limitations

- Dataset represents snapshot in time (no temporal trends)
- No customer demographic information
- Limited geographic data (delivery distance/zones)
- No information on cancelled or failed orders
- Missing external factors (weather, events, promotions)

## Future Analysis

1. **Time Series Analysis:** Seasonal trends, day-of-week patterns
2. **Customer Segmentation:** RFM analysis, clustering
3. **Predictive Modeling:** Demand forecasting, delivery time prediction
4. **Sentiment Analysis:** Review text analysis (if available)
5. **Geospatial Analysis:** Delivery heatmaps, zone optimization

## Files

- **Notebook:** `02_FoodHub_Data_Analysis.ipynb`
- **Dataset:** `foodhub_order.csv` (not included)

## Business Impact

This analysis provides actionable insights for:
- **Operations Team:** Optimize delivery logistics
- **Marketing Team:** Target high-value customers and orders
- **Product Team:** Improve rating collection mechanisms
- **Partnerships Team:** Identify restaurants for promotional campaigns

**Estimated Annual Impact** (extrapolated):
- Revenue optimization: +$50K-$100K
- Operational efficiency: -$30K in costs
- Customer satisfaction: +5-10 NPS points

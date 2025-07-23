# Startup Health Scoring Model

The given task outlines the methodology used to create a composite health score for 100 startups, similar to a credit score. 
The goal is to evaluate startup potential based on the indicators provided in the dataset.

1. Data Preprocessing and Normalization

The first step involved loading the `Startup_Scoring_Dataset.csv`. 
To ensure fair comparison across features with different scales, all numeric columns were normalized to a 0-1 range using Min-Max Scaling.

Handling Negatively Correlated Metrics:

For monthly_burn_rate_inr, where a lower value indicates a better outcome which means less money spent, all values in that column were inverted. 
After normalizing monthly_burn_rate_inr to a 0-1 range, the normalized value was subtracted from 1 (`1 - normalized_burn_rate`). This transformation ensures that:
- A very low burn rate (good) results in a normalized value close to 1.
- A very high burn rate (bad) results in a normalized value close to 0.
This aligns its contribution positively with the overall composite score, meaning a higher inverted normalized burn rate contributes more positively to the final score.

2. Custom Scoring Formula and Feature Weighting

A custom scoring formula was designed to generate a composite score out of 100. This formula is a weighted sum of the normalized features. 
The choice of weights reflects my assessment of each feature's importance in determining a startup's potential:

- Monthly Active Users (0.30): Given the highest weight. This metric is a direct indicator of product-market fit, user engagement,
and traction, which are often the most critical factors for early-stage startup success and future growth.

- Market Size (0.20): A larger, more accessible market is crucial for scalability and long-term growth potential. Even with a great product, a small market limits ultimate success.

- Team Experience (0.15): A strong team is fundamental. Experienced founders are more likely to navigate through hardships, and execute their vision effectively.

- Valuation (0.15): Reflects market perception and investor confidence. A higher valuation generally indicates external validation of potential.

- Funds Raised (0.10): Indicates investor confidence and provides the necessary power for operations and growth. 
However it's less important than actual traction or market size as money alone doesn't guarantee success.

- Monthly Burn Rate (0.10, inverted): Startups will initially have a higher burn rate and cannot be a good indicator of success in early stages. Hence it has a lower weight.


3. Ranking and Interpretation

All 100 startups were ranked based on their calculated composite scores.

Insights: 

The top-performing startups typically exhibited a strong combination of high monthly active users, large market size, and experienced teams, coupled with reasonable burn rates. 
Conversely, the bottom-performing startups often showed deficiencies in these key areas. A startup with low monthly active users, a small market, and potentially a high burn rate would naturally rank very low. 
The ranking clearly highlights that traction (monthly active users) and market potential are highly influential in this scoring model, reflecting their importance in real-world startup evaluation.

4. Visualizations
 
- Bar Chart: Provides a clear visual representation of the score distribution across all startups, making it easy to see the range and identify clusters of high/low performers.
- Correlation Heatmap: Shows the relationships between the original input features. This can reveal if funds raised are highly correlated with valuation, or if team experience correlates with market size.
- Score Distribution Histogram: Illustrates how the composite scores are distributed. It helps understand if scores are clustered around an average or if there are distinct groups of high and low scorers.

Conclusion

This model provides a foundational framework for startup scoring. The choice of weights and the handling of negative metrics are critical design decisions that can be refined.
If available, incorporating time-series data for metrics like burn rate could allow for analysis of trends and growth trajectories, which are crucial for dynamic startup evaluation.

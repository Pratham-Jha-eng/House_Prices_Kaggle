# House_Prices_Kaggle
An end-to-end regression project to predict house prices, featuring comprehensive EDA, feature engineering, and an XGBoost model.
Predicting House Prices in Ames, Iowa
This repository contains an end-to-end machine learning project to predict house prices for the Ames, Iowa dataset from the Kaggle competition. The project involves comprehensive data exploration, feature engineering, and model training, culminating in an XGBoost model that achieves a competitive Kaggle score.

Final Kaggle Score: 0.15

Project Workflow
The project followed a structured workflow, moving from data understanding to predictive modeling.

1. Data Exploration and Visualization
The initial phase involved a deep dive into each feature to understand its relationship with SalePrice. This was a critical step to build intuition and guide the feature selection process.

Numerical Features (GrLivArea, YearBuilt, etc.): Analyzed using scatter plots to identify linear trends and potential outliers.

Categorical Features (Neighborhood, OverallQual, etc.): Analyzed using boxplots to visualize the distribution of SalePrice for each category. This was crucial for identifying which categories had a significant impact on price.

2. Feature Engineering & Selection
This was the most critical phase. Features were not just included based on intuition, but on the evidence gathered from the visualization step. The goal was to select features with a strong, clear signal and discard those that were noisy, redundant, or had low variance.

Key Feature Selection Decisions:
Features We Kept (The "Goldmines"):

OverallQual & ExterQual: These were top-tier features. Their boxplots showed a perfect "staircase" pattern, where each increase in quality rating led to a clear and predictable increase in the median SalePrice. This strong, ordered (ordinal) relationship is ideal for a predictive model.

GrLivArea & TotalBsmtSF: These numerical features showed a strong, positive linear relationship with SalePrice in their scatter plots. The trend was clear: as the square footage increased, the price consistently increased.

GarageFinish: This feature was chosen over the noisier GarageType. Its boxplot showed a clean ordinal trend (Unfinished < Rough Finished < Finished), providing a direct and reliable signal of quality and value.

Neighborhood: The boxplot for Neighborhood showed significant variation in median prices between different areas (e.g., 'NridgHt' vs. 'Edwards'), confirming that location is a primary driver of price.

Features We Dropped (The "Noise"):

OverallCond & ExterCond: These features were dropped because their boxplots were noisy and counter-intuitive. The most common category, "Typical/Average," had a massive price variance and the medians did not follow a logical order, indicating a poor signal-to-noise ratio.

Heating & Electrical: These were dropped due to having near-zero variance. The boxplots showed that over 95% of houses fell into a single category (GasA or SBrkr), providing no useful information to differentiate between houses.

MiscFeature: This feature was dropped because after filling missing values with 'None', the 'None' category dominated the dataset. The other "golden" features like 'Tennis Court' were too rare to be statistically reliable, representing lottery-ticket-like events that would likely cause overfitting.

Feature Engineering Steps:

Handling Missing Values: Missing values were imputed strategically. For example, LotFrontage was filled with the median of its respective Neighborhood, and missing garage/basement information was filled with 'None' or 0 after confirming the data was missing by design.

Grouping Rare Categories: For nominal (unordered) features like SaleCondition, categories with very few samples were grouped into a single 'Other' category. This prevents the model from overfitting to rare events and increases the statistical power of the feature.

3. Data Preprocessing
Before modeling, the data was prepared for machine learning algorithms.

Log Transformation: The target variable, SalePrice, was highly skewed. A logarithmic transformation (np.log1p) was applied to make its distribution more normal, which is a key assumption for many models.

Dummy Variables: Categorical features were converted into a numerical format using pd.get_dummies. This one-hot encoding allows the model to interpret categorical data without assuming a false order.

4. Modeling
The project progressed through several models to find the best performance.

Linear & Ridge Regression: These were used as initial baseline models. Their poor performance on the Kaggle leaderboard indicated that the relationships in the data were too complex and non-linear for a simple linear model to capture.

XGBoost (Extreme Gradient Boosting): The final model was an XGBRegressor. This powerful, tree-based model was chosen for its ability to capture complex, non-linear relationships and interactions between features, which was essential for achieving a high score.

5. Results and Conclusion
The final XGBoost model achieved a score of 0.15 on the Kaggle leaderboard, a significant improvement over the baseline linear models. This result validates the feature engineering decisions and the choice of a more complex, non-linear model.

Future improvements could include hyperparameter tuning of the XGBoost model using GridSearchCV or RandomizedSearchCV to further optimize performance.

How to Run This Project
Clone the repository.

Ensure you have the necessary libraries installed (pandas, numpy, scikit-learn, seaborn, matplotlib, xgboost).

Place the train.csv and test.csv files in the data/ directory.

Run the House_Prices.ipynb notebook in a Jupyter environment.

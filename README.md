# UCB-MOD11
Understand what factors make a car more or less expensive using CRISP-DM
README — Used Car Price Prediction (CRISP‑DM Project)
Project Overview
This project explores a large dataset of used‑car listings with the goal of understanding what drives used‑car prices and building predictive models to support better inventory and pricing decisions for a used‑car dealership.
The project follows the CRISP‑DM framework:
Business Understanding → Data Understanding → Data Preparation → Modeling → Evaluation → Deployment.

1. Business Understanding
Used‑car dealerships must decide which vehicles to purchase, how much to offer, and how to price inventory.
The dealership wants to know:
Key Business Questions
	• What characteristics make a used car more (or less) valuable?
	• Can we build a model to predict fair market price?
	• How can these insights help guide purchasing and pricing decisions?
Business Objective
Provide actionable insights and data‑driven guidance on:
	• The strongest predictors of used‑car pricing
	• Models that can reasonably estimate fair value
	• Recommendations for optimizing inventory choices

2. Data Understanding
The dataset includes vehicle‑level attributes such as:
	• Price
	• Year
	• Odometer (mileage)
	• Manufacturer
	• Model
	• Condition
	• Cylinders
	• Fuel type
	• Transmission
	• Drive type
	• Title status
	• Vehicle type & size
	• Paint color
	• Region and state
Initial exploration revealed:
	• Missing values common in cylinders, paint_color, model, and some categorical fields.
	• Outliers in price (very high or zero values) and mileage.
	• High‑cardinality categories (e.g., region names).
These findings guided the Data Preparation phase.

3. Data Preparation
Cleaning Steps
	• Removed entries with missing or zero price.
	• Converted numeric fields (year, odometer, price) to proper numeric types.
	• Trimmed extreme price cases (1st–99th percentile).
	• Removed invalid or extreme odometer values.
Feature Engineering
	• Vehicle age = current year – model year
	• Cylinders_num = numeric extraction from "6 cylinders"
	• Condition score = ordinal mapping (salvage → new)
	• Is_clean_title = binary indicator for clean title
	• Rare categories bucketed for manageable modeling.
Transformations
	• Train/test split (80/20)
	• Standardization for numeric features
	• One‑hot encoding for categorical features
	• Optional: log‑transform of price inside TransformedTargetRegressor to stabilize variance
Leakage Prevention
All cleaning and transformations performed inside scikit‑learn Pipelines and ColumnTransformers, ensuring no knowledge from the test set leaks into training.

4. Modeling
Several regression models were trained and compared:
Model	Description
Linear Regression	Simple, interpretable baseline assuming linear relationships
Random Forest (RF)	Tree‑based ensemble averaging many trees; robust and non‑linear
Gradient Boosting (GBR)	Sequential tree ensemble optimizing errors; often strong performance
Hyperparameter Tuning
	• Initial grid search replaced with fast randomized search due to dataset size
	• Subsampled training set for tuning, then refit best models on full training
	• Evaluated models with MAE (average dollar error), RMSE, and R²

5. Evaluation
Key Findings
Across models, the strongest predictors of price are:
	1. Vehicle age
	2. Mileage (odometer)
	3. Vehicle condition
	4. Title status
	5. Manufacturer
	6. Vehicle type (e.g., pickup/SUV)
Model Performance
	• Linear Regression provided a simple baseline but struggled with non‑linear effects.
	• Random Forest and Gradient Boosting performed significantly better on MAE and RMSE.
	• Models were accurate enough to guide competitive pricing and evaluate potential purchases.
Feature Importance
Tree‑based models consistently ranked:
	• Age & mileage as the most influential predictors
	• Clean title, condition, and manufacturer also had significant weight

6. Deployment (Deliverables to Client)
Actionable Recommendations for Dealership
	• Prioritize younger, low‑mileage vehicles—they retain value best.
	• Avoid salvage/rebuilt titles unless priced deeply below market.
	• Invest more in trucks & SUVs, which show strong price retention.
	• Use the model’s predicted price as a fair‑value benchmark for assessing deals.
	• Identify underpriced listings by comparing list price with predicted fair price.
Deliverables Provided
	• Cleaned, transformed dataset ready for modeling
	• Multiple trained models with evaluation metrics
	• Feature‑importance charts and tables
	• A narrative explanation summarizing findings
	• A business‑facing report describing inventory strategy recommendations

7. Tools & Environment
	• Python
	• Pandas, NumPy
	• scikit‑learn (pipelines, transformers, Random Forest, Gradient Boosting, CV)
	• Matplotlib (optional charts)
	• Jupyter Notebook

8. How to Run the Notebook
	1. Place vehicles.csv in the same directory as the notebook.
	2. Run cells top‑to‑bottom.
	3. The notebook performs cleaning, feature engineering, modeling, and evaluation.
	4. Final output includes: 
		○ MAE/RMSE metrics
		○ Best model selection
		○ Feature importances
		○ Recommendations summary

9. Summary
This project provides a complete, CRISP‑DM–driven analysis of used‑car pricing.
The modeling confirms industry‑consistent pricing drivers and offers data‑backed guidance for inventory decisions.
The final output equips the dealership with insights to reduce risk, improve pricing accuracy, and identify profitable opportunities in the used car market.


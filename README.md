# Lagos Property Price Classification & Pricing Strategy

## Executive Summary
This project builds an end-to-end machine learning pipeline to identify high-priced property listings in Lagos, Nigeria. Using 3,656 listings, three classification models were evaluated to predict whether a property sells above the median price (₦295 million). The final Random Forest Classifier achieved an F1-Score of 0.81 and an ROC-AUC of 0.90 helping agents and buyers quickly judge whether a listing is priced high or low for the market.

## Dataset
- **Source:** Kaggle, "Lagos House Prices, Sales and Valuation Dataset" by ogwucheemmanueld. https://www.kaggle.com/datasets/ogwucheemmanueld/lagos-house-prices-sales-and-valuation-dataset
- 3,657 rows (3,656 after removing 1 duplicate), 20 columns, no missing values
- **Target:** `High_Price` = 1 if Price is above the median, else 0 (balanced: 1,830 vs 1,826)

## Key Insights & Visual Highlights
- **Primary Price Drivers:** Number of bedrooms, the island-and-bedrooms interaction and number of bathrooms are the top indicators of a high-priced listing.
- **Model Comparison:** Random Forest narrowly outperformed Gradient Boosting and Logistic Regression.

| Model | Accuracy | Precision | Recall | F1-Score | ROC-AUC |
|---|---|---|---|---|---|
| **Random Forest** | 0.827 | 0.887 | 0.749 | 0.812 | 0.898 |
| Gradient Boosting | 0.821 | 0.864 | 0.762 | 0.810 | 0.892 |
| Logistic Regression | 0.787 | 0.787 | 0.787 | 0.787 | 0.873 |

![ROC Curve Comparison](outputs/roc_curve_comparison.png)
![Feature Importance](outputs/feature_importance.png)

## Business Recommendations
1. **Price Screening:** Use bedrooms, bathrooms and location features as first filters when valuing a listing.
2. **Review Outliers:** Flag listings where the model's prediction disagrees with the asking price for manual review.
3. **Better Data:** Collect size (sqm) and year built to improve accuracy further.

## How to Reproduce
1. Clone repository: `git clone https://github.com/yourusername/lagos-property-capstone.git`
2. Install dependencies: `pip install -r requirements.txt`
3. Run pipeline: `python notebooks/olamilekanoyewolefirstproject.ipy`

## Repository Structure
```text
lagos-property-capstone/
├── data/
│   ├── Lagos_houses_prices.csv        <- Raw input dataset
│   └── cleaned_lagos_houses.csv       <- Preprocessed dataset
├── notebooks/
│   └── olamilekanoyewolefirstproject.ipy       <- EDA, scaling, 3-model comparison, charts
├── outputs/
│   ├── eda_charts.png
│   ├── roc_curve_comparison.png
│   └── feature_importance.png
├── .gitignore
├── requirements.txt
└── README.md
```

## Limitations
- 578 listings have 0 bathrooms and 305 have 0 bedrooms (possibly land or missing data)
- Neighborhood_Tier, Luxury_Score and several other columns were already in the file; their origin is unknown
- A median split gives a high/low answer, not an exact price

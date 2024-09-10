# Boston House Market Price Prediction

## Introduction
Housing is one of life's essential needs, along with food, water, and other fundamentals. As living standards improve, the demand for housing continues to rise. The housing market significantly impacts a country's economy and currency. Various factors influence housing sales prices, including the property area, location, construction materials, age, number of bedrooms, and garages.

A house price prediction model provides valuable insights into current market valuations for home buyers, property investors, and housebuilders. It assists in identifying features that match a buyer's budget and enables investors and builders to make informed decisions.

## Objective
The goal of this project is to predict housing prices in Boston suburbs based on various locality features. This includes identifying the most important features that affect house prices, preprocessing the data, and building regression models to predict prices for unseen data.

## Dataset
The dataset used for this project consists of records describing suburbs or towns in the Boston Standard Metropolitan Statistical Area (SMSA). It includes various attributes, such as crime rates, the proportion of residential land, and the median value of owner-occupied homes.

### Data Dictionary
| Attribute    | Description |
|--------------|-------------|
| **CRIM**     | Per capita crime rate by town |
| **ZN**       | Proportion of residential land zoned for lots over 25,000 sq.ft. |
| **INDUS**    | Proportion of non-retail business acres per town |
| **CHAS**     | Charles River dummy variable (1 if tract bounds river; 0 otherwise) |
| **NOX**      | Nitric oxide concentration (parts per 10 million) |
| **RM**       | Average number of rooms per dwelling |
| **AGE**      | Proportion of owner-occupied units built before 1940 |
| **DIS**      | Weighted distances to five Boston employment centers |
| **RAD**      | Index of accessibility to radial highways |
| **TAX**      | Full-value property-tax rate per $10,000 |
| **PTRATIO**  | Pupil-teacher ratio by town |
| **LSTAT**    | Percentage of lower-status population |
| **MEDV**     | Median value of owner-occupied homes in $1000s |

## Exploratory Data Analysis (EDA)
EDA was conducted to understand the structure of the dataset, detect patterns, and identify any anomalies. This step informed the data preprocessing and modeling strategies.

### Steps for EDA:
1. **Distribution of MEDV**  
   - Examined the distribution of the target variable, MEDV (median value of homes), to understand its central tendency, spread, and potential skewness.
   
2. **Correlation Heatmap**  
   - Analyzed the correlation between MEDV and other features, identifying strong relationships that guided feature selection.

3. **Univariate Analysis**  
   - Conducted individual analysis of each feature to detect patterns, potential outliers, and skewness.

4. **Bivariate Analysis**  
   - Explored relationships between features that exhibited significant correlations (>= 0.7 or <= -0.7) with each other and with MEDV.

5. **Skewness Check and Log Transformation**  
   - Checked the skewness of MEDV and applied a log transformation to normalize its distribution when necessary.

## Feature Engineering
Several transformations were performed to enhance the predictive power of the dataset:
- **Polynomial Features**: Created polynomial features for LSTAT to capture non-linear relationships.
- **Log Transformation**: Applied log transformations to skewed features like CRIM and DIS, creating new features (CRIM_log, DIS_log).
- **Interaction Features**: Created interaction terms (CRIM_LSTAT, AGE_LSTAT) to capture combined effects.
- **Binning and Encoding**: Binned AGE into categories (New, Moderate, Old) and encoded them into dummy variables.

## Data Preparation for Modeling
Standardized numerical features using the `StandardScaler` to ensure they were on a similar scale. This step is essential for machine learning algorithms to perform optimally.

## Initial Model Training and Evaluation
An initial linear regression model was trained using the preprocessed data. The model was evaluated using key performance metrics:
- **Mean Absolute Error (MAE)**: 0.3098
- **Root Mean Squared Error (RMSE)**: 0.4321
- **R-squared (R²) Score**: 0.7901
- **Mean Absolute Percentage Error (MAPE)**: 211.40%

## Variance Inflation Factor (VIF) Analysis
Calculated VIF values to detect multicollinearity among features. High VIF values were addressed by feature engineering, and the recalculated VIF values showed significant improvement.

## Cross-Validation Results
Performed cross-validation to evaluate the model's generalization:
- **Cross-Validation RMSE**: 0.5729 ± 0.2420  
This indicates consistent model performance across different subsets of the data.

## Regularized Regression Models
Explored Lasso and Ridge regression models to improve predictive performance:
- **Lasso Regression**: Best alpha = 0.01, RMSE = 0.6162
- **Ridge Regression**: Best alpha = 10, RMSE = 0.6200

These models did not significantly improve upon the initial linear regression model but provided insights into feature selection and multicollinearity handling.

## Checking Linear Regression Assumptions
Verified that the assumptions of linear regression were satisfied (linearity, independence, homoscedasticity, and normality) using diagnostic plots.

## Final Cross-Validation Results
The final model performance was consistent with the initial results, confirming that the linear regression model was well-suited for predicting housing prices with a low average prediction error.

## Conclusion
The analysis of the Boston housing data has provided valuable insights into the factors influencing house prices. The linear regression model demonstrated good predictive performance and identified significant predictors, including:
- **NOX, RM, RAD, TAX, PTRATIO, DIS_log, and CRIM_LSTAT** were the most significant predictors.
- **Model Performance**: The linear regression model outperformed Lasso and Ridge regression models.

### Recommendations
1. **Utilize Linear Regression for Prediction**: The linear regression model, with its lower RMSE, is recommended for predicting housing prices.
2. **Leverage Lasso for Feature Selection**: While Lasso did not outperform linear regression, its feature selection capability can simplify models by identifying the most significant predictors.

### Policy and Planning Insights:
1. **Improve Air Quality**: Reducing nitric oxide (NOX) pollution can potentially increase property values.
2. **Promote Larger Living Spaces**: Developing properties with more rooms (RM) can boost property values.
3. **Enhance Infrastructure**: Improving accessibility to radial highways (RAD) positively impacts property prices.
4. **Invest in Educational Quality**: Enhancing the pupil-teacher ratio (PTRATIO) can raise property values.
5. **Urban Planning**: Shorter distances to employment centers (DIS_log) increase property values, suggesting that urban planning should focus on reducing commuting times.

## Technologies Used
- **Python**
- **Pandas**
- **NumPy**
- **Matplotlib**
- **Seaborn**
- **Scikit-learn**
- **Statsmodels**

## License
This project is licensed under the MIT License. See the LICENSE file for more details.

# car-price-prediction[Automobile Price Prediction]

A machine-learning regression project that estimates automobile prices from vehicle specifications such as make, engine size, horsepower, curb weight, dimensions, and fuel economy.
Project overview
Problem type: Supervised learning — regression
Dataset: Automobile / Imports-85 dataset
Dataset size: 201 cars, 25 input features, and 1 target (`price`)
Target variable: `price`
Models compared: Linear Regression, Decision Tree Regressor, Random Forest Regressor, and Gradient Boosting Regressor
Evaluation metrics: Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), and R²
The project explores the data, handles missing values, visualizes relationships between vehicle features and price, preprocesses numerical and categorical variables, and compares four regression models.



Objectives
Inspect the dataset and assess data quality.
Explore numerical and categorical variables using descriptive statistics and visualizations.
Identify features associated with automobile price.
Prepare data for machine learning while avoiding test-set leakage during imputation and preprocessing.
Train and compare multiple regression models.
Identify a candidate model and document limitations and possible improvements.


Dataset
The source file is `auto\_imports.csv`. It has no header row, so the notebook assigns the 26 column names manually. Missing values in the source data are represented by `?` and are converted to `NaN` when loaded.
The columns cover risk rating, make and body style, drivetrain and engine configuration, vehicle dimensions and weight, engine measurements, fuel economy, and price.
Important: Place `auto\_imports.csv` in the same directory as the notebook before running it. The dataset is not included in this repository unless you add it separately and have permission to redistribute it.


Tools and libraries
Python
Jupyter Notebook
pandas and NumPy
Matplotlib and Seaborn
scikit-learn


Workflow
1. Data loading and inspection
Read the headerless CSV with manually supplied column names.
Convert `?` markers to missing values.
Inspect dimensions, data types, summary statistics, duplicates, and missing values.
2. Exploratory Data Analysis (EDA)
The notebook uses:
Histograms to inspect numerical distributions
Box plots to inspect potential outliers
Count plots to understand categorical distributions
Scatter plots to inspect selected features against price
A correlation heatmap to explore relationships among numerical variables
A bar plot comparing average price by fuel type
The supplied project report records 201 rows and 26 columns, no duplicate rows, no missing target prices, and 51 missing feature cells. `normalized-losses` has the largest number of missing values.
3. Data preparation
The notebook creates a cleaned copy for EDA visualizations. That EDA copy is not used to train the models.
For modelling, the data is split into training and test sets using an 80/20 split and `random\_state=42`. Missing numerical values are filled with medians calculated from the training data only. Missing categorical values are filled with the most frequent training value. Numeric columns are scaled with `StandardScaler`, and categorical columns are one-hot encoded with `handle\_unknown="ignore"`.
4. Model training and evaluation
The notebook compares:
Linear Regression
Decision Tree Regressor
Random Forest Regressor (`n\_estimators=200`)
Gradient Boosting Regressor

Models are ranked by test-set RMSE. MAE and R² are also reported. The notebook includes model-comparison charts, an actual-versus-predicted plot, and a residual plot.

Results
The supplied project report identifies Gradient Boosting as the strongest candidate on the held-out test set. Its reported test metrics are approximately:
Metric	Reported result
MAE	$1,554
RMSE	$2,472
R²	0.950

The notebook's explanatory note records slightly different rounded results (MAE about $1,553 and RMSE about $2,469). Re-run the notebook from top to bottom to obtain the metrics for your current environment and use those freshly generated values in any final submission.
The supplied report also includes an additional 5-fold cross-validation check, with Gradient Boosting at approximately R² = 0.889 and RMSE = $2,191 ± $385. This cross-validation result is documented in the accompanying report; it is not implemented as a cross-validation cell in the uploaded notebook.
Key findings
Engine size, curb weight, horsepower, and width have strong positive relationships with price in the supplied analysis.
City and highway MPG have negative relationships with price.
The price distribution is right-skewed, with a smaller number of high-priced cars.
Several predictors are correlated, so individual feature relationships should not be interpreted as proof of causation.
The dataset is small and some categories have very few examples, limiting generalization.


How to run
Install Python and Jupyter Notebook.
Install the required packages:
```bash
   pip install numpy pandas matplotlib seaborn scikit-learn jupyter
   ```
Put `auto\_imports.csv` beside `automobile\_price\_prediction\_final.ipynb`.
Start Jupyter:
```bash
   jupyter notebook
   ```
Open the notebook and run all cells from top to bottom.
The notebook currently reads the dataset using the relative path `auto\_imports.csv`; running it from a different working directory may cause a file-not-found error.


Limitations
Only 201 cars are available.
Some categorical groups are rare or imbalanced.
Results can vary across train/test splits.
The data represents a particular market and period; prices may not reflect current market conditions or inflation.
The notebook does not perform hyperparameter tuning or cross-validation itself.
Model predictions show patterns in the data and do not establish causal effects.


Future improvements
Add cross-validation directly to the notebook.
Tune Gradient Boosting hyperparameters using cross-validation.
Test Ridge or Lasso regression as regularized linear baselines.
Evaluate a log transformation of the price target.
Collect more recent and more diverse vehicle data.
Save the complete preprocessing-and-model pipeline for reuse and validate it on external data before deployment.


Project structure
```text
project/
├── automobile\_price\_prediction\_final.ipynb
├── auto\_imports.csv
├── README.md
└── Automobile\_Price\_Prediction\_Project\_Report.docx
```

Conclusion
This project demonstrates an end-to-end regression workflow for automobile price estimation: data inspection, EDA, missing-value handling, feature transformation, model comparison, and evaluation. Based on the supplied results, Gradient Boosting is the leading model among the four tested candidates, but additional validation on larger and more current data is recommended before production use.

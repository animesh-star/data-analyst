# Student Performance Analysis & Academic Success Prediction

## Project Overview
This project applies data analytics and machine learning techniques to the Student Performance dataset (`student-mat.csv`), which records demographic, family, social, school-related, and academic information for 395 secondary-school students, along with their mathematics grades across three grading periods (G1, G2, and G3).

The project involves exploratory data analysis (EDA) to understand patterns between student characteristics and final academic performance, followed by the development of regression models to predict the final mathematics grade (G3). An interactive Power BI dashboard was also built to visually summarize the dataset's key indicators.

## Problem Statement
Educational institutions collect a wide range of information about their students, but this information is not always analyzed in a structured way to understand its relationship with academic outcomes. This project explores student performance data systematically — to identify which recorded characteristics show a meaningful association with final grades — and assesses whether such characteristics can be used to build a reasonably informative predictive model for final academic performance (G3), independent of a student's grades in earlier grading periods.

## Objectives
- Understand the structure and characteristics of the student performance dataset.
- Clean and prepare the dataset for analysis.
- Examine the distribution of students' final mathematics grades.
- Analyze relationships between student characteristics and final grades.
- Investigate factors such as study time, absences, and previous failures.
- Develop machine learning models for predicting final mathematics grades.
- Compare Linear Regression and Random Forest Regression.
- Evaluate the models using MAE, RMSE, and R².
- Create a Power BI dashboard to present the major findings visually.

## Dataset
- **Source file:** `student-mat.csv`
- **Records:** 395 students
- **Variables:** 33 columns (16 numerical, 17 categorical)
- **Missing values:** None
- **Duplicate rows:** None

Key variables include demographic details (`sex`, `age`, `address`), family background (`Medu`, `Fedu`), school-related attributes (`studytime`, `failures`, `schoolsup`), and academic grades across three grading periods (`G1`, `G2`, `G3`).

**Target variable:** `G3` — the student's final mathematics grade (0–20 scale).

## Technologies Used
- Python
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn (ColumnTransformer, Pipeline, StandardScaler, OneHotEncoder, LinearRegression, RandomForestRegressor, train_test_split, evaluation metrics)
- Jupyter / Google Colab Notebook
- Power BI (for the interactive dashboard)
- Microsoft Word (project report)
- Microsoft PowerPoint (project presentation)

## Project Workflow / Methodology
1. Load the dataset (`student-mat.csv`) into a pandas DataFrame.
2. Inspect the dataset structure (shape, data types, summary statistics).
3. Check for missing values and duplicate records.
4. Perform exploratory data analysis on the final grade and key predictor variables.
5. Generate a correlation heatmap across numerical variables.
6. Preprocess the data for modeling: median imputation and standard scaling for numerical features; most-frequent imputation and one-hot encoding for categorical features, combined using a scikit-learn `ColumnTransformer` within a `Pipeline`.
7. Split the dataset into training (80%) and testing (20%) subsets.
8. Exclude G1 and G2 from the primary model's input features, so predictions rely on student characteristics rather than prior grades.
9. Train and evaluate two regression models: Linear Regression and Random Forest Regression.
10. Compare model performance using MAE, RMSE, and R².
11. Build a Power BI dashboard using the same dataset to visualize key indicators.

## Exploratory Data Analysis
The EDA stage examined:
- **Final Grade (G3) Distribution:** Ranges from 0–20, mean ≈ 10.42, median = 11.
- **Study Time vs. Final Grade:** Weak positive correlation (r ≈ 0.10).
- **Absences vs. Final Grade:** Very weak correlation (r ≈ 0.03).
- **Previous Failures vs. Final Grade:** Clearest observed association — average G3 declines from ≈11.25 (0 failures) to ≈5.69 (3 failures), r ≈ −0.36.
- **Sex vs. Final Grade:** Mean G3 ≈ 9.97 (female) vs. ≈10.91 (male).
- **Age vs. Final Grade:** Weak-to-moderate negative correlation (r ≈ −0.16).
- **Mother's/Father's Education vs. Final Grade:** Weak positive correlations (r ≈ 0.22 and r ≈ 0.15 respectively).
- **School Support vs. Final Grade:** Students receiving support had a lower average grade (≈9.43 vs. ≈10.56) — reflecting that support is targeted at struggling students, not a causal effect.
- **Correlation Analysis:** G1 and G2 are strongly correlated with G3 (r ≈ 0.80 and r ≈ 0.91), which is why they were excluded from the primary predictive model.

## Machine Learning
- **Target Variable:** G3 (final mathematics grade)
- **Feature Selection:** All columns except G3, G1, and G2 were used as input features. G1 and G2 were deliberately excluded so the model predicts final performance from student characteristics rather than relying on the strong correlation between consecutive-period grades.
- **Train-Test Split:** 80/20 split — 316 students for training, 79 students for testing.
- **Preprocessing:** Numerical features — median imputation + standard scaling. Categorical features — most-frequent imputation + one-hot encoding. Combined via a scikit-learn `ColumnTransformer` and applied within a `Pipeline`.
- **Models Trained:**
  - Linear Regression
  - Random Forest Regression (`n_estimators = 300`, fixed random state)
- **Evaluation Metrics:** MAE, RMSE, and R² (R² is a regression metric describing proportion of variance explained — not the same as classification "accuracy").

## Model Results
Both models were evaluated on the same held-out test set (79 students):

| Model             | MAE   | RMSE  | R²    |
|-------------------|-------|-------|-------|
| Linear Regression | 3.395 | 4.196 | 0.141 |
| Random Forest     | 3.010 | 3.765 | 0.309 |

Random Forest produced a lower MAE, a lower RMSE, and a higher R² than Linear Regression on this test split — indicating a comparatively better, though still limited, fit. An R² of 0.309 means Random Forest explains roughly 31% of the variation in G3 on the test set, leaving the majority of the variation unexplained.

## Power BI Dashboard
An interactive Power BI dashboard (`Student_Performance_Dashboard.pbix`) was built using `student-mat.csv` to complement the statistical analysis performed in Python.

**KPI Cards:**
- Total Students
- Average Final Grade
- Average Absences
- Average Study Time

**Visualizations:**
- Final Grade Distribution
- Study Time vs Average Final Grade
- Absences vs Final Grade
- Previous Failures vs Average Final Grade
- Average Final Grade by Sex
- School Support vs Average Final Grade

## Key Findings
- The dataset (395 students, 33 variables) contains no missing values and no duplicate records.
- The final grade (G3) has a mean of approximately 10.42 and a median of 11.
- Previous failures show the clearest observed association with final grade: average G3 declines from ≈11.25 (0 failures) to ≈5.69 (3 failures).
- Weekly study time shows only a weak positive correlation with final grade (r ≈ 0.10).
- Absences show almost no linear correlation with final grade (r ≈ 0.03).
- Mother's and father's education levels show weak positive correlations with final grade (r ≈ 0.22 and r ≈ 0.15).
- G1 and G2 are strongly correlated with G3 (r ≈ 0.80 and r ≈ 0.91), which is why they were excluded from the primary predictive model.
- Random Forest Regression outperformed Linear Regression on the test set (MAE = 3.010, RMSE = 3.765, R² = 0.309 vs. MAE = 3.395, RMSE = 4.196, R² = 0.141).
- Even the better-performing model explains only around 31% of the variation in final grades when G1 and G2 are excluded, indicating that student characteristics alone are a limited predictor of final academic performance in this dataset.

## Project Structure
```
├── Student_Performance_Analysis.ipynb      # Jupyter/Colab notebook (EDA & analysis)
├── student-mat.csv                         # Dataset
├── Student_Performance_Project_Report.docx # Full written project report
├── Student_Performance_Presentation.pptx   # Project presentation slides
├── Student_Performance_Dashboard.pbix      # Power BI dashboard file
├── requirements.txt                        # Python dependencies
└── README.md                               # Project documentation
```

## How to Run the Project
1. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```
2. **Open the notebook:**
   - Locally: launch Jupyter Notebook/JupyterLab and open `Student_Performance_Analysis.ipynb`.
   - Or upload the notebook to Google Colab and open it there.
3. **Ensure the dataset is available:**
   - Place `student-mat.csv` in the same directory as the notebook (or upload it to your Colab session) so the notebook can load it.
4. Run the notebook cells in order to reproduce the analysis.

## Limitations
- The dataset is limited to 395 students from a specific mathematics course context and may not generalize to other subjects, schools, or student populations.
- The available variables do not capture every factor that could influence academic performance, such as classroom-level teaching quality or individual psychological factors.
- The evaluation results (MAE, RMSE, R²) are based on a single train/test split; results could vary with a different split or with cross-validation.
- The relationships described in the EDA are observed associations and do not establish causation.
- Both regression models leave a substantial share of the variation in final grades unexplained (R² of 0.141 and 0.309 respectively).
- The primary model deliberately excludes G1 and G2; including these earlier grades would likely yield substantially higher predictive performance, but this was outside the scope of the primary analysis.

## Future Scope
- Apply cross-validation to obtain more robust estimates of model performance.
- Experiment with additional regression algorithms and hyperparameter tuning.
- Explore a secondary model that includes G1/G2 for comparison purposes.
- Expand the dataset to other subjects or schools to test generalizability.

## References
- Dataset: Student Performance dataset (`student-mat.csv`)
- scikit-learn documentation
- pandas, numpy, matplotlib, and seaborn documentation
- Power BI documentation

## Author
Animesh Goswami

# Academic Performance Analysis using Multilevel and Mixed Modeling in R

## Project Overview

This project explores the academic performance of students, focusing on how various individual, classroom, and school/parental-level attributes affect a student's tendency to participate in class (as measured by raised hands) and overall performance. The analysis employs statistical models to explore relationships between these variables, particularly focusing on multilevel data.

## Authors
- Rebecca Ioffe
- Isabelle Phraner

## Utilities Used

The analysis was carried out using R and the following libraries:
- `tidyverse` for data manipulation and visualization
- `nlme`, `lme4` for mixed models
- `lmtest`, `sandwich` for statistical testing
- `effects` for visualizing effects of models
- `dplyr` for data wrangling

## Data

The dataset used in this project is titled `acad_perf.csv` and contains information on various attributes related to students' academic performance. It includes variables such as:
- **Place of Birth**
- **Raised Hands**
- **Gender**
- **Class (High, Middle, Low performance)**
- **Semester**
- **Parent School Satisfaction**
- **Discussion Participation**

### Data Cleaning

- Semester and gender variables were recoded for readability.
- A binary outcome variable, `result`, was created based on class performance (1 for middle or high-level, 0 for low-level).

## Models and Analysis

### Model 1: Linear Regression
We started by fitting a linear regression model to predict raised hands based on class performance and semester.

- **Formula**: `raisedhands ~ Class + Semester`
- **Significance**: The group effect (semester) appears statistically significant with a p-value near zero.

### Model 2: Mixed Effects Model (Intercepts Only)
To account for the hierarchical structure of the data, we fit an intercepts-only model with a random effect for GradeID.

- **Formula**: `raisedhands ~ 1 + (1 | GradeID)`
- **Intraclass Correlation Coefficient (ICC)**: A value of 1, suggesting extremely high correlation within groups.

### Model 3: Extended Mixed Effects Model
We extended the model by adding variables such as `Class`, `Discussion`, and `Parent School Satisfaction`.

- **Formula**: `raisedhands ~ Class + Discussion + ParentschoolSatisfaction + (1 | raisedhands)`
- The model showed significant improvement compared to the intercept-only model based on likelihood ratio tests.

### Model 5: Level-2 Variables
We added additional Level-2 variables like `StageID` and `PlaceofBirth` to further explore variability.

- **Formula**: `raisedhands ~ StageID + PlaceofBirth + (PlaceofBirth | ParentschoolSatisfaction)`
- **AIC**: Increased values indicated that some variables may be unnecessary, leading to further refinement.

## Visualizations
Plots were created to visualize residuals, variability in raised hands across different level-2 units, and the overall fit of the models. These visualizations helped identify trends and potential issues like overfitting.

## Conclusion

The final models demonstrated significant predictors of raised hands in class, with strong effects from class performance, parental satisfaction, and discussion participation. However, further refinement of the model is needed due to suspiciously high ICC values and other irregular statistics.

## Future Work

- Investigate potential causes of inflated ICC values and Chi-squared statistics.
- Rescale some variables for more interpretable results.
- Experiment with other modeling approaches to improve the prediction of academic performance.

## Example Plot Outputs
![Screenshot 2024-09-25 at 4 58 25 PM](https://github.com/user-attachments/assets/abe40b05-d22e-4c64-84aa-49ec89c820e7)
![Screenshot 2024-09-25 at 4 58 13 PM](https://github.com/user-attachments/assets/9ce52e73-3626-437f-9f2e-557e13f91810)
![Screenshot 2024-09-25 at 4 58 06 PM](https://github.com/user-attachments/assets/77b27017-7562-404b-b54d-6e2b9f5fb100)



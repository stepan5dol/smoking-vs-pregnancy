# Prediction of birth weight class using Gradient Boosting &amp; Feature Engineering
## Abstract
In this study, we explored a Kaggle [dataset](https://www.kaggle.com/datasets/debjeetdas/babies-birth-weight) containing information about mothers and their newborn children. We addressed data gaps, categorized the samples into gestation age groups and body weight classes, and conducted a statistical analysis. Our findings revealed a higher prevalence of smoking among mothers in the low body weight group. To focus on predicting low body weight using early features, we defined two body weight classes: 'Normal weight' and 'Low body weight.' We selected five features that could be determined before and during early stages of pregnancy for training machine learning models.

## EDA and Statystics
### EDA
The dataset provided by the authors initially consisted of a table with 7 features. Five of these features are related to the health of the mothers: `height`, `weight`, and `age` are numeric features, with any missing values filled in with the average; `parity` is a categorical feature indicating whether it is the mother's first pregnancy; and `smoke` is a categorical feature indicating whether the woman is a smoker.

The remaining two features provided are associated with the children: `bwt` (birthweight) and `gestation` (age of gestation at the time of birth). It is important to note that both low gestation age and low birth weight have negative implications for the future life of the child.

All numeric values have been converted to the metric system.

### Feature Engineering
To enhance the practical applicability of the analysis and simplify forecasting, we decided to categorize the gestation age into groups: `born preterm (0)`, `normal gestation age (1)`, and `postterm babies (2)`. We also classified the body weight into standard groups, including Macrosomia, Normal weight, Low body weight, Very low body weight, and Extremely low body weight. However, the dataset only includes three groups: `Macrosomia`, `Normal weight`, and `Low body weight`. Additionally, we considered replacing the mother's height and weight with the body mass index (BMI), as it may provide useful insights.

### Statistical analysis
Research showed all groups of weight throughout mothers, but there is no connection between BMI and birth
weight. There were a few extremely preterm infants in data, but no VLBW and ELBW children throughout them.
Also the correlation between gestation and birth weight was high (0.405), that might had influence on the
results of classification.[(Fig. 1)](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/2af4324ea9b116f120f714b19cc7771349c143ff/Figures/Figure%201.png) 
![Figure 1](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/2af4324ea9b116f120f714b19cc7771349c143ff/Figures/Figure%201.png)

Based on the observed distribution of smoking mothers across gestational groups, no significant correlation between these variables was found. However, a noteworthy finding is that the prevalence of smoking among women with children classified as low birth weight (LBW) is 1.65 times higher compared to women who gave birth to children with normal body weight  [(Fig. 2,](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/0922ed0d085ada7817a0516468458fe78608bde9/Figures/figure%202.png) [Fig. 3,](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/0922ed0d085ada7817a0516468458fe78608bde9/Figures/figure%203.png) [Fig. 4,](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/0922ed0d085ada7817a0516468458fe78608bde9/Figures/figure%204.png) [Fig. 5,](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/0922ed0d085ada7817a0516468458fe78608bde9/Figures/figure%205.png) [Fig. 6,](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/0922ed0d085ada7817a0516468458fe78608bde9/Figures/figure%206.png) [Fig. 7)](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/0922ed0d085ada7817a0516468458fe78608bde9/Figures/figure%207.png). $χ^2$ test was caried out showing significant differences betwen smoking and not smoking groups (p-value: 6.512350402416024e-05).

![Fig. 2](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/0922ed0d085ada7817a0516468458fe78608bde9/Figures/figure%202.png) ![Fig. 3,](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/0922ed0d085ada7817a0516468458fe78608bde9/Figures/figure%203.png) ![Fig. 4)](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/0922ed0d085ada7817a0516468458fe78608bde9/Figures/figure%204.png) ![Fig. 5,](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/0922ed0d085ada7817a0516468458fe78608bde9/Figures/figure%205.png) ![Fig. 6,](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/0922ed0d085ada7817a0516468458fe78608bde9/Figures/figure%206.png) ![Fig. 7)](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/0922ed0d085ada7817a0516468458fe78608bde9/Figures/figure%207.png) 

Considering all the aforementioned information, we propose addressing `the classification problem by grouping the children into two categories: Low body weight children and Normal weight children.` In this classification, we have included the macrosomal group within the Normal weight group due to the similar distribution patterns observed among smoking mothers across these groups.

## Machine learning
The AUC-ROC metric was selected for the binary classification task. Training, parameter selection, and validation were performed using cross-validation technique with RandomizedSearchCV. Due to the significant class imbalance (18.5 to 1), the bootstrapping technique was employed to equalize the class sizes.

Three models were trained to determine the most suitable model in this scenario: LightGBM, CatBoost, and XGBoost. Only XGBoost achieved metrics exceeding 95% on both the train and test samples.

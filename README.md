# Prediction of birth weight class using Gradient Boosting &amp; Feature Engineering
## Abstract
In this study, we explored a Kaggle [dataset](https://www.kaggle.com/datasets/debjeetdas/babies-birth-weight) containing information about mothers and their newborn children. We addressed data gaps, categorized the samples into gestation age groups and body weight classes, and conducted a statistical analysis. Our findings revealed a higher prevalence of smoking among mothers in the low body weight group. To focus on predicting low body weight using early features, we defined two body weight classes: 'Normal weight' and 'Low body weight.' We selected five features that could be determined before and during early stages of pregnancy for training machine learning models.

Among all the tested models, smoking emerged as the most significant feature. The best-performing model achieved an impressive ROC-AUC score of 94.8% on the test data, indicating its potential for accurately predicting low body weight in early stages. This outcome suggests that our model can be effectively utilized as a predictive tool for identifying cases of low birth weight.

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
results of classification.[(Fig. 1)]((https://github.com/stepan5dol/smoking-vs-pregnancy/blob/2af4324ea9b116f120f714b19cc7771349c143ff/Figures/Figure%201.png)) ![Figure 1](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/745e21926a13e33935f9dea4b6bd78b12f5923d9/Figure%201.png)

According to the distribution of smoking mothers among the groups of gestation, there is no connection between those facts. [(Fig. 2,](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/a60376266affbea1f3af5843eb4df70049f30571/figure%202.png) [Fig. 3,](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/a60376266affbea1f3af5843eb4df70049f30571/figure%203.png) [Fig. 4)](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/a60376266affbea1f3af5843eb4df70049f30571/figure%204.png) 

![Fig. 2](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/a60376266affbea1f3af5843eb4df70049f30571/figure%202.png) ![Fig. 3,](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/a60376266affbea1f3af5843eb4df70049f30571/figure%203.png) ![Fig. 4)](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/a60376266affbea1f3af5843eb4df70049f30571/figure%204.png) 

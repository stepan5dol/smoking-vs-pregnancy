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

Three models were trained to determine the most suitable model in this scenario: LightGBM, CatBoost, and XGBoost. Only XGBoost achieved ROC-AUC scores exceeding 95% on both the train and test samples, with LGBM and CatBoost achieving scores of 86.8% and 88.4% respectively. [(Fig. 8)](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/fd680a5cea3bed6f39a8c29df5d4579f19177f49/Figures/figure%208.png)

![Fig. 8](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/fd680a5cea3bed6f39a8c29df5d4579f19177f49/Figures/figure%208.png)

To assess the importance of features for prediction, feature importances were obtained using the built-in functionality of gradient boosting models. Additionally, the Permutation Importance technique from Scikit-learn was employed to validate the output quality. The significance of the `smoke` feature was given more weight in the evaluation, as reflected by the ROC-AUC score. [(Fig. 9](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/fd680a5cea3bed6f39a8c29df5d4579f19177f49/Figures/figure%209.png)
[10,](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/fd680a5cea3bed6f39a8c29df5d4579f19177f49/Figures/figure%2010.png)
[11)](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/fd680a5cea3bed6f39a8c29df5d4579f19177f49/Figures/figure%2011.png)

![Fig. 9](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/fd680a5cea3bed6f39a8c29df5d4579f19177f49/Figures/figure%209.png)
![Fig. 10](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/fd680a5cea3bed6f39a8c29df5d4579f19177f49/Figures/figure%2010.png)
![Fig. 11](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/fd680a5cea3bed6f39a8c29df5d4579f19177f49/Figures/figure%2011.png)

However, the Permutation Importance analysis yielded slightly divergent results [(Fig. 12)](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/1c450e5a8d0ef2083467d6939afac52e52eef455/Figures/figure%2012.png). Among the three models (LGBM, CatBoost, and XGBoost), smoking among mothers emerged as the second most important feature for LGBM and CatBoost, and the third most important for XGBoost predictions. Nevertheless, it is evident that the `smoke` feature retains considerable importance. Notably, it should be acknowledged that this feature is the only modifiable one within the given dataset.

![(Fig. 12)](https://github.com/stepan5dol/smoking-vs-pregnancy/blob/1c450e5a8d0ef2083467d6939afac52e52eef455/Figures/figure%2012.png)

## Conclusions
In conclusion, our analysis of the dataset on birth weight prediction using gradient boosting models and feature engineering techniques yielded several key findings:

1. The prevalence of smoking among mothers was significantly higher in the low body weight group compared to the normal body weight group.
2. We observed a strong correlation between gestation age and birth weight, indicating the importance of gestation age in predicting birth weight.
3. A chi-square test revealed a significant association between smoking and the likelihood of having a baby with low body weight.
4. Machine learning models, including LightGBM, CatBoost, and XGBoost, were trained to predict low body weight. XGBoost outperformed the other models, achieving ROC-AUC scores exceeding 95% on both the training and test datasets.
5. Feature importances were analyzed using the built-in functionality of gradient boosting models, and the Permutation Importance technique was employed to validate the results. The analysis consistently identified smoking as one of the most important features in predicting low body weight, although the exact ranking differed slightly between models.
6. The findings suggest that smoking is a significant factor contributing to the likelihood of having a baby with low body weight, emphasizing the importance of smoking cessation programs for expectant mothers.

Overall, our study highlights the value of machine learning models and feature engineering techniques in understanding the factors influencing birth weight and provides insights into the impact of smoking on infant health. Further research and interventions can be conducted based on these findings to improve birth outcomes and promote maternal and child well-being.

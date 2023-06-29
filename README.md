# Tree_Structures_Modeling_R

## 1.	Introduction of Forest Inventory
Continuous monitoring and managing natural resources through forest inventory of plantation is fundamental in forestry industries (Fankhauser, Strigul, and Gatziolis 2018). The main variable of traditional forest inventory is structural tree information, such as height and diameter at breast height (DBH). Based on those information can be obtained the volume of the trees which is of important for managers. In a traditional way forest inventory was done by intensive sampling field survey which are time-consuming, less accurate, and labor intensive, especially for comprise large scales (Means et al. 2000; White et al. 2016). 
Nowadays, LiDAR is considered the most advanced technology for forest inventory, because it is fully census, accurate, cost-saving, and be able to provides efficient workflow. LiDAR technology is involves modeling to get the DBH and volume. Previous study showed that LiDAR able to provide precision DBH information through regression model with RMSE of 4.9 cm (Popescu 2007).
## 2.	DBH Modeling
Transition from traditional forest inventory to LiDAR-based model need a quite huge amount of field data depend on the trees characteristics and variability (Huang, Price, and Titus 2000). In this case simulated building a model of Eucalyptus tree using field forest inventory, containing the tree height and tree DBH. The model will be obtained through linear regression.
LiDAR basically able to duplicated the trees structures in 3D perspective. However, for landscape scale like this case the LiDAR cannot reconstruction the whole tree’s structure perfectly. Fortunately, LiDAR able to provide accurate information of the tree height, tree canopy, ground, and other earth surface. Therefore, it is required to derive correlation between DBH and height of the trees using linear regression. 
### 2.1	Initial Assessment – R²
R-squared, also known as the coefficient of determination, is a statistical measure used to assess the goodness of fit of a regression model. It provides information about the proportion of the variance in the dependent variable that can be explained by the independent variables in the model.
R-squared values range from 0 to 1, where: 0 indicates that the independent variables explain none of the variance in the dependent variable. 1 indicates that the independent variables explain all of the variance in the dependent variable, resulting in a perfect fit.
Field inventory data that used in this model building process containing height and DBH information of two type tree species which is Eucalyptus and Acacia Crassicarpa.


After removing NA value, subset for Eucalyptus tree species, we will found the R² is 0.82. Since the correlation still not good enough and potentially to improved. It’s able to do with outliers removal with assumption the outliers considered as an error of field measurement.

### 2.2	Remove Outliers
Removing outliers referring to process to excluding the data that deviate significantly from the majority. Method used here is Z-score: by subtracting the mean and dividing by the standard deviation (Equation 1). Data points with a z-score above a certain threshold can be considered outliers and removed. 
Z Score=(x-x̅)/σ	(1)
Where, x = Standardized random variable. x̅ = Mean. σ = Standard deviation.
The threshold will be depend on how much confident interval that wanted. Let’s decided to choose 95% confident interval than the rest 5% data outside the Z-score threshold will be excluded (Figure 2). This threshold can be obtained from t-distribution table based on the confident interval and degree of freedom (sample size-1).  Another way, the t-value able to obtained using R base function and no need to look up to the t- distribution table.
 
Figure 2. Illustration of 95% confidence interval
The remaining data after outliers removal will be 383 which is exclude 25 data outside the Z-score threshold (between range -1.96 – 19.6). The result, R² increase from 0.82 to 0.90. Afterwards, the linear regression model was ready to build from our data.
Inside the section 2.3 below: “Plotting Linear Regression Model Result” you will see how the equation of DBH (Equation 2) derive from correlation with the tree height using linear regression model. 
DBH=0.33+(0.72×Height)

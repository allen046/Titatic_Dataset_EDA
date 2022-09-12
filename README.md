# Titatic_Dataset_EDA(Exploratory Data Analysis)

Dataset Used: titanic_dataset_csv(Kaggle) 

## Steps involved in the project
1. Preparation 
2. Examining the dataset, inspecting it's columns and attributes. 
3. Inspecting the dataset for further analysis. 
4. Consolidate the analysis in a concise packaged data dictionary.
5. Perform univariate analysis
6. Perform bivariate analysis
7. Perform multivariate analysis
8. Data Cleansing
9. Perform K means clustering 

(NB: Feature Engineering is not performed in this project.)

### 1. Preparation 

The following libraries are imported for data preparation and subsequent manipulation. 

`pandas` abbreviated as pd; for data analysis

`numpy` abbreviated as np; for numerical analysis and manipulation on lists

`matplotlib` abbreviated as plt; for data visualization

`seaborn` abbreviated as sns; for statistical modeling and visualization

`IPython.display`; for displaying images

`sklearn.preprocessing`; for normalizing and standardizing attributes

`sklearn.cluster`; for clustering and implementing K Means algorithm


Before delving into manipulating the datasets and performing various actions, the dataset needs to be thoroughly examined. Using the `.head()` method, we will get an overview of the dataset, it's attributes and variables. 

The index is set to the column that would uniquely identity the attributes. Index is set using `.set_index(col_name)`


### 2. Examining the dataset, inspecting it's columns and attributes. 
In this step, we will examine the dataset. 

The shape of the dataset is deciphered using `DataFrame.shape` to identify the number of the attributes and columns, `info()` method to get the information of the DataFrame and `describe()` to describe the data in the DataFrame. `describe()` would provide description of the count, standard deviation, max and min values in the DataFrame. 

### 3. Inspecting the dataset for further analysis. 

In this step, we find for null/missing values in the dataset. We generate a heatmap to identify the missing values in the columns. `sns.heatmap(DataFrame.isnull())` is used for this purpose. The percentage of missing data is plotted using `sns.displot(data=DataFrame.isna())`. This provides the distribution of the missing values. 

### 4. Consolidate the analysis in a concise packaged data dictionary.

The data types, missing values, count are packaged together in the data dictionary. This helps a clear and concise description of the variables. Also, the numerical and categorigal variables are segregated. 

### 5. Perform univariate analysis

Univariate analysis is the analysis of the all the variables independently. 
Here, the following analysis is performed
- Getting the relative frequency of the Survived variable to get the percentage of passengers who survived and those who didn't. `countplot()` shows the count of observations for those who survived and those who didn't. A percentage composition is plotted in a pie chart using `df['col_name'].value_counts().plot(kind='pie')`
- Similarly, the same aforementioned process is followed for Pclass, Sex, SibSp, Parch, and Embarked.
- From the univariate analysis, more passengers died(61.62%) than those who survived(38.38%).  
- This indicates that passengers with a lower socio-economic status (with a lower ticket bracket) were higher than the other passengers in the ship, i.e., Pclass with the lower class(3)
- There were more men(64.76%) than women(35.24%) in the ship.
- A greater percentage of passengers in the ship were with zero siblings/spouses.(68.2%)
-The percentage of passengers with no parents/children is the highest. (76.1%)
-The highest number of embarkations is at Southampton(72.4%), followed by Cherbourg(18.9%) and Queenstown(8.7%) having the lowest number of embarkations. 
- The plotting for variables Ticket and Cabin are unintelligible and require feature engineering. 
- We get the distibution of 'Fare' using `sns.distplot(df['Fare'])`; it is skewed between values 0 and 50 and doesn't follow a normal distribution. 
- Similarly, we get the distribution of age using `sns.distplot(df['Age'])`. It follows a normal distribution. 


### 6. Perform Bivariate Analysis
Bivariate analysis is performed by analysing 2 variables. 
- A pivot table is created with 'Survived as the index, with variables 'Age','SibSp','Parch','Fare' as values. 
  - This shows, People with a younger age have a greater chance of survival
  - People who paid more for the tickets have a greater chance of survival.
  - People with Parents/children have a greater chance of survival
  - People with a sibling/partner have a lesser chance of survival
- Pclass is split into classes based on their Survival using `df.groupby()`
- Similarly, 'SibSp', 'Parch', 'Sex', 'Embarked' are also split into categories based on their Survival. Bar grpahs are plotted for analysis. 
- Based on the analysis for Pclass and Survived, upper class passengers had a greater chance of survival with a 60% survival percentage, the middle class having a 45% survival percentage, while the lower class having the least percentage of survival with a meagre ~23-24%. This indicates that the chance of survival is skewed towards passengers with a greater socio-economic status.
-  The passengers on board with 3 parents/children had the greatest percentage of survival(~60%), followed closely by passengers with 2 and 1 parent(s)/child(ren). Passengers with 5 parents/children had the least percentage of survival while passengers with 0 children/parent(s) relatively low percentage of survival as well.
- The female sex had a greater percentage of survival(75%) compared to male(20%).
- The port of embarkation at Cherbourg had the highest survival percentage.
- For the distribution of Sex w.r.t. Fare, it indicates female passengers purchased tickets with a higher fare.
- For the distribution of Survived w.r.t. Age, people with a younger age had a slightly greater chance of survival. 
- For the distribution of PClass w.r.t. Age,  upper class passengers are of older age than the rest of the passengers with middle class and lower class socio economic brackets. The lower class passengers have the youngest age bracket.
- For the distribution of Survived w.r.t. Age,  passengers who paid a higher fare have a greater chance at survival. 
- Pivot Tables for comparisons between Survived and PClass, Survived and Sex, Survived and Embarked are created along with the count using `aggfunc=count` to further the aforementioned analysis. 

### 7. Perform multivariate analysis
- This is performed to identify correlations between variables. 
- Parch(Parents/children) and SibSp(siblings/parents) have a strong positive correlation. Furthering the analysis that families tend to stick together.
- Survived and Fare have a positive correlation, indicating fare of the ticket plays an important role in the chance for survival.
- There is a strong negative correlation between Survived and PClass, Pclass and age, age and sibsp, fare and Pclass

### 8. Data Cleansing

- To mitigate the null values in the Age column, a boxplot of Survived wrt Age is plotted to get the mean of Age. This mean value will be used to fill up the null values.
- A function is defined to get the mean ages for the both the conditions to fill up the missing values.
- Plotting a heatmap would result in the removal of all null values in the Age column.
- Since, feature engineering is not performed here, Cabin is dropped. 

### 9. Perform K means clustering 

- Age column is moved to a new DataFrame. 
- Since age is already normalized, we scale using `StandardScaler()` to fit the Age.
- K Means will cluster all the datapoints to their centroids. 
- `kmeans= KMeans(n_clusters=i)` will generate the number of clusters and the number of centroids.
- `kmeans.intertia_` we will calculate the distance between each data point and its centroid.
- Optimal number of clusters is selected using 'Within cluster sum of squares method'. Here the no. of clusters=2
- The shape of the centroid is used to form clusters.
- Then we perform inverse transfromation to get the clusters for Age
- Histograms are plotted to display the distribution for the clusters of Age. 


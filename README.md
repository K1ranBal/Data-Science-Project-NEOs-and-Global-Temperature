# Data-Science-Project-NEOs-and-Global-Temperature
Data science project analysing research question on whether NEOs impact changes of Earth's climate.
## Portfolio Link: https://kb-datascience.github.io/KB.github.io/ 

# Research Question
Are changes in global temperatures correlated with historical near-earth-object (NEO) impacts, is there a relationship between the two? 

# Exec Summary
This research explores whether there is a relationship between NEOs and global temperature changes by using statistical methods; correlation, K-means and regression to analyse historic NEO characteristics and temperature reports. Initially no strong linear correlations were found which led to clustering NEOs based on characteristics; magnitude and distance from Earth, by using K-means. Although successful clustering was applied, the regression model produced a weak relationship, R<sup>2</sup> = 0.17. Results suggest NEOs do not have a significant influence on climate changes, however further analysis can be conducted to improve the data, shedding more light on climate change and extraterrestrial influencers. 

# Introduction
Climate change is one of Earth’s largest concerns, with temperatures increasing by 1.36 degrees (2023) compared to the 19th century. Statistics show that the last 10 years have been the warmest recorded since 1884. (NASA, 2024). A study was done to determine the environmental perturbations caused by asteroid or comet impacts but what if we could determine these before impact?

NEOs have consequential impact on sudden climate change, with the latest technology available from NASA we can analyse predicted NEOs and their characteristics helping us identify impactful events and their potentially destructive effects like climate change – preparing us for the future.

If a relationship is determined, we can use the historical data to predict the impact on temperatures, based on the criteria of NEOs, we can use this prediction model to prepare for NEOs that impact Earth’s climate and mitigate earlier resulting in a safer future for mankind.

# Analysis Outline
### Data Sources
1.	Near Earth Objects 1900 to 2200: Near Earth Objects 1900 to 2200 (kaggle.com)
 Variables: 	NASA NEO ID, Name, Date & Time, Min Distance to Earth, Max Distance to Earth, Velocity, Magnitude, Diameter, Rarity.
2.	NASA - Near Earth Objects: NASA - Nearest Earth Objects (kaggle.com)
 Variables: 	NASA NEO ID, Est Diameter Min, Est Diameter Max, Velocity, Miss Distance, Absolute Magnitude, Hazardous.
3.	NASA NEO Earth Close Approaches: NASA Near Earth Objects Information (kaggle.com)
 	Variables: 	NASA NEO ID, Object, Absolute Magnitude, Threat Flag, Min Diameter of NEO.
4.	Global Surface Temperatures Data (NASA): Global Surface Temperatures Data By NASA (kaggle.com)
 Variables: 	Global Temps: Year, Month, Temperature. 
             Northern Hemisphere (NHem) Temps: Year, Month, Temperature.
             Southern Hemisphere Temps (SHem): Year, Month, Temperature.
             Zonal Temps: Year, Global, NHem, SHem, Zones, Temperature.

Justification: All datasets have been chosen as they score high on completeness, credibility and compatibility. They are large in volume allowing for robust analysis and reliable modelling. They contain key variables on characteristics and temperature, which can be split by terrestrial coordinates for future research, that are crucial in addressing the research question.

Risks: A correlation may be found between NEOs and climate changes however other factors can contribute to temperature changes, we may not be able to prove causation based on correlation solely from this data. There is also a risk of the model overfitting from using a large amount of data, which can result in an inability to generalise newer data reducing performance of the model. 



### Data Preparation

To prepare the data, Feature Manipulation Engine (FME) is used to join the four datasets into a single table schema for ease of conducting in-depth analysis. Dataset 1 is the primary schema as it holds key fields to join both dataset 2 (ID to ID) and dataset 3 (Name to Object). Repeating columns of data are removed to reduce unnecessary noise and increase optimisation of the workbench. Data cleansing is applied to remove null rows where full data is not present to ensure a robust dataset. Duplicate ID entries are removed to minimise skewness within the model at analysis stage. Dataset 4 is then joined to match yearly temperatures to the date stamp within the NEO dataset to allow for correlation statistics and regression to be performed within the analysis.
 **ETL diagram and FME workbench can be found in the data prepration folder**

### Data Analysis

Exploratory Data Analysis (EDA) is performed initially to identify linear relationships between NEO variables and climate changes. No significant relationships were determined meaning the interaction of variables are more complex. K-means clustering is then initiated to group the NEOs by the most influential relationships/characteristics. This method is used to uncover patterns of similar behaving NEOs, reducing dimensionality and increasing computation efficiency in the large dataset. Secondary EDA is implemented to understand the descriptive statistics and distribution of temperature by clusters supporting validation. Clustering is taken forward for further statistical analysis; linear regression to discover whether there is a relationship. The regression model is imperative for predictive analysis so we can understand the behaviours of NEOs in the future and their potential impacts.

# Results
Initial EDA analysis shows no significant correlation between temperature and variables within NEO data. Relative velocity shows the highest value of R2 at 0.3 and Rarity shows a negative R2 of 0.33 however, individually these variables are not strong enough to build a regression model from.

At this point K-means clustering is initiated to group characteristics of NEOs together; relative velocity (speed), miss distance (distance from earth at point of passing orbit) and absolute magnitude (size). Although absolute magnitude shows one of the weakest correlations, these three variables have been grouped as physical characteristics that are most likely to determine the threat to Earth.

During K-means clustering, the three variables were normalised as the units of measurement were significantly different, this ensures accuracy when performing the K-means algorithm. Initial centroids were chosen at random from the normalised data points, which were calculated and recalculated to the point of stabilisation (the change between centroids after each iteration was almost non-existent). 

The number of clusters (K values) have been determined by using the Elbow method, using the within-cluster sum of squares (inertia) value for a range of K values. The inertia at each K value was plotted on a line chart, where the ‘elbow point’ was shown as K=4: determining 4 as the optimal number of clusters to use for this data.

Descriptive statistics were performed on variables within each cluster to better understand the behaviours of a cluster.

Distribution charts paired with the descriptive statistics help understand the left-skewness; most of the temperature values are on the higher end of the scale between each cluster meaning there is a risk of imbalanced data. Lower temperature outliers in each category are spotted which can drastically affect the performance of the regression model. 

Finally linear regression was applied to the data resulting in a weak correlation where R<sup>2</sup> = 0.17, it is unlikely that the NEO variables influence the temperature. However the Standard Error (SE) = 0.2 indicating that the model predictions are close to the actual data points, potentially explained by the wide range of temperatures in each cluster. The minimum and maximum range of temperatures were between -0.5 and 1 for all clusters. The P value of the model was 0 resulting in rejecting the null hypothesis: NEOs have no impact on changes in global temperature. Overall the R<sup>2</sup> value is not strong enough to prove causation of the research question however there is potential for further analysis to be conducted, splitting the data by its spatial properties to introduce granularity by region and month strengthening the value of R<sup>2</sup>. 

**Results workbook can be found in analysis folder**

# Conclusion
NASA historical NEOs have been used for this research to determine if a model can be built to predict expected climate change in future. Research papers demonstrate scenarios where NEOs collide with Earth and result in drastic climate change (Chapman, 2003), this research uses statistical analysis to predict scenarios of NEOs that may contribute to climate change.

The results of the model determine a weak correlation between the variables chosen in NEOs and temperature changes. Whilst this research shows merits in clustering NEOs by most significant variables, there are some limitations within the data specifically its outliers that affect the performance of the regression. A future recommendation would be to address outliers in each cluster to achieve normal distribution. Finally further analysis can enhance this research where we match NEOs orbit coordinates to terrestrial coordinates in Global Temperatures, then re-train the regression model for a strengthened and improved value of R<sup>2</sup> based on their position on Earth. 


# Introduction
Climate change in recent years has become a subject of global focus, with growing demand for extensive analysis and understanding of global temperature trends. The aim of this research is to perform a detailed exploration of global land temperature data between the year 1900 to 2010 and create a forecasting model for the years 2011 to 2015 using state-of-the-art tools, especially PySpark and Pandas.

# Dataset
The data used in this research was collected from Berkeley Earth, and it contains high resolution land and ocean time series data, aggregating 1.6 billion temperature readings from 16 pre-existing archives. The focus of this research is on a subset of the Global Land Temperature Dataset concentrating on five countries: Brazil, India, Kenya, United Kingdom, and United States. 
The subset of countries investigated represents a varying spectrum of geographic locations and climate attributes, serving as a miniature representation of the world climate system. Brazil represents the tropical region of South America, India embodies the complexities of a country with diverse climate zones, Kenya showcases a subtropical climate while the United Kingdom and United States are representations of countries with temperate climates.
Dataset is publicly available at https://berkeleyearth.org/data/ 

# Data Exploration
I applied SQL queries and Pandas for indepth data exploration. SQL queries like count, groupby, orderby and agg were useful in extracting important insights from the dataset. 
The dataset contains 4 variables dt, AverageTemperature, AverageTemperatureUncertainty, and Country. Total number of observations in the dataset before cleaning were 577462. Total number of countries were 243.
Pandas along with other python libraries, Seaborn and Numpy were very useful in the exploratory data analysis to create insightful visualizations.

![image](https://github.com/user-attachments/assets/26aba290-bcdd-4eaa-a4fb-e11aea38619b)

Top left is Box plot showing temperature variations for each country, Top right is line plot depicting a steady increase in average global land temperature over the years and this is in line with the trend of Global warming. Bottom left is a line plot showing monthly average temperature for UK. UK is seen to be hottest in July and coldest in January. Bottom right is seasonal decomposition of Brazil time series into trend, seasonal and residual component. The seasonal variation is the same magnitude over time and this indicates an additive decomposition

# Data Preprocessing
I used the count function to check for null values in the dataframe and dropped them. I converted the dt column to a date type then I extracted observations from 1900 to 2010. After this I filtered out all other countries except Brazil, India, Kenya, United Kingdom, and the United States. Each country had 1332 observations. I created separate dataframes for each country to make for easy comparison during modelling.
Before modelling I began with checking each country's time series for stationarity using ADF (Augmented Dickey-Fuller) test. 
I defined the hypothesis testing as follows: 
Null Hypothesis(H0): Series is non-stationary
Alternate Hypothesis(H1): Series is stationary
P-value > 0.05: Fail to reject the null hypothesis (H0)
P-value <= 0.05: Reject the null hypothesis (H0)
Brazil and Kenya had p-values greater than the common significance level of 0.05. Hence their time series did not give enough evidence to reject the null hypothesis. However, India, United Kingdom and United States had p-value less than 0.05 which is enough evidence to reject the null hypothesis. 
I proceeded to apply first order differencing on Brazil and Kenya time series in a bid to achieve stationarity.  Stationarity was achieved after applying first order differencing. 

# Time Series Modelling
The Autoregressive Integrated Moving Average (ARIMA) model is used to model the time series for each country. ACF (AutoCorrelation Function), and PACF (Partial AutoCorrelation Function) were used to determine p, d and q.
I tuned the models for each country by adjusting p, d and q parameters for optimal model performance. 

# Forecast Results
![image](https://github.com/user-attachments/assets/69ec6940-4335-4472-bf49-eb2bf6d98d21)
![image](https://github.com/user-attachments/assets/c928dd9d-e51e-4c7b-b255-6e3d55e36e1e)
![image](https://github.com/user-attachments/assets/c8a76404-f036-47b7-af1b-fc6d1dfe283c)
![image](https://github.com/user-attachments/assets/a21e5016-c9e5-4a11-830b-082054e2e1b0)
![image](https://github.com/user-attachments/assets/e3bc4b8a-898c-436f-8008-4069e71ceedb)
 
# Conclusion
High R2 in United States and India implies that the most of the variance in the temperature can be explained by the model.
With low to moderate errors, the models for Brazil, India, and Kenya show good to very good performance, capturing a major amount of the temperature range.
Although still functioning well, the US and UK models show larger errors, particularly in terms of MAE and RMSE, indicating a marginally less exact match than the other nations. 
To improve performance of the models for more accurate forecasting, I will apply transformations. Transformation stabilizes the variance and normalizes the distribution.
Accurate temperature forecasts are essential for maximising crop management techniques in the agriculture sector. Precise forecasts help farmers schedule when to sow and harvest, lessen the effects of severe weather, and increase output overall. 


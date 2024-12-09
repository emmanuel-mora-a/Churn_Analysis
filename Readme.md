# Final Project for Data science Graduation from Stackfuel Gmbh

Final Project for Data Analyst Graduation from Stackfuel Gmbh

Participants receive another larger dataset that they must analyze independently, with less guidance compared to the practice project. In an individual project discussion with the mentoring team from StackFuel, participants receive feedback on their approach to the solution.

# Why the notebook contains screenshot for the result

Regrettably, Stackfuel GmbH is unable to permit the release of our learning materials or completed projects due to copyright regulations and associated licensing rights. To showcase my project externally, I would need to recode everything outside the learning environment. However, without access to the dataset, the results can only be viewed within the learning environment. Consequently, the only method to display my work externally is through screenshots

# Scenario

You work for the telecommunications provider Teleconfia. It is currently trying to gain a foothold in the USA. Florida was selected as the first trial area. New customers were able to use cell phones on the Teleconfia network for one year at very favorable conditions. Not all customers stayed for a year. Many left. This customer churn is to be counteracted by two marketing campaigns.

The first marketing campaign targets urban areas where posters are to be put up. An urban area is a small town or a district of a large city. The four urban areas with the highest customer churn are to be selected in order to launch the marketing campaign in them. The second marketing campaign targets individual customers. Those customers who are likely to leave Teleconfia are to be called in order to agree special conditions with them.

The aim is to identify the urban areas or those customers for whom marketing campaigns should be launched. You have to find out which data series should be used for the decision. You should also find out whether there are certain factors from which customers should be contacted. Finally, a logistic regression should be used to determine the critical value at which a customer is more likely to churn than not to churn. 

Your decisions and recommendations should be substantiated and illustrated in the form of visualizations.



![](C:\Users\emman\AppData\Roaming\marktext\images\2024-11-30-23-19-25-image.png)



# Reading in data

- **Importing Necessary Libraries**:
  
  - **pandas** for data manipulation and analysis.
  
  - **numpy** for numerical computations.
  
  - **sqlalchemy** for database interactions.
  
  - **matplotlib.pyplot** and **seaborn** for data visualization.
  
  - **%matplotlib inline** to display plots inline within Jupyter notebooks.

- **Connecting to a Database**:
  
  - **Creating an Engine**: Establish a connection point to an SQLite database named `telco_churn.db`.
  
  - **Establishing a Connection**: Open a connection to the database to execute queries and retrieve data
  
  ### Importance of This Process
  
  1. **Data Handling**:
     
     - By importing libraries like `pandas` and `numpy`, we gain powerful tools for handling, manipulating, and analyzing large datasets efficiently.
     
     - `sqlalchemy` allows for seamless interaction with databases, enabling us to pull data into our environment for analysis.
  
  2. **Visualization**:
     
     - Libraries like `matplotlib` and `seaborn` are essential for creating visualizations that help us understand data trends, patterns, and outliers.
     
     - `%matplotlib inline` ensures that our visualizations are displayed directly within our Jupyter notebook, making it easier to interactively explore and understand our data.
  
  3. **Database Connection**:
     
     - Using SQLAlchemy to create an engine and connection helps us to integrate SQL queries within our Python code. This is crucial for data-driven applications where data retrieval and manipulation are performed through databases.
  
  4. **Integrated Analysis**:
     
     - This setup allows us to perform an end-to-end analysis, from data extraction, processing, and visualization, all within a single script. This integrated approach is crucial for efficient and effective data analysis workflows.
  
  5. **Reproducibility and Documentation**:
     
     - Documenting each step with comments and detailed docstrings ensures that the code is understandable and reproducible by others. This is important for collaboration and maintaining code quality.
  
  By following these steps, we set up a robust environment for data analysis and visualization, which is essential for making data-driven decisions and insights
  
  # Checking and cleaning data
  
  I got a databank with different table so i procide to explore each of this table looking for the possibilities of joining using a foreing key

### exploring churn table dataset

1. **Understanding the Dataset's Structure**:
   
   - `print(df_churn_data.shape)`: This line prints the shape of the DataFrame, indicating the number of rows and columns. Knowing the dimensions of the dataset helps you gauge its size and complexity.

2. **Identifying Data Types**:
   
   - `print(df_churn_data.dtypes)`: This line prints the data types of each column in the DataFrame. Understanding the data types is crucial for determining how to handle and process each column. For example, numeric columns can be used for statistical analysis, while categorical columns might need encoding.

3. **Detecting Missing Values**:
   
   - `nan_values_churn = df_churn_data.isna().sum()`: This line calculates the number of missing (NaN) values in each column.
   
   - `print(nan_values_churn)`: This line prints the count of missing values for each column. Identifying columns with missing values is a critical step in data cleaning and preprocessing, as missing values can impact the results of your analysis and models.

4. **Previewing the Data**:
   
   - `df_churn_data.head()`: This line displays the first few rows of the DataFrame. It provides a quick glance at the data's structure and content, which helps in understanding the initial state of the dataset.
   
   ### Overall Importance
- **Initial Data Exploration**: This code block is a fundamental part of EDA, giving you a snapshot of the dataset's structure, types, and cleanliness. It helps in identifying potential issues such as missing values or incorrect data types that need to be addressed before further analysis.

- **Data Cleaning**: By detecting missing values and understanding data types, you can plan necessary data cleaning steps, such as imputing missing values, converting data types, or removing invalid entries.

- **Informed Decision Making**: A clear understanding of the dataset's structure and content allows for informed decision-making on how to proceed with the analysis. It ensures that subsequent analyses are based on a solid understanding of the data.
  
  ### exploring cities table dataset

I used the same code that I used for exploring churn table

### checking the values from CHURN on local_area_code and from CITY on area_code to see if the match and then join

This block of code is used to check the unique values in the `local_area_code` column from the `df_churn_data` DataFrame and the `area_code` column from the `df_cities` DataFrame. The goal is to see if these values match, which would allow for joining the datasets based on these columns.

### joining tables

This block of code executes an SQL query that joins the `churn_data` and `cities` tables based on a common column and loads the result into a pandas DataFrame. 

### controlling the DF

This block of code is used to further explore the DataFrame (`df`) that results from joining the `churn_data` and `cities` tables. It provides insights into the DataFrame’s structure, data types, and the presence of any missing values.

### Convert int, Float, Str, Datatime into each other according to the situation

This block of code is used to explore the data types of the `df` DataFrame and convert specific columns to the appropriate data types.

#### Explanation:

1. **Exploring Current Data Types**:
   
   - `print(df.dtypes)`: This line prints the current data types of all columns in the DataFrame `df`. Understanding the initial data types is crucial for determining which columns need conversion.

2. **Defining Columns for Conversion**:
   
   - `cat_col = ['international_plan', 'voice_mail_plan', 'churn', 'phone_num', 'city', 'local_area_code']`: This list specifies the column names that should be converted to the `category` data type. These columns likely contain categorical data, which can benefit from being stored as the `category` type for efficiency and clarity.

3. **Converting Columns to 'category' Data Type**:
   
   - `for col in cat_col: df.loc[:, col] = df.loc[:, col].astype('category')`: This loop iterates over the list of columns defined in `cat_col` and converts each column to the `category` data type using the `astype('category')` method.

4. **Printing Data Types After Conversion**:
   
   - `print('-----------------------------')`: These lines print separators for better readability.
   
   - `print('---------NEW DTYPE-----------')`: This line indicates that the following output will show the new data types.
   
   - `print(df.dtypes)`: This line prints the data types of all columns after the conversion. It allows you to verify that the columns have been correctly converted to the `category` data type.

# Dealing with outliers

at the section  the code focuses on identifying numeric columns in a DataFrame, visualizing their distributions using boxplots, and addressing outliers

#### Controlling the outliers with boxplots

![](C:\Users\emman\AppData\Roaming\marktext\images\2024-11-30-23-21-17-image.png)



### New dataframe without outliers

This block of code is focused on creating a new DataFrame (`df_tight`) where outliers are identified and replaced with `NaN` values using boolean masks. The aim is to make the data as tight and clean as possible for further analysis

### Analazing Missing values to decide what to do with them

This block of code is used to count the number of rows in the DataFrame (`df_tight`) that contain NaN values and decide whether to drop, replace, or mark these missing values.

### Dropping all rows with nan

The numbert of rows from df where a nan is found, only represents the 2.94% of the df.  i decided to remove all of them.
This block of code is used to remove all rows in the DataFrame (`df_tight`) that contain any NaN values

#### New controll of histograms and boxplots after eliminating nan values and outliers



![](C:\Users\emman\AppData\Roaming\marktext\images\2024-11-30-23-22-17-image.png)



![](C:\Users\emman\AppData\Roaming\marktext\images\2024-11-30-23-22-32-image.png)



# Chech redundant columns

This block of code is used to check for redundant columns in the `df_cleaned` DataFrame by creating a correlation matrix and visualizing it using a heatmap. This process helps identify highly correlated columns, which may be redundant and can be removed to simplify the dataset



i checked the redundant columns with a heatmap

![](C:\Users\emman\AppData\Roaming\marktext\images\2024-11-30-23-23-03-image.png)

### drop redundant columns

here the code is used to remove specific columns from the DataFrame `df_cleaned` that were identified as redundant in the previous step

chek heatmap again:



![](C:\Users\emman\AppData\Roaming\marktext\images\2024-11-30-23-23-29-image.png)





# Names of the four urban areas with the highest customer churn

This block of code uses a pandas DataFrame to store and manipulate multidimensional data, focusing on analyzing and visualizing churn data by city. The code creates several plots to compare churn counts and percentages across different cities.

**ANSWER**
**The cities with the biggest Churn problem are:** 
**- 1 - Jacksonville** 
**- 2 - Orlando 1**
**- 3 - Cape coral**
**- 4 - Orlando 2**

![](C:\Users\emman\AppData\Roaming\marktext\images\2024-11-30-23-24-08-image.png)



![](C:\Users\emman\AppData\Roaming\marktext\images\2024-11-30-23-24-24-image.png)





# Which categorical variable is suitable as an indicator of customer churn? Identify all customers who should be contacted on this basis

This block of code is designed to find numeric columns in the `df_cleaned` DataFrame that have fewer than 20 unique values.

after running the code I could find that the feature ''customer_service_calls' was the only one with less than 20 unique values, so is easer to the their influence while plotting some bar charts



![](C:\Users\emman\AppData\Roaming\marktext\images\2024-11-30-23-25-03-image.png)







**ANSWER**  
**from four onwards the probability of leaving multiplies by 4**  
**from five onwards is more probable that the customer leaves than to stay**

# Which floating point variable could be used as an indicator of customer churn? Determine the threshold here using a logistic regression. Identify the customers who should be contacted on this basis

I plotted a heatmap to identify  which other numeric feature is highly correlated with churn. 

After plotting the Heatmap i could see that ' total_day_minutes' has also a interesting values of correlation of 0.2

# Logistic regression

This block of code performs a logistic regression analysis to understand the relationship between the `total_day_minutes` and `churn` in the `df_cleaned`

after running the regression model I got to the next conclusion:

**Pseudo R-squared:** The Pseudo R-squared value is 0.05163, which is relatively low.  
This indicates that the model explains only about 5.16% of the variance in the dependent variable (churn).  
While Pseudo R-squared values are generally lower than traditional R-squared values, this still  
suggests that there may be other important predictors not included in the model1.  

**Log-Likelihood:** The Log-Likelihood value of -1268.1, while better than the null model (-1337.2),\ still indicates that there is room for improvement in the model

**Conclution** there is a small tendency of leaving the company for thoso who has more minutes called during the day, but it is  
not so significant to take into account

# formulation of recommendations

---

Based on the provided data, here are some recommendations to help prevent customers from leaving the company:

**----------The first marketing campaign targets urban areas----------**

**Important locations:** **the cities with the higher migration rate are:**

1 - **Jacksonville** with **21%** of the total migration  
2 - **Orlando 1** with **15%** of the totalmigration  
3 - **Cape coral** with **14%** of the total migration  
4 - **Orlando 2** with **12%** of the total migration

**----------individual customers. Those customers who are likely to leave Teleconfia----------**

1 - Costumers that do have a international_plan, they will have a probilty of leaving of = 42.22%

2 - Costumers that do have a voice_mail_plan, they will have a probilty of leaving of = 8.555%**

3 - Costumers that had called costumer service more than 5 times, are more like to leave than to stay (probability of leaving > 50%)

**----------Recommendations----------**

**Review and Improve International Plans:** Since customers with international plans have a higher probability of leaving (42.22%), it might be beneficial to review these plans. Consider enhancing the value offered, such as better rates, more inclusive services, or additional benefits to make these plans more attractive and competitive.

**Promote Voice Mail Plans:** Customers without a voice mail plan have a higher probability of leaving (16.75%) compared to those with one (8.56%). Promoting the benefits of having a voice mail plan and possibly bundling it with other services at a discounted rate could encourage more customers to subscribe, thereby reducing their likelihood of leaving.

**Enhanced Customer Support**: After analyzing the customer service calls and the factors contributing to customer migration  
I recommend reaching out to clients who have contacted customer service more than four times and have not yet left.  
These clients have a high probability of migrating, with a likelihood of 44% or higher.  
Ensure that customer service is proactive and responsive.  
Providing excellent support can significantly improve customer satisfaction and loyalty.

**Base on the data there are 129 customer under this conditions.  
Attached to this report you will find a list of these clients.**

**Personalized Offers and Incentives:**  
while contacting these customers, consider Adressing the two first analazed point  
(International Plan, Promote Voice Mail Plans) to offer better conditions

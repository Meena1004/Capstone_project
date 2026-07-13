# Part1 - Data Acquistion, Cleaning and Exploratory Data Analysis
# Project Overview.
This is Part 1 of my Applied AI & ML essentials Capstone Project.
In this part1 loaded the raw dataset, checked the quality of data, cleaned the missing values, analysed the dataset using statisyics andvisualizations and created a clean dataset which is be used in part 2 & 3.
The oyput of this part is "cleaned_data.csv".

# Dataset Informations.
The name of the dataset is **Ames Housing Dataset**.
This dataset has **2930** number of rows.
This dataset has **82** number of columns.
And the target column is **SalePrice**.
This dataset contains the information about houses like area, quality, basement, garage, rooms, neighborhood and finally the sale prics.

# Why i selected this datset.
I have gone through the some dataset those are not meet my criteria like those are either empty or fully cleaned dataset so i selected Ames Housing dataset because it satisfies all assignment requirements.
Because it has,
  - More than 500 rows
  - More than 5 columns
  - Numeric and categorical features
  - Real-world housing data
  - Missing values
  - Outliers
  - Skewed columns
So this is suitable for performing complete data preprocessing and machine learning.

# Why i used the complete dataset instead of taking a sample.
I did not take only a sample from the dataset.
I used all 2930 records because the dataset size is already managable in Google Colab.
Using the complete dataset helps the model learn from more examples.
If i use only a small sample, some important information, missing values and outliers may not appear properly.
Using the complete dataset also gives better statistics and better visualization results.

# Loading Dataset.
The dataset was loaded using **pd.read_csv()**
After loading i checked 
  -First 5 rows
  -Datatypes
  -Dataset shape
This helped me understand the dataset before cleaning.

# Missing Value Analysis.
I calculated Total missing values, Missing percentage for every column.
Columns having more than 20% missing values were filled.
Numeric columns were filled using the median.

# Why i selected Median instead of Mode
I selected median because many numeric columns were positively skewed.
Mean is affected by very large values.
Median is more stable because it is not affected much by outliers.
Therefore median gives better imputation for skewed data.

# Duplicate check
I checked is any duplicate rows are present by using - **df.duplicated().sum()**
But here there is no duplicate rows were found in the dataset.
So no rows were removed.
Because duplicates were not removed, the missing value percentages also remained unchanged.

# Datatyoe Conversion
Some columns were converted into category dataset because they contain repeated values.
For example -MS SubClass
            -MS Zoning  
This reduced memory usage.
I also compared memory usage before and after conversion.

# Descriptive Statistics.
I calculated descriptive statistics for all numeric columns using - **describe()**
This helped understand - Mean
                       - Median
                       - Standard Deviation
                       - Minimun
                       - Maximum
                       - Quartiles

# Skewness Analysis
I calculated skewness for every numeric column.
The highest skewd columns were - Misc Val
                               - Pool Area
These columns are positively skewed
These means most values are very small while only few records have very large values.
Because of this the mean moves toward large values.
So median is a better choice for filling missing values.

# Outlier Detection.
I used the IQR method.
I calculated  - Q1
              - Q2
              - IQR
              - Lower Bound 
              - Upper Bound
I checked outliers for - SalePrice
                       - Lot Area 
I found many outliers.
I did not remove them because housing datasets naturally contain expensive houses and  very lage plots.
Removing them may remove important information.
Therefore I decided to keep the outliers and let the machine learning models handle them in part 2.

# Visualizations
I created all required plots.
1.Line plot:
  A line plot was created to observe how one numeric variable changes across records.
2.Bar plot:
  A bar plot compares average values between categories.
  This helps understand which category has higher average values.
3.Histogram:
  A histogram was created for the most skewed column.
  The distribution is heavily right skewed because most values are zero and only a few values are very large.
4.Scatter plot:
  I plotted Garage Area against Garage Cars.
  The scatter plot shows a strong positive relationship.
  Generally houses with large garage are have more garage spaces.
5.Box plot:
  I compared SalePrice across zoning categories.
  Different categories show different median prices and spread.
  some categories also contain many outliers.

# Correlation Heatmap
I generated Pearson correlation heatmap.
The strongest correlation was found between - Order
                                            - Yr Sold
This does not necessarily mean one variable causes another.
Both variables increase together because of the ordering of records in the dataset.
So this is correlation but not a casual relationship.
Another possible explanatiom is that houses were recorded in chronological order.

# Mean vs Median Comparison
For the two highest skewed columns i printed both - Mean 
                                                  - Median
Median was selected because both columns are positively skewed.
After filling missing values i confirmed that no missing values remainded.

# Spearman Correlation
I calculated both - Pearson correlation
                  - Spearman correlation
Then i compared both correlation matrics.
Some variable pairs had larger spearman correlation than pearson correlation.
This indicates a monotonic relationship instead of a perfectly linear relationship.
For feature selection in part2, i mainly used pearson correlation because my regression models linear relationships.
spearman was used only as additional analysis.

# Group Aggregation
I grouped one categorical column with one numeric column.
I calculated - Mean
             - Standard Deviation
             - Count
I identified - Group with highest Mean
             - Group with highest Standard Deviation
A higher standard deviation means values inside that category vary a lot.
So the categorical feature alone cannot perfectly predict the target.
I also calculated the ratio between highest and lowest group mean.
The ratio showed that the categorical feature contains useful predictive information.

# Output Files.
This folder contains
  - AmesHousing.csv
  - part1.ipynb
  - cleaned_data.csv
  - correlation.png
  - hist_plt.png
  - scatter_plt.png
  - box_plt.png
  - line_plt.png
  - bar_plt.png

# Challenges Faced
During this part i faced some problems.

  - Many columns has large missing values.
  - Some columns were highly skewed.
  - Choosing proper imputaton method needed analysis.
  - Some columns needed datatype conversion.
  - Understanding the correlation between many variables was difficult.
  - I had to carefully interpret outliers without removing useful housing information.
These problems were solved using pandas, matplotlib and seaborn.

# Conclusion
In this part i successfully cleaned the raw dataset and performed complete exploratory data analysis.
The final cleaned dataset was saved as **cleaned_data.csv**
This cleaned dataset will be used for building machine learning model in part 2.

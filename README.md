
This  file provides an overview of the data cleaning project, detailing the steps taken to clean the dataset and prepare it for further analysis.

Project Overview
The goal of this project is to clean a diabetes dataset, handling missing values, correcting inconsistencies, and removing outliers and duplicates. The cleaned dataset is then saved as a new CSV file.

Libraries Used
pandas: For data manipulation and analysis.
seaborn: For data visualization, particularly for identifying outliers.
Data Cleaning Steps
Import Necessary Libraries. 


python
Copy code
import pandas as pd
import seaborn as sns
Read the Data File. 

python
Copy code
df = pd.read_csv("diabetes_unclean.csv")
Initial Data Inspection. 

Display the first record of the data
python
Copy code
df.head()
Display the last 5 records
python
Copy code
df.tail()
Display the number of columns
python
Copy code
df.columns
Rename Columns. 

Rename the column 'No_Pation' to 'Pation_No'
python
Copy code
df.rename(columns = {"No_Pation":"Pation_No"}, inplace=True)
Handling Missing Values. 

Check for missing values
python
Copy code
df.isnull().sum()
Replace missing values in the 'HbA1c' column with the mean value
python
Copy code
mean_value = df["HbA1c"].mean()
df["HbA1c"] = df["HbA1c"].fillna(mean_value)
Drop remaining missing values in other columns
python
Copy code
df1 = df.dropna()
df1.isnull().sum()
Data Information and Aggregation. 

Get information about the dataset
python
Copy code
df1.info()
Aggregate data by 'CLASS'
python
Copy code
df1.groupby("CLASS")["CLASS"].agg("count")
Cleaning Categorical Data. 

Check unique values in the 'CLASS' column
python
Copy code
df["CLASS"].unique()
Replace inconsistent values in 'CLASS' column
python
Copy code
df1["CLASS"] = df1["CLASS"].str.replace("Y ", "Y")
df1["CLASS"] = df1["CLASS"].str.replace("N ", "N")
df1["CLASS"].unique()
Handling Outliers. 

Check for outliers in 'Cr' column using boxplot
python
Copy code
sns.boxplot(df1["Cr"])
Remove outliers beyond the 99.5th percentile
python
Copy code
max_cr = df1["Cr"].quantile(0.995)
df2 = df1[df1["Cr"] < max_cr]
sns.boxplot(df2["Cr"])
Check for outliers in 'HbA1c' column
python
Copy code
sns.boxplot(df1["HbA1c"])
Removing Duplicates. 

Check for duplicate values
python
Copy code
df2.duplicated()
Drop duplicate values
python
Copy code
df3 = df2.drop_duplicates()
df3.duplicated().sum()
Save Cleaned Data. 

Save the cleaned data to a new CSV file
python
Copy code
df3.to_csv("cleaned_diabetes.csv", index=False)

# EXNO2DS
# AIM:
To perform Exploratory Data Analysis on the given data set.
      
# EXPLANATION:
  The primary aim with exploratory analysis is to examine the data for distribution, outliers and anomalies to direct specific testing of your hypothesis.
  
# ALGORITHM:
STEP 1: Import the required packages to perform Data Cleansing,Removing Outliers and Exploratory Data Analysis.

STEP 2: Replace the null value using any one of the method from mode,median and mean based on the dataset available.

STEP 3: Use boxplot method to analyze the outliers of the given dataset.

STEP 4: Remove the outliers using Inter Quantile Range method.

STEP 5: Use Countplot method to analyze in a graphical method for categorical data.

STEP 6: Use displot method to represent the univariate distribution of data.

STEP 7: Use cross tabulation method to quantitatively analyze the relationship between multiple variables.

STEP 8: Use heatmap method of representation to show relationships between two variables, one plotted on each axis.

## CODING AND OUTPUT

    # ----------------------------------------
# Step 1: Import the Required Packages
# ----------------------------------------
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

# ----------------------------------------
# Step 2: Load the Dataset
# ----------------------------------------
# Replace 'your_data.csv' with your actual dataset filename
data = pd.read_csv('titanic_dataset.csv')
data.head()
print("Dataset loaded successfully.\n")

# ----------------------------------------
# Step 3: Data Cleansing - Replace Null Values
# ----------------------------------------
# Use mean for numeric columns and mode for categorical columns
for column in data.columns:
    if data[column].dtype == 'object':
        data[column] = data[column].fillna(data[column].mode()[0])
    else:
        data[column] = data[column].fillna(data[column].mean())

print("Missing values handled.\n")

# ----------------------------------------
# Step 4: Boxplot to Analyze Outliers (Fare)
# ----------------------------------------
plt.figure(figsize=(6,4))
sns.boxplot(x=data['Fare'])
plt.title("Boxplot - Fare")
plt.xlabel("Fare")
plt.show()

# ----------------------------------------
# Step 5: Remove Outliers Using IQR Method
# ----------------------------------------
def remove_outliers_iqr(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR
    return df[(df[column] >= lower) & (df[column] <= upper)]

# Apply IQR method on 'Salary'
data = remove_outliers_iqr(data, 'Fare')
print("Outliers removed using IQR method.\n")

# ----------------------------------------
# Step 6: Countplot for Categorical Data
# ----------------------------------------
plt.figure(figsize=(7,4))
sns.countplot(x='SibSp', data=data)
plt.title("Countplot - SibSp Distribution")
plt.xticks(rotation=45)
plt.show()

# ----------------------------------------
# Step 7: Displot for Univariate Distribution (Age)
# ----------------------------------------
sns.displot(data['Age'], kde=True, height=4, aspect=1.5)
plt.title("Displot - Age Distribution")
plt.xlabel("Age")
plt.ylabel("Sex")
plt.show()

# ----------------------------------------
# Step 8: Cross Tabulation
# ----------------------------------------
crosstab_result = pd.crosstab(data['Sex'], data['SibSp'])
print("\nCross Tabulation Result (Sex vs SibSp):\n")
print(crosstab_result)

# ----------------------------------------
# Step 9: Heatmap to Show Correlation
# ----------------------------------------
plt.figure(figsize=(8,6))
correlation_matrix = data.select_dtypes(include=np.number).corr()
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm')
plt.title("Correlation Heatmap")
plt.show()

<img width="731" height="588" alt="Screenshot 2026-03-09 104003" src="https://github.com/user-attachments/assets/e6bc5e0f-b110-43c6-9c39-f32723d14838" />

<img width="925" height="587" alt="Screenshot 2026-03-09 104013" src="https://github.com/user-attachments/assets/1320ec3f-4642-4d70-b146-3539eb86f458" />

<img width="883" height="612" alt="Screenshot 2026-03-09 104027" src="https://github.com/user-attachments/assets/a62d5acc-c153-4c98-8a09-49d96bc90457" />

<img width="1063" height="804" alt="Screenshot 2026-03-09 104046" src="https://github.com/user-attachments/assets/1b95e38b-4701-444c-a86c-4a82ddf23d20" />

# RESULT
Thus, the Exploratory Data Analysis on the given data set is successfully performed.

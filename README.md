# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
```
import pandas as pd
```
#READ CSV FILE HERE
```
data = pd.read_csv("/content/iris (1).csv")
data
```
![Screenshot 2025-03-21 102308](https://github.com/user-attachments/assets/fd1518c2-3bce-4909-844d-921db2cdc606)

#DISPLAY THE INFORMATION ABOUT CSV AND RUN THE BASIC DATA ANALYSIS FUNCTIONS
```
data.describe()
```
![Screenshot 2025-03-21 102350](https://github.com/user-attachments/assets/6e0a389f-cecb-4da4-9763-1a0233a12525)
```
data.info()
```
![Screenshot 2025-03-21 102446](https://github.com/user-attachments/assets/23b9554a-325c-4218-9bec-52b7cb952a3c)

#CHECK OUT NULL VALUES IN DATA SET USING FUNCTION
```
data.isnull()
```
![Screenshot 2025-03-21 102541](https://github.com/user-attachments/assets/5b7ede1d-7deb-4c86-bf37-c67b02785bba)

#DISPLAY THE SUM ON NULL VALUES IN EACH ROWS
```
data.isnull().sum()
```
![Screenshot 2025-03-21 102630](https://github.com/user-attachments/assets/d82052ce-d768-4ebd-a45c-278b9e61a947)

#DROP NULL VALUES
```
data.dropna()
```
![Screenshot 2025-03-21 102823](https://github.com/user-attachments/assets/cadf143f-01c5-4d0d-99a7-9a382a39f30c)

#FILL NULL VALUES WITH CONSTANT VALUE "O"
```
data_filled = data.fillna("O")
data_filled
```
![Screenshot 2025-03-21 102902](https://github.com/user-attachments/assets/20efacf9-8b50-471b-9218-d9bbd0b920e6)

#FILL NULL VALUES WITH ffill or bfill METHOD
```
fill= data.fillna(method='ffill')
fill
```
![Screenshot 2025-03-21 103203](https://github.com/user-attachments/assets/16bd3374-0987-4518-b0db-f20df0119ad3)

#CALCULATE MEAN VALUE OF A COLUMN AND FILL IT WITH NULL VALUES

```
mean1 = data['sepal_length'].mean()
data['sepal_length'].fillna(mean1, inplace=True)
data
```
![Screenshot 2025-03-21 103529](https://github.com/user-attachments/assets/9d6526cc-c319-4b5d-85df-0959d19bb7f5)

#DROP NULL VALUES
```
data.dropna()
```
![Screenshot 2025-03-21 103615](https://github.com/user-attachments/assets/09394430-62bb-43a0-bf86-ba023f4fbf3a)

```
import pandas as pd
import seaborn as sns
age = [1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af = pd.DataFrame(age, columns=['Age'])
af
```
![Screenshot 2025-03-21 103820](https://github.com/user-attachments/assets/3636bffd-925e-4318-b700-33e28e9c9a2d)

#USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
```
plt.figure(figsize=(8, 5))
sns_bp.boxplot(x=af['age'])
plt.title("Boxplot to Detect Outliers")
plt.show()
```

![Screenshot 2025-03-21 103923](https://github.com/user-attachments/assets/6babac76-b580-411c-975f-170a9c2dce75)

#PERFORM IQR METHOD AND DETECT OUTLIER VALUES
```
q1=af.quantile(0.25)
q2=af.quantile(0.5)
q3=af.quantile(0.75)
iqr=q3-q1
iqr

Q1=np.percentile(af,25)
Q3=np.percentile(af,75)
IQR=Q3-Q1
IQR
```
![Screenshot 2025-03-21 104202](https://github.com/user-attachments/assets/531431bd-4699-41dd-bdb5-585a5985b829)

#REMOVE OUTLIERS
```
lower_bound=Q1-1.5*IQR
upper_bound=Q3+1.5*IQR
lower_bound

lower_bound=Q1-1.5*IQR
upper_bound=Q3+1.5*IQR
lower_bound
upper_bound

outliers=[x for x in age if x<lower_bound or x>upper_bound]
print("Q1:",Q1)
print("Q3:",Q3)
print("IQR;",IQR)
print("Lower bound:",lower_bound)
print("Upper bound:",upper_bound)
print("Outliers:",outliers)
```

![Screenshot 2025-03-21 104309](https://github.com/user-attachments/assets/d0a649f8-5dd0-46ee-9ff4-63419befa375)

#USE BOXPLOT FUNCTION HERE TO CHECK OUTLIER IS REMOVED
```
af=af[((af>=lower_bound)&(af<=upper_bound))]
af
af.dropna()
sns.boxplot(data=af)
sns.scatterplot(data=af)
```
![Screenshot 2025-03-21 104353](https://github.com/user-attachments/assets/35595ceb-1754-4bab-a821-59314c4bcbf5)

#STATS METHOD IS USED TO IMPLEMENT Z SCORE METHOD
```
from scipy import stats
from matplotlib import pyplot as plt
from scipy.stats import zscore
import seaborn as sns
from seaborn import boxplot as sns_bp
data=[1,12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,72,75,78,81,84,87,90,93,96,99,158]
df=pd.DataFrame(data,columns=['Values'])
```

#USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER
```
plt.figure(figsize=(8, 5))
sns.boxplot(x=df['Values'])
plt.title("Boxplot to Detect Outliers")
plt.show()
```
![Screenshot 2025-03-21 105314](https://github.com/user-attachments/assets/f8248ebb-0473-4a03-a177-6f296c98556a)

#PERFORM Z SCORE METHOD AND DETECT OUTLIER VALUES
```
z_scores = zscore(df['Values'])
df['Z-Score'] = z_scores
outliers_zscore = df[df['Z-Score'].abs() > 3]
print("Outliers detected by Z-Score method:")
print(outliers_zscore)
```
![Screenshot 2025-03-21 105346](https://github.com/user-attachments/assets/0b6cf119-4c09-480b-8116-995b9745ade5)

#REMOVE OUTLIERS
```
df_no_outliers_zscore = df[df['Z-Score'].abs() <= 3]
print("\nDataFrame after removing outliers (Z-Score method):")
print(df_no_outliers_zscore)

plt.figure(figsize=(8, 5))
sns.boxplot(x=df_no_outliers_zscore['Values'])
plt.title("Boxplot After Removing Outliers (Z-Score method)")
plt.show()
```
![Screenshot 2025-03-21 105447](https://github.com/user-attachments/assets/3a5dba8b-e622-4949-88ae-82dc0f0efae6)

#USE BOXPLOT FUNCTION HERE TO CHECK OUTLIER IS REMOVED
```
plt.figure(figsize=(8, 5))
sns_bp(x=df_no_outliers_zscore['Values'])
plt.title("Boxplot After Removing Outliers (Boxplot method - IQR)")
plt.show()
```
![Screenshot 2025-03-21 105522](https://github.com/user-attachments/assets/175b41de-eefe-4887-b809-e3272beb0c4f)

# Result
Thus, the Data Cleaning Process is executed Successfully.

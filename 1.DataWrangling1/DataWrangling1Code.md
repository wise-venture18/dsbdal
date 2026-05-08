Q. Data Wrangling, I 
Perform the following operations using Python on any open source dataset (e.g., data.csv) 
1. Import all the required Python Libraries. 
2. Locate an open source data from the web (e.g., https://www.kaggle.com). Provide a clear  
            description of the data and its source (i.e., URL of the web site). 
3. Load the Dataset into pandas dataframe. 
4. Data Preprocessing: check for missing values in the data using pandas isnull(), describe() 
function to get some initial statistics. Provide variable descriptions. Types of variables etc. 
Check the dimensions of the data frame. 
5. Data Formatting and Data Normalization: Summarize the types of variables by checking 
the data types (i.e., character, numeric, integer, factor, and logical) of the variables in the 
data set. If variables are not in the correct data type, apply proper type conversions. 
6. Turn categorical variables into quantitative variables in Python. 
 
In addition to the codes and outputs, explain every operation that you do in the above steps and 
explain everything that you do to import/read/scrape the data set.

* Dataset Download Link (Titatnic) : https://www.kaggle.com/datasets/yasserh/titanic-dataset?resource=download
---

# 📘 PS1: Data Wrangling I

---

## 🔹 Cell 1: Import Libraries

```python
import pandas as pd
import numpy as np
```

---

## 🔹 Cell 2: Load Dataset

```python
df = pd.read_csv("titanic.csv")

df.head()
```

---

## 🔹 Cell 3: Basic Info & Dimensions

```python
print("Shape:", df.shape)

df.info()
```

---

## 🔹 Cell 4: Missing Values Check

```python
print(df.isnull().sum())
```

---

## 🔹 Cell 5: Statistical Summary

```python
df.describe(include='all')
```

**Upgrade:** Includes categorical columns too.

---

## 🔹 Cell 6: Data Types

```python
print(df.dtypes)
```

---

## 🔹 Cell 7: Handle Missing Values

```python
df['Age'] = df['Age'].fillna(df['Age'].mean())

df['Embarked'] = df['Embarked'].fillna(df['Embarked'].mode()[0])

df['Cabin'] = df['Cabin'].fillna('Unknown')
```


---

## 🔹 Cell 8: Verify Missing Values Removed

```python
print(df.isnull().sum())
```


---

## 🔹 Cell 9: Data Type Conversion

```python
df['Age'] = df['Age'].astype(float)

df['Survived'] = df['Survived'].astype(int)
```

---

## 🔹 Cell 10: Data Normalization

```python
df['Age_norm'] = (
    (df['Age'] - df['Age'].min()) /
    (df['Age'].max() - df['Age'].min())
)

df[['Age', 'Age_norm']].head()
```

---

## 🔹 Cell 11: Convert Categorical → Numerical

```python
# Label Encoding
df['Sex'] = df['Sex'].map({
    'male': 0,
    'female': 1
})

# One Hot Encoding
df = pd.get_dummies(df, columns=['Embarked'])
```

---

## 🔹 Cell 12: Final Output

```python
print("Final Shape:", df.shape)

df.head()
```

---

# ✅ **Important Rules (Don’t Miss)**

* Run cells **in order**
* Do NOT run encoding twice
* Always handle missing values before normalization

---Here are **viva questions + crisp answers** based exactly on your Data Wrangling Problem Statement. These are the ones examiners usually ask.

---

# 📘 **Viva Questions & Answers (Data Wrangling)**

---

## 🔹 **Basic Questions**
* What is Data Science?
:data Science is the field of extracting useful information and insights from data using:

* What is Pandas?
:pandas is a Python library used for data manipulation and analysis.

* What is NumPy?
:NumPy is a Python library used for numerical and mathematical operations.

### 1. What is Data Wrangling?

**Answer:**
Data wrangling is the process of cleaning, transforming, and preparing raw data into a structured format suitable for analysis.

---

### 2. What is a DataFrame?

**Answer:**
A DataFrame is a 2D tabular data structure in pandas with rows and columns, similar to a table in a database or Excel sheet.

---

### 3. What is pandas?

**Answer:**
pandas is a Python library used for data manipulation and analysis, especially for handling structured data.

---

### 4. What is NumPy?

**Answer:**
NumPy is a library used for numerical computations, especially arrays and mathematical operations.

---

## 🔹 **Dataset Related**

### 5. Which dataset did you use?

**Answer:**
Titanic dataset from Kaggle.

---

### 6. What does the dataset contain?

**Answer:**
It contains passenger details such as age, gender, ticket class, fare, and survival status.

---

### 7. What is the target variable?

**Answer:**
Survived column, which indicates whether a passenger survived (1) or not (0).

---

## 🔹 **Preprocessing Questions**

### 8. How did you check missing values?

**Answer:**
Using:

```python
df.isnull().sum()
```

---

### 9. How did you handle missing values?

**Answer:**

* Age → filled with mean
* Embarked → filled with mode
* Cabin → filled with "Unknown"

---

### 10. Why do we handle missing values?

**Answer:**
Because missing data can affect analysis accuracy and machine learning models.

---

### 11. What does `describe()` do?

**Answer:**
It provides statistical summary such as mean, standard deviation, min, max, and percentiles.

---

### 12. What does `info()` show?

**Answer:**
It shows number of rows, column names, data types, and non-null values.

---

## 🔹 **Data Types & Formatting**

### 13. What are different data types in pandas?

**Answer:**

* int
* float
* object (string)
* bool

---

### 14. Why is data type conversion important?

**Answer:**
To ensure correct analysis and avoid errors in computations.

---

## 🔹 **Normalization**

### 15. What is normalization?

**Answer:**
It is the process of scaling values to a range, usually 0 to 1.

---

### 16. Why did you normalize Age?

**Answer:**
To bring values to the same scale, which improves model performance.

---

## 🔹 **Categorical Conversion**

### 17. What is categorical data?

**Answer:**
Data that represents categories, like gender or city.

---

### 18. Why convert categorical to numerical?

**Answer:**
Because machine learning models require numerical input.

---

### 19. What is Label Encoding?

**Answer:**
Converting categories into numbers, e.g., male = 0, female = 1.

---

### 20. What is One-Hot Encoding?

**Answer:**
Creating separate binary columns for each category.

---

### 21. What happened to the Embarked column after encoding?

**Answer:**
It was replaced by:

* Embarked_C
* Embarked_Q
* Embarked_S

---

## 🔹 **Error-Based Questions (Very Important 🔥)**

### 22. Why did you get KeyError for Embarked?

**Answer:**
Because the column was already converted into dummy variables and no longer exists.

---

### 23. What is chained assignment warning?

**Answer:**
It occurs when modifying a copy of data instead of the original DataFrame.

---

### 24. How did you fix it?

**Answer:**
By using:

```python
df['col'] = df['col'].fillna(...)
```

---

## 🔹 **Advanced Questions**

### 25. Difference between normalization and standardization?

**Answer:**

* Normalization → scales between 0 and 1
* Standardization → mean = 0, std = 1

---

### 26. What is feature scaling?

**Answer:**
Adjusting values of features to a similar range.

---

### 27. What is data cleaning?

**Answer:**
Removing errors, handling missing values, and correcting inconsistencies.

---

### 28. Why is data wrangling important?

**Answer:**
Because raw data is often messy and unsuitable for analysis.
ort)**
* 📄 **Printable one-page revision sheet**

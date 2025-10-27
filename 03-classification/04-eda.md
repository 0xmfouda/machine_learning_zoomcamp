# 3.4 EDA - Exploratory Data Analysis

- We will use the `df_full_train` dataset for our exploratory data analysis.

### Checking Missing Values

- First, let's check if there are any missing values in our training data.

```python
df_full_train.isnull().sum()
```

- Result: No missing values were found.
- The missing values originally in the `totalcharges` column were already handled during the data preparation step.
- No additional cleaning is needed.

### Exploring Target Variable: `churn`

- Next, we'll examine the distribution of our target variable, churn.

```python
# count
df_full_train.churn.value_counts()
```

- `0`: Represents non-churning users, who are the majority.
- `1`: Represents churning users. There are about 3 times fewer churning users than non-churning ones.

- To see this as a percentage, we can use `normalize=True`.

```python
df_full_train.churn.value_counts(normalize=True)
```

- This shows that approximately 26-27% of users in this dataset churned.
- This percentage is known as the churn rate.

**A Quicker Way to Calculate Churn Rate**

- Because the churn variable is binary (1 for churn, 0 for no churn), we can calculate the churn rate simply by taking its mean():

```python
df_full_train.churn.mean()
```

- This works because the mean is the sum of all values divided by the total count. Since all non-churners are 0, the sum is simply the total count of churners (1s).

  $Mean = \frac{\sum x_i}{n} = \frac{\text{Sum Of ones (churners)}}{\text{Total Customers}} = \text{Churn Rate}$

- We can store this as the global churn rate.

```python
global_churn_rate = df_full_train.churn.mean()

round(global_churn_rate, 2)
```

### Analyzing Other Variables

- let's look at **categorical** and **numerical** variables.

**Identifying Data Types**

```python
# Check data types
df_full_train.dtypes
```

- Note: seniorcitizen is listed as int64, but it actually represents a categorical variable (0 for "no," 1 for "yes").

**Separating Features**

- Let's create lists for our numerical and categorical variables.

```python
## Selecting Numberical Variables
numerical = ['tenure', 'monthlycharges', 'totalcharges']

## Selecting Categorical Variables
df_full_train.columns

# Removing 'customerid', 'tenure', 'monthlycharges', 'totalcharges', and 'churn'
categorical = ['gender', 'seniorcitizen', 'partner', 'dependents', 'phoneservice', 'multiplelines', 'internetservice',
       'onlinesecurity', 'onlinebackup', 'deviceprotection', 'techsupport',
       'streamingtv', 'streamingmovies', 'contract', 'paperlessbilling',
       'paymentmethod']
```

**Counting Unique Values for Categorical Variables**

- Let's check how many unique values each categorical variable has:

```python
df_full_train[categorical].nunique()
```

- Most variables are binary (2 values).
- Some variables have 3 values, and `paymentmethod` has 4.

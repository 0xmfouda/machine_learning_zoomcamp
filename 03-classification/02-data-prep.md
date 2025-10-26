<h1 align="center">3.2 Data preparation</h1>

- Download the `csv` and read it with pandas

  ```py
  import pandas as pd
  import numpy as np

  import matplotlib.pyplot as plt

  data = 'https://raw.githubusercontent.com/alexeygrigorev/mlbookcamp-code/master/chapter-03-churn-prediction/WA_Fn-UseC_-Telco-Customer-Churn.csv'

  !wget $data -O data-week-3.csv
  ```

  ```py
  df = pd.read_csv('data-week-3.csv')
  df.head()
  ```

- There are quite a lot of columns; to take a look at all of them at once, we can transpose the dataframe (rows become cols)

  ```py
  df.head().T
  ```

- To normalize column names, we can lowercase them and replace spaces with underscores.

  ```py
  df.columns = df.columns.str.lower().str.replace(' ', '_')

  categorical_columns = list(df.dtypes[df.dtypes == 'object'].index)

  for c in categorical_columns:
      df[c] = df[c].str.lower().str.replace(' ', '_')
  ```

- Inspect the data types:

  ```py
  df.dtypes
  ```

  - `seniorcitizen` is a number (int64)
  - `totalcharges` is an object (string), though it should be numeric.
    - Why?
      - Maybe some of the values are not numbers.
      - `pd.to_numeric(df.totalcharges)` -> error (unable to parse string "\_")

- Convert `totalcharges` to numbers and replace anything pandas can't parse with `NaN`.

  ```py
  tc = pd.to_numeric(df.totalcharges, errors='coerce')

  # Inspecting missing values
  tc.isnull().sum()         # 11

  # get customers rows with missing totalcharges.
  df[tc.isnull()][['customerid', 'totalcharges']]
  ```

- Fill columns with missing numeric charges with `0`

  - _Note_ that this is sometimes okay but may not be ideal because the data might be just unknown and they actually spent some money.

  ```py
  # convert total_charges to numeric, forcing errors to NaN
  df.totalcharges = pd.to_numeric(df.totalcharges, errors='coerce')
  df.totalcharges = df.totalcharges.fillna(0)
  ```

- Convert `churn` from `"Yes"/"No"` to `1/0` (binary target) because we are interested in numbers.

  ```py
  df.churn.head()
  df.churn = (df.churn == 'yes').astype(int)
  ```

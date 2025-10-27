<h1 align="center">3.3 - Setting Up The Validation Framework</h1>

- Standard data split: train, validation, test (60/20/20 distrbution).
  - Previously done with _NumPy_ and _Pandas_.
- Now we want to implement this using _Scikit-learn_.

  - `scikit-learn`: Python library with common ML algorithms + helpful utilities.

  ```python
  from sklearn.model_selection import train_test_split

  # Look at the docs
  train_test_split?
  ```

  - `test_size`: defines how large the test set is (e.g. `0.2` for 20%).
  - `random_state`: fixes the random seed -> results are reproducible.

**Splitting Data**

- `train_test_split` splits into 2 parts only: training and testing.

  ```py
  df_full_train, df_test = train_test_split(df, test_size=0.2, random_state=1)

  len(df_full_train), len(df_test)
  ```

**Getting Three Datasets (Train, Validation, Test)**

- Need another split on `full_train`:

  ```py
  df_train, df_val = train_test_split(df_full_train, test_size=0.25, random_state=1)

  len(df_train), len(df_val)
  ```

  - `test_size` for validation = 20% of **original data**,
    → 20% of 80% = **25% of full_train**.
  - So use `test_size = 0.25` when splitting `full_train`.

- Reset indices so they’re sequential:

  ```python
  df_train = df_train.reset_index(drop=True)
  df_val = df_val.reset_index(drop=True)
  df_test = df_test.reset_index(drop=True)
  ```

- Shuffling doesn’t affect models, but cleaner to view sequential indices.

**Getting `y` Variables**

- Extract target variable (`churn`) into separate arrays:

  ```python
  y_train = df_train.churn.values
  y_val = df_val.churn.values
  y_test = df_test.churn.values
  ```

- Then delete the `churn` column from dataframes:

  ```python
  del df_train['churn']
  del df_val['churn']
  del df_test['churn']
  ```

- Don’t delete from `df_full_train` yet
  - needed for next lesson.

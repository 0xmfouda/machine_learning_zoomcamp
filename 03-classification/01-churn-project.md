<h1 align="center">3.1 Churn prediction project</h1>

### Problem Setup

- Imagine that we work at a telecom company.
- Some clients might not be happy or see a better alternative and might stop the contract with us and leave for another company (Telco 2) or stop using services altogether.
- What we want to do is identify which customers are about to churn and assign everyone a score between zero and one that indicates how likely this customer is to leave.

### Identifying Customer Churn Likelihood with Personalized Offers

- Example scores: 20%, 30%, 35%, 45%, and high-risk like 85%.
- If a customer is likely to churn, we want to send promotional messages (e.g., 25% off) to keep them.
- We must be accurate: don’t offer discounts to people who would stay (we’d lose money) and don’t miss people who will churn.

### Framing as Supervised Learning (Binary Classification)

- This is a binary classification problem.
- Formula for a single observation:

$$\large g\left(x_{i}\right) = y_{i}$$

- $x_i$ is a feature vector describing customer $i$.
- $y$ is whether the customer left (churn).
- $y$ takes two values: 1 = positive example (customer did leave/churn), 0 = negative example (no churn).

### Model Output & Approach

- The model $g(x_i)$ outputs a score between 0 and 1 (the likelihood that customer $i$ will churn).
- We take historical customers (e.g., from last month). For each customer, we know if they left (label = 1) or stayed (label = 0). That becomes $y$, and customer info becomes $X$.
- Features: demographic info, location, monthly charges, contract type, tenure (months with company), services used, etc.
- Main idea: Train model on historical data, apply model to current customers, score each, and target high-score customers with promotions.

### Dataset

- We will use the dataset from Kaggle: [Telco Customer Churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn).

### Project Plan & Analysis Steps

1. Download the data and perform preparation.
2. Setting up the validation framework:
   - This time, we will use `scikit-learn`.
3. EDA (exploratory data analysis):
4. Feature importance metrics:
   - Churn rate, risk ratio, mutual information, and correlation.
5. One-hot encoding.
6. Logistic regression:
   - Compare logistic regression with linear regression.
7. Training logistic regression with `scikit-learn`.
8. Model interpretation:
   - Inspect coefficients of logistic regression to interpret what they mean.
9. Using the model:
   - Use the model to score customers and target promotions.

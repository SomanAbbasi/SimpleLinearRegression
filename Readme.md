# Simple Linear Regression

## 1. What is Linear Regression?

### Definition

**Linear Regression** is a supervised machine learning algorithm used to predict a **continuous numerical value** by learning a relationship between input features and an output.

Example:

```text
CGPA ─────────→ Placement Package
        Linear Regression
```

If we know a student's CGPA, we can predict their expected salary/package.

---

# 2. Types of Linear Regression

| Type                       | Input               | Output              |
| -------------------------- | ------------------- | ------------------- |
| Simple Linear Regression   | 1 input             | 1 continuous output |
| Multiple Linear Regression | Multiple inputs     | 1 continuous output |
| Polynomial Regression      | Polynomial features | 1 continuous output |

For now, we focus on **Simple Linear Regression**.

---

# 3. Simple Linear Regression

### Definition

**Simple Linear Regression** predicts a continuous output using **one input feature** by fitting the best possible straight line through the data.

### Example

Suppose we have:

```text
CGPA → Package

6.0 → 3.0 LPA
6.5 → 3.5 LPA
7.0 → 4.2 LPA
7.5 → 5.0 LPA
8.0 → 6.0 LPA
```

Here:

* **X = CGPA** → input/independent variable
* **Y = Package** → output/dependent variable

The goal is to find a line that represents the overall relationship between CGPA and package.

---

# 4. The Linear Regression Equation

The equation of a straight line is:

```text
y = mx + b
```

Where:

* **x** = input feature
* **y** = predicted output
* **m** = slope
* **b** = intercept

In Machine Learning, it can also be written as:

```text
ŷ = mx + b
```

Here, **ŷ (y-hat)** means **predicted value**.

Another copy-friendly version is:

```text
y_hat = mx + b
```

---

# 5. Best Fit Line

Real-world data usually does not lie perfectly on a straight line.

Instead, we may have:

```text
Package
  ↑
  |                 ●
  |             ●
  |          ●      ●
  |       ●
  |    ●
  | ●
  +------------------------→ CGPA
             /
            /
       Best Fit Line
```

The **Best Fit Line** is the line that represents the overall relationship between X and Y while keeping the prediction errors as small as possible.

### Important

The line does **not** necessarily pass through every data point.

Why?

Because real-world data contains variation and randomness.

---

# 6. Prediction Error

For each data point:

```text
Error = Actual - Predicted
```

Mathematically:

```text
e_i = y_i - ŷ_i
```

Since:

```text
ŷ_i = mx_i + b
```

we get:

```text
e_i = y_i - (mx_i + b)
```

Where:

* **e_i** = error/residual for data point i
* **y_i** = actual value
* **ŷ_i** = predicted value
* **x_i** = input value

### Example

```text
Actual package     = 5 LPA
Predicted package  = 4.5 LPA

Error = 5 - 4.5
      = 0.5 LPA
```

---

# 7. How Do We Find the Best Line?

We need to find the values of:

```text
m = slope
b = intercept
```

that produce the best predictions.

A common approach is **Least Squares**.

We calculate the squared errors:

```text
SSE = Σ (y_i - (mx_i + b))²
```

The objective is:

```text
Choose m and b
such that:

SSE = Σ (y_i - (mx_i + b))²

is minimum.
```

This means:

> Choose **m** and **b** such that the sum of squared errors is as small as possible.

This function is commonly called:

* **Sum of Squared Errors (SSE)**
* **Residual Sum of Squares (RSS)**

So:

```text
SSE = RSS
```

---

# 8. Why Square the Errors?

Suppose:

```text
Error 1 = +2
Error 2 = -2
```

If we simply add them:

```text
2 + (-2) = 0
```

The errors cancel each other.

Instead, we square them:

```text
2² + (-2)²
= 4 + 4
= 8
```

Therefore, squaring:

* prevents positive and negative errors from cancelling
* gives larger errors more penalty
* allows us to optimize the error mathematically

### Important intuition

An error of:

```text
1 → squared error = 1
2 → squared error = 4
3 → squared error = 9
10 → squared error = 100
```

So large errors receive a much larger penalty.

---

# 9. Mathematical Formula for Slope

After minimizing the squared error, the optimal slope is:

```text
m = Σ[(x_i - x̄)(y_i - ȳ)]
    -------------------------
       Σ[(x_i - x̄)²]
```

A single-line version:

```text
m = Σ[(x_i - x̄)(y_i - ȳ)] / Σ[(x_i - x̄)²]
```

Where:

* **x_i** = individual input value
* **y_i** = individual output value
* **x̄** = mean/average of X
* **ȳ** = mean/average of Y
* **Σ** = sum over all data points

### Mean formulas

The mean of X is:

```text
x̄ = Σx_i / n
```

The mean of Y is:

```text
ȳ = Σy_i / n
```

Where:

```text
n = number of data points
```

---

# 10. Mathematical Formula for Intercept

Once we know the slope:

```text
b = ȳ - mx̄
```

Therefore, the final regression equation becomes:

```text
ŷ = mx + b
```

The complete process is:

```text
Calculate x̄ and ȳ
        ↓
Calculate slope m
        ↓
Calculate intercept b
        ↓
Build equation
        ↓
ŷ = mx + b
```

---

# 11. Intuition Behind Slope and Intercept

## Slope m

The **slope tells us how much the predicted output changes when the input increases by one unit.**

Example:

```text
y = 2x + 1
```

Here:

```text
m = 2
```

So, if X increases by 1:

```text
X increases by 1
        ↓
Y increases by approximately 2
```

### Simple interpretation

> **Slope = change in Y for a one-unit change in X.**

For example:

```text
m = 2

X increases from 5 → 6
Y increases by approximately 2
```

---

## Intercept b

The **intercept is the predicted value of Y when X = 0.**

Example:

```text
y = 2x + 1
```

When:

```text
x = 0
```

then:

```text
y = 2(0) + 1
y = 1
```

So:

```text
Intercept = 1
```

### Simple interpretation

> **Intercept = predicted Y value when the input X is zero.**

---

# 12. Complete Example

Suppose our model learns:

```text
Package = 2(CGPA) + 1
```

For a student with:

```text
CGPA = 7
```

Prediction:

```text
Package = 2(7) + 1
        = 14 + 1
        = 15
```

So the predicted package is:

```text
15 LPA
```

The important point is that the model learned a **general relationship** rather than memorizing individual students.

---

# 13. Training and Prediction

The basic workflow is:

```text
             Training Data
                  │
                  ▼
        Find relationship between X and Y
                  │
                  ▼
           Calculate m and b
                  │
                  ▼
        Learn: ŷ = mx + b
                  │
                  ▼
             New Input X
                  │
                  ▼
          Calculate prediction
                  │
                  ▼
                 ŷ
```

In simple words:

```text
Training Data
      ↓
Learn the Best Line
      ↓
Find m and b
      ↓
ŷ = mx + b
      ↓
Give New X
      ↓
Get Predicted Y
```

---

# 14. Simple Linear Regression in Python

Using Scikit-Learn:

```python
from sklearn.linear_model import LinearRegression

model = LinearRegression()

# Training
model.fit(X_train, y_train)

# Prediction
y_pred = model.predict(X_test)
```

After training:

```python
model.coef_       # slope (m)
model.intercept_  # intercept (b)
```

The learned equation is:

```text
y_hat = model.coef_ * x + model.intercept_
```

For example, if:

```python
model.coef_ = 2
model.intercept_ = 1
```

Then:

```text
y_hat = 2x + 1
```

---

# 15. Simple Linear Regression from Scratch

The main idea can be implemented without Scikit-Learn:

```python
class SimpleLinearRegression:

    def fit(self, X, y):
        x_mean = X.mean()
        y_mean = y.mean()

        numerator = ((X - x_mean) * (y - y_mean)).sum()
        denominator = ((X - x_mean) ** 2).sum()

        self.m = numerator / denominator
        self.b = y_mean - self.m * x_mean

    def predict(self, X):
        return self.m * X + self.b
```

The important part is understanding what `fit()` is doing:

```text
Training
   ↓
Calculate mean of X and Y
   ↓
Calculate slope (m)
   ↓
Calculate intercept (b)
   ↓
Store m and b
```

Then `predict()` simply applies:

```text
y_hat = mx + b
```

---

# 16. Important Terms

| Term                 | Meaning                                |
| -------------------- | -------------------------------------- |
| Independent Variable | Input feature X                        |
| Dependent Variable   | Output Y                               |
| Slope                | Change in Y for one-unit change in X   |
| Intercept            | Predicted Y when X = 0                 |
| Prediction           | Model's estimated output               |
| Residual/Error       | Actual - Predicted                     |
| Best Fit Line        | Line that minimizes squared errors     |
| Least Squares        | Method used to minimize squared errors |
| SSE/RSS              | Sum of squared prediction errors       |

---

# 17. Key Idea

Simple Linear Regression is basically:

```text
Given:

X → Input
Y → Output

Learn:

y_hat = mx + b

where:

m = slope
b = intercept

Goal:

Find m and b
that minimize prediction error.
```

### One-Line Definition

> **Simple Linear Regression learns the best straight-line relationship between one input variable and one continuous output variable.**

### Easy Memory

```text
Data
 ↓
Find Best Line
 ↓
y_hat = mx + b
 ↓
Use Line for Prediction
```

---

# 18. Most Important Formulas to Remember

If you are preparing for an exam/interview, these are the formulas you should remember:

### 1. Linear Regression Equation

```text
y_hat = mx + b
```

### 2. Error / Residual

```text
e_i = y_i - y_hat_i
```

### 3. Squared Error

```text
e_i² = (y_i - y_hat_i)²
```

### 4. Sum of Squared Errors

```text
SSE = Σ(y_i - y_hat_i)²
```

or:

```text
SSE = Σ(y_i - (mx_i + b))²
```

### 5. Slope

```text
m = Σ[(x_i - x̄)(y_i - ȳ)] / Σ[(x_i - x̄)²]
```

### 6. Intercept

```text
b = ȳ - mx̄
```

### 7. Mean of X

```text
x̄ = Σx_i / n
```

### 8. Mean of Y

```text
ȳ = Σy_i / n
```

---

# 19. Final Mental Model

Think of Linear Regression like this:

```text
                DATA
                  ↓
        ┌─────────────────┐
        │ Find Best Line   │
        └─────────────────┘
                  ↓
             y_hat = mx + b
                  ↓
       ┌──────────┴──────────┐
       ↓                     ↓
    m = slope            b = intercept
       ↓                     ↓
 Change in Y            Y when X = 0
 for +1 X
       └──────────┬──────────┘
                  ↓
             PREDICTION
```

The entire idea can be remembered as:

```text
INPUT X
   ↓
Learn m and b
   ↓
Best-fit line
   ↓
y_hat = mx + b
   ↓
PREDICT Y
```

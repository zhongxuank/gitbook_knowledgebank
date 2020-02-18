---
description: >-
  Describing Linear Regression, as well as general concepts for Machine
  Learning.
---

# Linear Regression

{% embed url="https://towardsdatascience.com/introduction-to-machine-learning-algorithms-linear-regression-14c4e325882a" caption="Source for this page\'s content" %}

## What is Linear Regression?

A linear regression model is a simple model that takes as input some independent variables, `x`, and outputs the dependent variable, `y`. This is largely based on the assumed _linear relationship_ between the independent variables and the dependent variable. 

The goal is to plot a "line of best fit", which will be a line that best models the data points. The line can thus be modeled with the equation

```text
y = a_0 + a_1 * x
```

where `a_0` and `a_1` are the model's parameters. The goal of the learning process is thus to learn the optimal values for `a_0` and `a_1` .

In this article, I make use of the single variable case, where the linear regression model only takes in 1 independent variable as an input. The method generalizes to multiple independent variables. The number of weights that need to be calculated would increase with the number of variables, with each variable having their own weight, and then 1 more overall weight for the bias.

## Cost Functions

Optimization problems are often framed as a minimizing \(or maximizing\) of some measure. Thus, we want to come up with a way to quantify how good our model is. Intuitively, we want our predicted value to be as close to our actual value as possible. Thus, optimizing our model would be trying to reduce that **error** between the predicted and actual value.

In practice, we use **cost functions** to represent the error of a model, and we optimize it by minimizing the error. A common one that is used for the linear regression problem is the **Mean Squared Error \(MSE\)**. 

$$
\min J(pred_i, y_i) = \min\frac{1}{n} \sum^n_{i=1}\left( pred_i - y_i \right)^2
$$

## Gradient Descent

Now that we have our cost function, how do we minimize it? Intuitively, we can think of the value of the cost function at various parameters as a surface. At any point on this surface, we are standing on some type of slope. To find the minimum, we want to go down this slope until we find the lowest possible point we can reach. That is the main idea behind **Gradient Descent** - to move in the direction of our slope until we find the minimum point. Before describing the process of gradient descent, there are a few concepts we have to understand and consider.

### Learning Rate

Firstly, there is the problem of the **learning rate**. Imagine you're in a big pit, and you are trying to walk towards the bottom of the slope. You know the direction it is in, but you don't know how far away it is. Additionally, you are only allowed to take 1 step at a time \(of any length\), and you can only check your position at the end of the step. 

How big of a step should you take? If you play it safe and take small steps, you may take a long time to reach the bottom of the pit. If you decide to take huge steps, you may reach the bottom quicker, but there's also a good chance that you will overshoot the pit, and have to turn back. In gradient descent, the learning rate determines how "big" of a step you take, and it is a parameter that decides how fast your algorithm converges to the minimum point. Since the learning rate is a parameter of the learning algorithm, not your model \(we've already used the term parameter to describe `a_0` and `a_1`\), we call it a _hyperparameter_. 

![Visualization of learning rate problem \(from linked article\)](../../../.gitbook/assets/image%20%282%29.png)

### Local Minimum Problem

Another issue that we have to consider is the **local minimum problem**. In describing the cost function so far, I have visualized it as a big U-shaped pit. While the learning rate is a problem, we know that in this set up, there is a guarantee that at some point, we will find the minimum point. These type of "U-shaped" functions are called **convex cost functions**, with the idea being that there is only 1 minimum point, and at any point in the cost function, the slope points towards it.

Not all cost functions are convex. **Non-convex cost functions** thus have the property that while they may have 1 _global_ minimum point, they have many _local_ minimum points. One can think of the function as instead of a U-shape to instead be a mountain range, with a number of valleys which, when viewing it locally, could seem like a minimum. Traditional gradient descent methods would thus be caught in these local minimum points, as the method is based on local information, and not global ones. 

![Convex vs Non-convex cost functions. Notice the two &quot;minimum&quot; points in the non-convex case.](../../../.gitbook/assets/image%20%283%29.png)

Thankfully, for the problem of linear regression, the cost function is convex, and thus a straightforward one to optimize for.

### Mathematics of Gradient Descent

Now that we understand the problems we have to consider, we can jump in to discuss how gradient descent works conceptually. We've talked about the idea of following a slope to find the minimum. Mathematically, we can find the direction in which the function is pointing to by using derivatives. Thus, gradient descent works updating each parameter by the partial derivative of the cost function on that parameter. For linear regression, given learning rate `alpha,`

$$
f(x_i) = a_0 + a_1x_i, \newline
J(f(x), y) = \frac{1}{n}\sum^n_{i=1}(f(x_i) - y_i)^2 = \frac{1}{n} \sum^n_{i=1}(a_0 + a_1x_i - y_i)^2, \newline
\frac{\partial J}{\partial a_0} = \frac{2}{n}\sum^n_{i=1}(a_0 + a_1x_i - y_i) = \frac{2}{n}\sum^n_{i=1}(f(x_i) - y_i), \newline
\frac{\partial J}{\partial a_1} = \frac{2}{n}\sum^n_{i=1}(a_1 + a_1x_i - y_i)\cdot x_i = \frac{2}{n}\sum^n_{i=1}(f(x_i) - y_i) \cdot x_i,  
\newline
a_{0, t+1} = a_{0, t} - \alpha \cdot \frac{\partial J}{\partial a_0} =  a_{0, t} - \alpha \cdot \frac{2}{n}\sum^n_{i=1}(f(x_i) - y_i), \newline
a_{1, t+1} = a_{1, t} - \alpha \cdot \frac{\partial J}{\partial a_1} =  a_{1, t} - \alpha \cdot \frac{2}{n}\sum^n_{i=1}(f(x_i) - y_i) \cdot x_i.
$$

## Implementing Linear Regression

With any machine learning algorithm these days, a quick and easy way to implement a linear regression model is though our handy `sklearn` library on Python.

```python
from sklearn.linear_model import LinearRegression

lm = LinearRegression()
lm.fit(x_train, y_train)
y_pred = lm.predict(x_test)
score = scoring_function(y_test, y_pred)
```

This doesn't tell us much about the inner workings of the model, but we know for sure that it is optimized and that it works!

Here is a manual implementation of a linear regression model, which is based on the gradient descent formula we've shown above.

```python
from numpy import np

# Set learning rate 'alpha' and number of epochs
alpha = 0.0001
epochs = 1000

# Initialize weights
a_0 = 0
a_1 = 0

e_count = 0
while e_count <= epochs:
    y = np.add(a_0, np.multiply(a_1, x_train))
    error = np.add(y, -y_train)
    a_0 -= alpha * (2/n) * np.sum(error)
    a_1 -= alpha * (2/n) * np.sum(np.multiply(x_train, error))
    e_count += 1
    if e_count % 10 == 0:
        print("MSE at Epoch ", e_count, " : ", np.sum(np.power(error,2))/n)
        
def predict(x_test):
    y_pred = np.add(a_0, np.multiply(a_1, x_test))
    return y_pred
```

### Geeky Stuff: Solving directly with Linear Algebra

{% embed url="https://machinelearningmastery.com/solve-linear-regression-using-linear-algebra/" %}

There's a neat trick to solve linear regression problems which comes from Linear Algebra. I really like it, so I wanted to note it down.

First, note that the linear regression model can be rewritten into a matrix multiplication between two matrices, in the following way:

$$
X = \begin{bmatrix} 1, x_1 \\ \vdots \\ 1, x_n \end{bmatrix}, b = \begin{bmatrix}b_0 \\ b_1 \end{bmatrix}, \newline
Y_{pred} = Xb = \begin{bmatrix} b_0 + b_1 x_1 \\ \vdots \\ b_0 + b_1 x_n \end{bmatrix}.
$$

Thus, this becomes a case of solving a system of linear equations. To do so, we want to minimize the mean squared error, which can be represented as

$$
\min ||Xb - Y||^2 = \min \sum_{i=1}^n(b_0 + b_1x_i - y_i)^2,
$$

and linear algebra gives us that this can be solved using the normal equation

$$
X^TXb = X^Ty \implies b = (X^TX)^{-1}X^Ty
$$

Thus, this gives us a direct formula to find the weights \( $$b$$ \) for the Linear Regression formula from the data. Implementing it in numpy would look something like this:

```python
import numpy as np
from numpy.linalg import inv

X = [[1] + x for x in x_train] # remember to append the 1 to account for bias
Y = y_train.reshape(-1,1)
b = inv(X.T.dot(X)).dot(X.T).dot(y)

# Predict using b
Y_pred = X.dot(b)
```

Isn't that neat! The only issue that this presents is that the inverse calculation may take a long time. To address this, we can use the QR decomposition method to speed this process up. QR decomposition is a method of breaking down an `m * n` matrix into a product of two matrices, Q, which is `m * m`, and R, which is an upper triangular `m * n` matrix.

Decomposing `X` to `Q` and `R`, we can rearrange the equation to

$$
b = R^{-1}Q^Ty,
$$

which while still involving an inverse, it can be calculated quickly due to the upper triangular nature of `R`.

This can also be implemented in `numpy` with the in-built `qr()` function.

```python
import numpy as np
from numpy.linalg import inv, qr

X = [[1] + x for x in x_train] # remember to append the 1 to account for bias
Y = y_train.reshape(-1,1)
Q, R = qr(X) # QR Decomposition
b = inv(R).dot(Q.T).dot(y)

# Predict using b
Y_pred = X.dot(b)
```


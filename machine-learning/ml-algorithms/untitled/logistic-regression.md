# Logistic Regression

{% embed url="https://christophm.github.io/interpretable-ml-book/logistic.html" %}

{% embed url="https://towardsdatascience.com/logistic-regression-detailed-overview-46c4da4303bc" caption="Sources for this page." %}

## What is Logistic Regression?

A logistic regression model is a type of regression model where, in the basic case, it models a type of Bernoulli trial. This means that the model aims to output the probability of success for some kind of True / False test, given the independent variables. Formally, the model takes in independent variables `x_1, ... , x_n` as inputs, and outputs a value between 0 and 1. A classical example of a situation where logistic regression makes sense is in testing whether or not a tumor is malignant or not malignant. 

The logistic regression is built on the Logisitic function, also commonly referred to as a Sigmoid function:

$$
\Sigma(\eta) = \frac{1}{1 + \exp(-\eta)}
$$

![The shape of the Logistic Function.](https://christophm.github.io/interpretable-ml-book/images/logistic-function-1.png)

To get the actual model itself, we can think of the Logistic Regression model as a wrapping of the linear regression model. Where for a linear regression, the output of the model looks like

$$
y = b_0 + b_1x_1 + \cdots + b_nx_n,
$$

what the logistic function allows us to do is to basically wrap this in a Sigmoid function, which then changes the output to a value between 0 and 1. In other words, for a logistic regression model,

$$
y^{(i)} = \Sigma(b_0 + b_1x^{(i)}_1 + \cdots + b_nx^{(i)}_n) = \frac{1}{1 + \exp(-(b_0 + b_1x^{(i)}_1 + \cdots + b_nx^{(i)}_n))}
$$

With this, we can go from a Regression model to a classification model by just stating a threshold \(often set at 0.5\), and just return whether the output is above or below the threshold.

## Cost Function

For ease of presentation, let $$h(x^{(i)})$$ be the predicted value from our model, i.e.

$$
h(x^{(i)}) = \frac{1}{1 + \exp(-(b_0 + b_1x^{(i)}_1 + \cdots + b_nx^{(i)}_n))}.
$$

Then, for the case of a problem with `m` samples of `n` variables each, we can define the cost function of a logistic regression as 

$$
J(b) = \frac{1}{m} \sum^m_{i = 1} C(h(x^{(i)}, y^{(i)}),
$$

where `C` is defined by

$$
C(h(x), y) = \begin{cases} -\log(h(x)) & \text{if }y=1, \\ -\log(1-h(c)) & \text{if }y = 0. \end{cases}
$$

Thus, this cost function decreases if the value of `h(x)` is closer to the actual value of `y`. 

![Cost function for logistic regression](https://s3.amazonaws.com/images.internalpointers.com/2017/10/cost-function-logistic-regression.svg)

We can simplify this cost function into a one line representation, as follows:

$$
J(b) = -\frac{1}{m}\sum^m_{i=1}\left( y^{(i)}\log(h(x^{(i)}))+(1-y^{(i)})\log(1-h(x^{(i)}))\right)
$$

## Gradient Descent

Again, similar to the linear regression case, we get the Gradient Descent update by doing, for learning rate `alpha`,

$$
b_i = b_i - \alpha\frac{\partial}{\partial b_i}J(b).
$$

Working out the derivative, we actually get that

$$
b_0 = b_0 - \alpha \frac{1}{m}\sum^m_{i=1}(h(x^{(i)})-y^{(i)}), \newline
b_j = b_j - \alpha \frac{1}{m}\sum^m_{i=1}(h(x^{(i)})-y^{(i)})x_j, \forall j \in \{1, \ldots,n\}
$$

This actually looks just like the gradient descent function of the multivariate linear regression. What is different is how the $$h(x^{(i)})$$ term expands.

## Implementations in Code

Again, there's a handy implementation located in `python`, under the `sklearn` library.

```python
from sklearn.linear_model import LogisticRegression

x_train, x_test, y_train, y_test = [etc.]

lr = LogisticRegression().fit(x_train, y_train)
lr.predict(x_test) # prints out the categorical guess
lr.predict_proba(x_test) # Prints out probabilities

lr.score(x_test, y_test)
```

Here is a manual implementation of the code.

```python
import numpy as np

def weightInit(n_features):
    w = np.zeros((1, n_features))
    b = 0
    return w, b
    
def sigmoidActivation(result):
    final_result = 1/(1+np.exp(-result))
    return final_result

def modelOptimize(w, b, X, Y):
    m = X.shape[0]
    
    # Prediction
    final_result = sigmoidActivation(np.dot(w, X.T) + b)
    Y_T = Y.T
    cost = (-1/m)*(np.sum((Y_T*np.log(final_result)) + 
                  ((1 - Y_T)*(np.log(1 - final_result)))))
    
    # Gradient Calculation
    dw = (1/m)*(np.dot(X.T, (final_result - Y.T).T))
    db = (1/m)*(np.sum(final_result - Y.T))
    
    grads = {"dw" : dw, "db": db}
    
    return grads, cost
    
def modelFit(w, b, X, Y, learning_rate, n_iters):
    costs = []
    for i in range(n_iters):
        grads, cost = modelOptimize(w, b, X, Y)
        
        dw = grads["dw"]
        db = grads["db"]
        
        w = w - (learning_rate * (dw.T))
        b = b - (learning_rate * db)
        
        if (i % 100 == 0):
            costs.append(cost)
            print("Cost after %i iteration is %f" %(i, cost))
    
    # Final Parameters
    coeff = {"w" : w, "b": b}
    gradient = {"dw" : dw, "db": db}
    
    return coeff, gradient, costs
    
def predict(final_pred, m):
    y_pred = np.zeros((1,m))
    for i in range(final_pred.shape[1]):
        if final_pred[0][i] > 0.5:
            y_pred[0][i] = 1
    return y_pred
    
```




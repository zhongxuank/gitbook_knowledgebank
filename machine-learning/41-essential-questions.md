---
description: >-
  Notes and Thoughts from
  https://www.springboard.com/blog/machine-learning-interview-questions/
---

# 41 Essential Questions

## Algorithms / Theory

### Q: What is the trade-off between bias and variance?

More readings: [https://en.wikipedia.org/wiki/Bias%E2%80%93variance\_tradeoff](https://en.wikipedia.org/wiki/Bias%E2%80%93variance_tradeoff)

**Bias Error** stems from erroneous or overly simplistic assumptions in the learning algorithm. High bias can result in the model underfitting to your data, making it difficult to have a high predictive accuracy.

**Variance Error** is due often to high levels of complexity in the learning algorithm. This leads to models being too sensitive to the variations in the training data, which would lead to overfitting. This means that the noise from your training data is being carried over, which would be meaningless to your test data.

The **bias-variance decomposition** allows us to analyze an algorithms _expected generalization error_ with respect to a particular problem by splitting it into a sum of 3 terms - bias, variance, and the irreducible error due to noise in the underlying dataset. 

Intuition: If you make your model more complex, you'll lose bias but gain variance - too simple and you gain variance \(your test results are more predictable\) but you gain bias \(they don't capture enough information from the training data\). The goal is to find a good trade-off between the two.

### Q: What is the difference between supervised and unsupervised machine learning?

More reading: [https://www.quora.com/What-is-the-difference-between-supervised-and-unsupervised-learning-algorithms](https://www.quora.com/What-is-the-difference-between-supervised-and-unsupervised-learning-algorithms)

**Supervised Learning** is the case when your model is trained on labelled data. As an example, for a classification task, each sample is tagged with a label describing the classification of that sample. On the other hand, **Unsupervised Learning** is the where training is done on unlabelled data. 




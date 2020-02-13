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

### Q: How is K-Nearest Neighbors different from K-means clustering?

More reading: [https://www.quora.com/How-is-the-k-nearest-neighbor-algorithm-different-from-k-means-clustering](https://www.quora.com/How-is-the-k-nearest-neighbor-algorithm-different-from-k-means-clustering)

K-Nearest Neighbors is a supervised learning method - the label assigned to a given test point is decided by the k neighbors closest to the candidate point \(they "vote" with their own label\). The algorithm is optimized by choosing the right k.

On the other hand, K-means clustering does not require labels. Instead, its goal is to group the data points into k groups. This is done by picking k random cluster centers \(usually initialized near the data but far from each other\). Each data point is then assigned to its nearest center. The center will then be moved to the average distance of the data points it is assigned to. This process is repeated until convergence \(or after a specific number of iterations\).

### Q: Explain how the ROC \(Receiver Operating Characteristic\) curve works.

More readings: [https://en.wikipedia.org/wiki/Receiver\_operating\_characteristic](https://en.wikipedia.org/wiki/Receiver_operating_characteristic), [https://journals.plos.org/ploscompbiol/article/file?type=supplementary&id=info:doi/10.1371/journal.pcbi.0020157.sd001](https://journals.plos.org/ploscompbiol/article/file?type=supplementary&id=info:doi/10.1371/journal.pcbi.0020157.sd001)

The ROC curve is a graphical plot that describes the diagnostic ability of a binary classifier system as its discrimination threshold is varied. It compares the model's true positive rates \(y axis\) and false positive rates \(x axis\). It's used as a proxy for the trade-off between the sensitivity of the model \(true positives\) vs the fall-out / probability that it will trigger a false alarm.

### Q: Define precision and recall.




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

More reading: [https://en.wikipedia.org/wiki/Precision\_and\_recall](https://en.wikipedia.org/wiki/Precision_and_recall)

![Diagram of the difference between Precision and Recall.](../.gitbook/assets/precisionrecall.png)

Recall is also known as the true positive rate, and it concerns itself with the model's ability to select relevant items. Its about how many positive samples the model is able to "recall". Mathematically, Recall = TP / TP + FN

Precision on the other hand is also known as positive predictive value - of all the samples that your model marked as positive, how many of them are actually relevant. Mathematically, Precision = TP / TP + FP

### Q: What is Bayes' Theorem? How is it useful in the Machine Learning context?

![Fun handwritten version!](../.gitbook/assets/bayes.jpg)

Bayes' Theorem is a mathematical tool to calculate conditional probabilities. In statistics, it is used in the process of "updating" the distribution of a parameter. In Machine Learning, it is often used in the case of understanding how to calculate the probability of something being true given that it tested true, while knowing other probabilities. 

Let's say that there is a test for a specific disease, and I am interested in finding out the probability that I have the disease, given that I tested positive for it in the test. Assume that the probability that the test returns a positive result given that you have the disease is 80%. Assume also that if you don't have the disease, there is still a 10% chance that the test will return a positive result. Furthermore, we also know that in general, there is a 5% chance that a random member of the public would have the disease.

Thus, we know that the probability of getting a positive result is \(0.8 \* 0.05\) + \(0.1 \* 0.95\) = 0.135. Thus, we know that the probability of me having the disease given that I have a positive result can be calculated by taking the product of the probability that I have the disease and the probability I have a positive result given that I have the test \(0.8 \* 0.05 = 0.04\), and divide it by the probability of getting a positive result. Thus, the final answer would be 0.04 / 0.135, which is only about 30%. 

### Q: Why is "Naive Bayes" naive?

More reading: [https://towardsdatascience.com/whats-so-naive-about-naive-bayes-58166a6a9eba](https://towardsdatascience.com/whats-so-naive-about-naive-bayes-58166a6a9eba)

Naive Bayes makes the assumption that all features of a dataset are mutually independent, and as a result of that assumption, it is possible to calculate the probability of the sample by breaking it down to just a pure, unweighted product of the probability of observing each feature. This is often times not possible in real-life, and is thus a flawed assumption. Thus, this is why it is considered "naive".

### Q: What is the difference between L1 and L2 regularization? 

L1 and L2 comes from the L1 and L2 norms - where L1 norm is calculated by taking the sum of the absolute values of the components, and the L2 norm is derived from the sum of the squares. The intuitive idea is that regularization works by adding a term that minimizes on the L1 / L2 norm of the weights. The difference in the norm results in a difference in the effect of the regularization: L1 regularization tends to result in sparse weights \(some weights will be 0, while the others will be relatively large\), whereas L2 regularization spread the reduction across the weights.

### Q: What's the difference between Type I and Type II errors?

More reading: [https://en.wikipedia.org/wiki/Type\_I\_and\_type\_II\_errors](https://en.wikipedia.org/wiki/Type_I_and_type_II_errors)

Type I errors are also called False Positive. Think of it as telling a dog that it is a cat.

Type II errors are known as False Negatives. Think of this as telling a dog that it is not a dog. 

### Q: What is a Fourier Transform?

More reading: [https://en.wikipedia.org/wiki/Fourier\_transform](https://en.wikipedia.org/wiki/Fourier_transform)

Fourier transformations involve decomposing a function \(i.e. a signal\) into a series of periodic functions of various frequencies. In other words, it transforms the data from a time domain to a frequency domain. It is a method of extracting features from time-based data.

### Q: What is the difference between Probability and Likelihood?

\(I don't quite like the answers I can find online - this part is mostly from Statistical Inference with Maria De Iorio, and it might not be very well phrased\)

Online a lot of the explanation seems to point at Likelihood being interchangeable with the idea of cumulative probability, whereas Probability is the idea of the probability density. I don't necessarily know if this is the right answer. 

The terms Likelihood and Probability are used interchangeably \(which should not be correct\), and the above description does not address this in my opinion. To describe my understanding of the difference, I'll talk about the difference between the fundamental assumptions of classical and Bayesian statistics. 

In classical statistics, when studying a model with an unknown parameter, the parameter is assumed to be fixed, but unknown. This means that the goal is, with more and more test, to work our estimation towards this true value. Due to this, when we are looking at potential parameters, we ask how likely was it the case that the potential parameter is the true value of the parameter, given what we have observed in the sample. This captures the idea of "Likelihood" - we are trying to observe a fixed constant \(the parameter\), and the data can constantly be repeated to work towards an understanding.

On the other hand, the Bayesian view of this is that the unknown parameter is itself a random variable, with its own probability distribution. The data, the samples that we get, are what is fixed, and we can only ever update our understanding of the parameter's probability distribution based on the data we observe, and our prior knowledge of the parameter. Thus, the parameter truly remains in the realm of probability, as it is a random variable. 


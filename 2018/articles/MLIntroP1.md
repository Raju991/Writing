# Machine Learning Basics - Part 1

[<img src="https://images.unsplash.com/photo-1493514789931-586cb221d7a7?ixlib=rb-0.3.5&ixid=eyJhcHBfaWQiOjEyMDd9&s=f8ab2656cca1f3fadd0cc4e254b27c8d&auto=format&fit=crop&w=2251&q=80">](
https://unsplash.com/photos/cXU6tNxhub0)
Photo by Andre Benz on Unsplash - https://unsplash.com/photos/cXU6tNxhub0

The sdfdsfsdf


## Table of Contents

<!-- TOC -->

- [Machine Learning Basics - Part 1](#machine-learning-basics---part-1)
  - [Table of Contents](#table-of-contents)
  - [Definition](#definition)
  - [Linear regression with one variable](#linear-regression-with-one-variable)
    - [Model representation](#model-representation)
    - [Cost function](#cost-function)
    - [Gradient Descent](#gradient-descent)
  - [Linear regression with multiple variables](#linear-regression-with-multiple-variables)
    - [Feature Scaling and Mean Normalization](#feature-scaling-and-mean-normalization)
    - [Learning Rate](#learning-rate)
    - [Polynomial Regression](#polynomial-regression)
    - [Normal equation (for analytical computing)](#normal-equation-for-analytical-computing)
  - [Logistic Regression](#logistic-regression)
    - [Classification](#classification)
    - [Adapted cost function and gradient descent](#adapted-cost-function-and-gradient-descent)
    - [Alternatives to gradient descent](#alternatives-to-gradient-descent)
    - [Multiclass Classification](#multiclass-classification)

<!-- /TOC -->

## Definition

>A computer program is said to learn from experience E with respect to some class of tasks T and performance measure P, if its performance at tasks in T, as measured by P, improves with experience E. - Tom Mitchell

- Supervised Learning
- Unsupervised Learning
- Reinforcement Learning
- Recommender Systems

## Linear regression with one variable

### Model representation

Create a prediction for a certain value by applying a hypothesis ( formed with the learned algorithm ) to a set of other variables. 

Plot data with hypothesis as linear regression.

### Cost function

We want to set the parameters in order to achieve a minimal difference between the predicted and the real values.

> We can measure the accuracy of our hypothesis function by using a cost function. This takes an average difference (actually a fancier version of an average) of all the results of the hypothesis with inputs from x's and the actual output y's.

![costfunction](../assets/mlIntro/costFunction.png)

### Gradient Descent

Keeps changing the Parameters to reduce the cost function gradually. With each iteration we shall come closer to a minimum. With each iteration the parameters must be adapted simultaneously! The size of a "step"/iteration is determined by the parameter alpha (the learning rate).

>The way we do this is by taking the derivative (the tangential line to a function) of our cost function. The slope of the tangent is the derivative at that point and it will give us a direction to move towards. We make steps down the cost function in the direction with the steepest descent.

![costfunction](../assets/mlIntro/gradientDescent.png)

Choosing the value of alpha is crucial. If it is too small the algorithm will be slow, if it is too large it will fail to converge. 

When specifically applied to the case of linear regression, a new form of the gradient descent equation can be derived, where m is the size of the training set. Again both paramters must be updated simultaneously.

![costfunction](../assets/mlIntro/gradientDescentLR.png)

>Note that, while gradient descent can be susceptible to local minima in general, the optimization problem we have posed here for linear regression has only one global, and no other local, optima; thus gradient descent always converges (assuming the learning rate α is not too large) to the global minimum.

## Linear regression with multiple variables

Now, instead of one feature/variable that is responsible for a certain outcome we have multiple ones.

Therefore the hypothesis changes accordingly and takes multiple parameters into account. The same applies for the gradient descent. It simply is extend for the additional parameters, which must be updated.

![costfunction](../assets/mlIntro/logisticRegGD.png)

### Feature Scaling and Mean Normalization

To make sure that all values of features are on a same scale and have the same mean it's necessary to use Feature Scaling and Mean Normalization.

>Feature scaling involves dividing the input values by the range (i.e. the maximum value minus the minimum value) of the input variable, resulting in a new range of just 1. Mean normalization involves subtracting the average value for an input variable from the values for that input variable resulting in a new average value for the input variable of just zero.

### Learning Rate

To choose a suitable learning rate, gradient descent has to be plotted and "debugged".

> Make a plot with number of iterations on the x-axis. Now plot the cost function, J(θ) over the number of iterations of gradient descent. If J(θ) ever increases, then you probably need to decrease α.

If J(0) stops to decrease significantly in an iteration step convergence can be declared.

### Polynomial Regression

Features can be improved by re-defining the hypothesis function into a quadratic, cubic or square root function.

In this case extra emphasize must be applied to feature scaling!

### Normal equation (for analytical computing)

Instead of using gradient descent for gradually minimizing the cost function, the normal equation sets the derivatives to zero. 

![normalEquation](../assets/mlIntro/normalEquation.png)

The normal equation doesn't need a learning rate alpha and no iteration at all but requires the transpose of the design matrix. When you have a large number of features (eg 10000) the calculation will take longer than the iterative process with gradient descent. To improve the quality of the normal equation algorithm features should be regularized and redundant features deleted. 

## Logistic Regression

### Classification

To classify data the result shall eiter be 0 or 1 (binary classification). From a regression point of view this can mean to classify output, that is >=0.5 as 1 and < 0 as 0 (whereas 0,5 is the decision boundary).

The adapted hypothesis, using the logistic/sigmoid function, would now be:

![logRegHypoth](../assets/mlIntro/logRegHypoth.png)

It returns the probability for the output being 1. 

### Adapted cost function and gradient descent

Due to the use of the sigmoid function the cost function has to be adapted accordingly by using the logarithm. Since the goal now is not to minimize the distance from a predicted value, but rather to minimize the distance between the output by the hypothesis and y (0 or 1). 


![costFLogReg](../assets/mlIntro/costFLogReg.png)

Or for a vectorized implementation:

![costFLogRegVec](../assets/mlIntro/costFLogRegVec.png)


However, gradient descent stays the same because the formula uses the derivative part of the hypothesis!

![GDLogReg](../assets/mlIntro/GDLogReg.png)

Or for a vectorized implementation:

![GDLogRegVec](../assets/mlIntro/GDLogRegVec.png)

### Alternatives to gradient descent

More complex opimization algorithms like 
- Conjugate Gradient, 
- BFGS or 
- L-BFGS 

often allow faster computation with no need for picking a learning rate alpha.

### Multiclass Classification

The previously described classification problem solving only works for binary classification. Having more possible outcome than n=2 is called multiclass classification. To apply the concept on multiple classes the "one-vs-all" method is used, which is essentially applying the binary classification on each class (one class is positive, all the rest is negative). Instead of setting y to either 0 or 1, y is set to i, which itself is tested against all the other classes. Basically the process is twofold: 
1. Setting the logistic classifier to y. (if y is 3, we create 3 classifiers) 
2. New input is tested against all classifiers and choose the one with the highest probability.

---

Thanks for reading my article! Feel free to leave any feedback! 

---

Daniel is a LL.M. student in business law, working as a software engineer and organizer of tech related events in Vienna. 
His current personal learning efforts focus on machine learning. 

Connect on:
- [LinkedIn](https://www.linkedin.com/in/createdd) 
- [Github](https://github.com/DDCreationStudios)
- [Medium](https://medium.com/@ddcreationstudi)
- [Twitter](https://twitter.com/DDCreationStudi)
- [Steemit](https://steemit.com/@createdd)
- [Hashnode](https://hashnode.com/@DDCreationStudio)

<!-- Written by Daniel Deutsch (deudan1010@gmail.com) -->
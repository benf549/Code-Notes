# Notes From Stanford CS229

### Linear Regression

###### What is a linear regression?

*In a regression problem, we aim to predict the output of a continuous value, like a price or a probability. Contrast this with a classification problem, where we aim to select a class from a list of classes (for example, where a picture contains an apple or an orange, recognizing which fruit is in the picture).*

The line that when drawn through data splits it into n groups evenly.



###### Example Data: Predicting House Value

We would expect increased # of bedrooms and sq. feet to increase the value of the home linearly and thus can use linear regression.

| Size (sq. feet) | # Bedrooms | Price ($1000) |
| :-------------: | :--------: | :-----------: |
|      2104       |     3      |      400      |
|      1416       |     2      |      232      |
|      1534       |     3      |      315      |
|       843       |     2      |      178      |



Define a hypothesis function (an affine function) that takes in a vector X and makes a prediction such as price:
$$
h(x) = \theta_0 + \theta_1x_1 + \theta_2x_2 \ + \ ...
$$
Where x_1 is the first factor e.g. size and x_2 is the second factor e.g. # bedrooms. **x_0 is always 1** and is omitted above. Therefore the hypothesis function can also be written:
$$
h(x) = \sum _ {j=0} ^ {n} \theta_j x_j
$$

###### Variables

| Variable | Definition                                                   |
| -------- | ------------------------------------------------------------ |
| m        | Number of rows in the training data                          |
| theta    | The parameters being adjusted to create fit                  |
| x        | The inputs or features                                       |
| y        | The output or target variable                                |
| n        | The number of features of inputs you have per training point |
| alpha    | The learning rate (initialized to 0.1)                       |


$$
\theta = \begin{bmatrix} \theta_0 \\ \theta_1 \\ \vdots \\ \theta_n \end{bmatrix}
\quad \textrm{and} \quad 
x = \begin{bmatrix} x_0 \\ x_1 \\ \vdots \\ x_n
\end{bmatrix}
$$
We will use these weight and input vectors to construct a cost function that can be minimized and a prediction function that can be used to predict Y from X given a particular theta.
$$
\textrm{Prediction/Hypothesis Function: The goal is to select a} \ \theta \ \textrm{such that:}\\
h_\theta(x) = y   \\
\textrm{Define Cost Function J as square of difference between prediction and true values for given theta:}\\ \quad J(\theta) = \frac{1}{2}\sum_{i=1}^m (h_\theta(x^{(i)}) - y^{(i)})^2
$$


###### Gradient Descent Algorithm

Want to find the absolute minimum of the cost function corresponding to the theta at which h(x) produces the predictions closest to y
$$
\theta_j := \theta_j - \alpha \frac{\partial}{\partial\theta_j} J(\theta) \\
\textrm{Plug in J equation from above} \\
\theta_j := \theta_j - \alpha \frac{\partial}{\partial\theta_j} \frac{1}{2}\sum_{i=1}^m (h_\theta(x^{(i)}) - y^{(i)})^2 \\
\textrm{Plug in h(x) from above and move derivative} \\
\theta_j := \theta_j - \alpha \frac{\partial}{\partial\theta_j} \frac{1}{2}\sum_{i=1}^m ( \sum _ {j=0} ^ {n} \theta_j x_j - y^{(i)})^2 = \theta_j - \alpha  \frac{1}{2}\sum_{i=1}^m \frac{\partial}{\partial\theta_j}( \sum _ {j=0} ^ {n} \theta_j x_j - y^{(i)})^2 \\
\textrm{Recognize derivative of sum removes theta_j leaving x_j so finally:} \\
\theta_j := \theta_j - \alpha  \sum_{i=1}^m (h_\theta(x^{(i)}) - y^{(i)})x_j^{(i)}
$$
The := operator means theta is being updated. Repeat these updates for until convergence/training is complete.



###### Stochastic Gradient Descent

This is opposed to the 'Batch Gradient Descent' algorithm as introduced above. 

Applies the gradient descent algorithm per training point rather than as a sum over all of the data points. This allows the training data to be processed in batches rather than necessarily an epoch at a time. 

Stochastic gradient descent necessarily takes a noisy path down the gradient but is more useful for large datasets that cannot be loaded into memory all at once. The noisy path will never converge but with a sufficiently large dataset, minimizes the cost function.
$$
\theta_j := \theta_j - \alpha(h_\theta(x^{(i)}) - y^{(i)})x_j^{(i)}
$$

###### Normal Equation

A formula that calculates the absolute minimum for linear regression without applying gradient descent. Is found by linear algebra manipulation of $ J(\theta)$ set equal to a zero vector.
$$
\theta = (X^TX)^{-1}X^TY
$$

This is a unique property of the linear regression and actually can replace the gradient descent algorithm as it gives the minimum cost as long as X is invertible.



### Locally Weighted Regression

Also known as *Weighted Least Squares* or as *LOESS*

A parametric algorithm fits a fixed set of parameters while a non-parametric algorithm has a number of parameters that grows with the size of the training set.

A locally weighted regression is non-parametric. When making a prediction, the locally weighted regression takes in an X to make a prediction and looks at the training points that it knows near that point and weights their influence based on the distance they are from the test point. Essentially fits a straight line using closest known values. 

Fits theta to minimize a cost function as before. 

###### Cost Function

Choose theta to minimize.
$$
J(\theta) = \sum_{i=1}^m w^{(i)}(y^{(i)} - \theta^Tx^{(i)})^2
$$
such that the weight function is defined as:
$$
w^{(i)} = e^{\frac{-(x^{(i)}-x)^2}{2\tau^2}}
$$


Where tau sets the broadness of the curve. It's probably between zero and one. 

So that small distances give a weight near 1 while large distances have weight near zero. Takes the form of a bell curve centered at the point observed. It is not a gaussian curve but just functions to weight data locally.

![image-20210117114215533](C:\Users\benfy\AppData\Roaming\Typora\typora-user-images\image-20210117114215533.png)

Essentially doing a linear fit with weights. 

Locally weighted linear regression is most useful **n is small** (2 or 3) and there's a lot of data. 

Implemented in Machine Learning Fundamentals on GitHub as '***Locally Weighted Regression.ipynb***' 

### Logistic Regression

The most commonly used ML algorithm. A classification question. Ex: Is tumor malignant (y=1) or benign (y=0).

Assume a binary classification such that
$$
h_\theta(x) \in [0,1] \\
h_\theta(x) = g(\theta^Tx) = \frac{1}{1+e^{-z}}
$$
Where is the **sigmoid function** (aka the logistic function) which outputs values between zero and one. 

![image-20210117122114847](C:\Users\benfy\AppData\Roaming\Typora\typora-user-images\image-20210117122114847.png)

###### PMF

Out hypothesis is no longer a linear function of theta multiplied by x. We are now taking the linear regression and passing it through the sigmoid function which returns values between 0 and 1. We can use this as a classification algorithm.
$$
P(y=1 | x;\theta) = h_{\theta}(x) \\
P(y=0 | x;\theta) = 1-h_{\theta}(x)
$$
Because y can only take on two values, we can write the probability (as a binomial PMF?)
$$
P(y | x;\theta) = h_{\theta}(x)^y \ (1-h_{\theta}(x))^{1-y}
$$
###### Gradient Ascent

Using ***maximum likelihood estimation***, the maximum theta can be found with **Batch Gradient Ascent**:
$$
\theta_j := \theta_j + \alpha \ \frac{\partial}{\partial\theta_j} \ l(\theta)\\
\theta_j := \theta_j + \alpha \ \sum_{i = 1}^m (y^{(i)} - h_\theta(x^{(i)}))x_j^{(i)}
$$
where $ l(\theta) $ is the log-likelihood of the PMF and the second equation is the solution to the partial derivative. Thus, the thetas are updated almost identically to those in the linear regression gradient descent algorithm.

There is no known Normal Equation to solve logistic regression.

###### Newton's Method

An alternative algorithm to Gradient Ascent. It can be faster in some cases. 

Have a function $f(\theta)$ and want a $\theta$ such that it is zero. So this function will be the derivative of our function. 

Starting at a random point on the function, we find the tangent line at that point and where it equals zero. The point at which the tangent line equals zero then becomes our next point which we then plug into the function and see where that equals zero. This process repeats until the function outputs a number that is sufficiently close to zero. 
$$
\theta^{\ t+1} := \theta^t - \frac{f(\theta^t)}{f'\theta^t}
$$
let $f(\theta) = l'(\theta)$ so:
$$
\theta^{\ t+1} := \theta^t - \frac{l'(\theta^t)}{l''\theta^t}
$$
Very fast because it has quadratic convergence (number of sig figs near zero doubles per iteration) however, in high dimensional problems, you have to invert very large matrices which is computationally expensive. Therefore, **Newton's method is usually faster unless the data has a large n**.
$$
\theta^{\ t+1} := \theta^t + H^{-1}\nabla_\theta l
$$
where $ H^{-1} $ is the inverted Hessian Matrix and $\nabla_\theta l$ is  the matrix of partial derivatives of l. Computing the inverted Hessian is computationally expensive if large.


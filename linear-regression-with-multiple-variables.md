# Linear Regression With Multiple Variables

![Source](https://cdn-images-1.medium.com/max/1200/0*tyZqTVxTLWiz1r3-)

In my previous article, I have discussed [Linear Regression with one variable](https://medium.com/swlh/linear-regression-with-one-variable-f205db7208ab?source=friends_link&sk=2cc612f4ad21c607eef818cdf9f8c991). There I have briefly covered the Linear regression algorithm, cost function and gradient descent. These concepts form the basis for this article. So if you’re not that comfortable with them, consider referring to my previous article.

So far we have considered a simple problem, where the output variable depended on just one feature\(i.e x\).

Eg: Predicting house prices, where prices of a house just depend on its size.

But often, we don’t have that simple dataset. Most of the time, the output variable depends on more than one feature. For eg. the price of a house depends on many other factors like the age of the house, location, no. of bedrooms, no. of floors, infrastructure etc.

So in order to find a relationship between the input variables and the output we need to understand Multivariate linear regression.

#### Multivariate linear regression

This is quite similar to linear regression with one variable, but with multiple features that contribute to the dependent variable.

**Notations**

* x₁, x₂, …, xₙ denotes n features\(eg size of a house, no. of bedrooms, age of house etc\)
* y = the output variable to be predicted
* n = the no. of features
* m = no. of training examples
* x⁽ⁱ⁾ = the iᵗʰ training example
* xⱼ⁽ⁱ⁾ = the value of feature j in the iᵗʰ training example

**Multivariate form of Hypothesis function**

The multivariate form of the hypothesis function is as follows:

```text
h(x)= θ₀ + θ₁x₁ + θ₂x₂ + … + θₙxₙ
where θ₀, θ₁, θ₂, …, θₙ are the parameters and x₁, x₂, …, xₙ denotes n features
```

In order to understand the above equation, we can think x₁ as size of the house in square meters, x₂ as no. of floors, x₃ as no. of rooms etc. Similarly θ₀ as basic price of house, θ₁ as price of a house per square meters, θ₂ as price per floor, θ₃ as price per room etc. You can see how different features have been adjusted in one equation.

The above equation can be more concisely written with help of matrix representation. Instead of thinking θ₀, θ₁ … θₙ as different features, we will think of a \(n+1\) by 1 matrix Θ, having elements — θ₀, θ₁ … θₙ and similarly a \(n+1\) by 1 matrix x, having elements — x₀, x₁, x₂, …, xₙ \(x₀ = 1, is added for making the matrices Θ and x compatible for multiplication.\) Or more precisely matrix x⁽ⁱ⁾ having elements — x₀⁽ⁱ⁾, x₁⁽ⁱ⁾, x₂⁽ⁱ⁾, …, xₙ⁽ⁱ⁾

![](https://cdn-images-1.medium.com/max/1200/0*1OgvxvGnrFHmBKDC)

The above image is the hypothesis function for one training example where x₁, x₂, …, xₙ are the feature values for that particular training example.

Now let’s have a look at how the cost function modifies for multivariate linear regression.

**Multivariate form of cost function**

As we already know, cost function helps us to find the accuracy of the hypothesis function.

![cost function for univariate linear equation](https://cdn-images-1.medium.com/max/1200/0*6T0FLZAcDRb2RmyB)

For multivariate, instead of just two parameters, we have more parameters to deal with.

![](https://cdn-images-1.medium.com/max/1200/0*vHx2pj2QY51TXwhw)

y⁽ⁱ⁾ is the output for iᵗʰ training example and h\(x⁽ⁱ⁾\) is the predicted output.  
Like done before, the parameters can be represented in matrix form —

![](https://cdn-images-1.medium.com/max/1200/0*3N2r4MXjq0063Jn-)

Θ is \(n+1\) by 1 matrix of θ₀, θ₁ … θₙ

**Multivariate form of Gradient descent**

Gradient descent for univariate linear equation —where j = 0, 1

![](https://cdn-images-1.medium.com/max/1200/0*I0aUHw-6De5DiI0z)

For multivariate —

![where j = 0, 1, &#x2026;, n](https://cdn-images-1.medium.com/max/1200/0*HgYRoySMxJBvUQJj)

As we know, Gradient descent is an algorithm to find the minimum of a function. Therefore, the above equation is used to find the minimum of a function with multiple variables.

Contour plots help in better visualization of 3-d plots. This would help us in analyzing the gradient descent function better. So let’s understand it.

#### Contour plots

It helps us to plot 3-D curves conveniently in 2-D space. Imagine a function with 2-D inputs\(say x and y\) and a 1-D output\(say z\).

![Plotted using 3-D Calculator-GeoGebra](https://cdn-images-1.medium.com/max/1200/0*BDM02oW6wUvfdwHN)

Consider above graph — z = x² + y². The idea is to slice the 3-D graph by a bunch of planes passing parallel to x-y plane.

![Plotted using 3-D Calculator-GeoGebra](https://cdn-images-1.medium.com/max/1200/0*MjKTW66AsS2HGJ7w)

All these planes have one thing in common — For every plane, z is constant i.e they represent the constant value of the function itself.

![Plotted using 3-D Calculator-GeoGebra](https://cdn-images-1.medium.com/max/1200/0*SGTWaBH2z6RdaPLK)

The black lines outline the intersection of the 3-D curve and the plane passing through it. These are called contour lines. Each contour line is special in a way that the points they outline have the same z value. Squishing these contour lines in x-y planes gives us the following contour plot —

![](https://cdn-images-1.medium.com/max/1200/0*OhFYab7ggB3SHktu)

_Et voila!_

Now we have a 2-D graph representing our previous 3-D graph. Each concentric circle represents a constant output of a function. You might have noticed that some lines are closer than other lines. The distance between contour lines gives us an idea about how steep the surface is.

* When the lines are far apart, it means the surface is less steep over there because you need to move a larger distance to increase the value of the function by one unit.
* When the lines are close, it means the surface is steeper because you need to move a smaller distance to increase the function by the same value.

In the above plot, warmer colors like red and orange represent higher values of the function and cooler colors like green and blue represent low values of the function.

**Contour plots for Gradient Descent**

![](https://cdn-images-1.medium.com/max/1200/0*qnSmAn5W6dZ9ct6W)

The above figure gives a rough idea about how the Gradient descent function works. The cross mark denotes some random θ₁, θ₂ values. As previously stated the warmer colors denote higher values of the function and cooler colors denote the lower value of the function. Since gradient descent is all about finding the function’s minima hence the actual minima of our function is located somewhat around the center of concentric circles which is also where our arrows are heading towards.

Also as stated above close contour lines denote steep surface i.e large derivatives and comparatively, far contour lines denote less steep surface i.e small derivatives. Thus the length of the arrow in the contour plot decreases as we approach the minima.

The Gradient Descent function works fine when the data are in somewhat the same range. But rarely do we have such datasets. Most of the times the data contains features highly varying in magnitude and range.

![](https://cdn-images-1.medium.com/max/1200/0*F3txP99hZcGEc7TV)

As you can see, without feature scaling the contour plots are long and elliptical. Thus it is easier for gradient descent to overshoot the minima and will take more time to converge. But with feature scaling the gradient descent converges quickly.

#### Feature Scaling

Two techniques that will help us in Feature scaling and Mean normalization.

**Feature scaling**: This involves dividing the input values by the range\(i.e maximum value-minimum value\). It ensures a new range of just 1.

**Mean normalization:** This involves subtracting the average of the input variables from the value of that input variable which results in a new average value for the input variable of 0.

Formula: xᵢ = xᵢ-μᵢ/sᵢ

where sᵢ is the range of values.

**Debugging Gradient descent function**

There is a nice way of detecting if your gradient descent function is working the way it should work.

Plot a graph with no. of iterations\(gradient descent is an iterative algorithm i.e the values of θ₀, θ₁… changes in steps.\) on x-axis and cost function on the y-axis.

Hopefully, if your gradient descent function is working fine, then as the no. of iteration increases, the cost function will decrease.

And this is what we even expect — As the gradient descent function works, it should take us closer to the cost function’s minima.

But if any time you find your cost function increasing, then probably you need to decrease the α as large learning rates can make your gradient descent to overshoot function’s minima.

#### Normal Equation — An alternative for Gradient descent

Unlike Gradient Descent which is an iterative algorithm, the Normal equation allows us to solve for Θ analytically. It basically exploits the fact that the derivative of a function is 0 at its minima. This allows us to find the optimum θ without iteration.

Normal Equation: θ = \(XᵗX\)⁻¹Xᵗy

where X is an m by \(n+1\) design matrix in which each row represents a particular training example and y is an m-dimensional vector of outputs.

**Comparison of Gradient descent and Normal Equation**

![](https://cdn-images-1.medium.com/max/1200/0*a6z10Br8T61CnUo6)

As seen above time complexity of the Normal Equation method is O\(n³\). Thus normal equation methods slow down for large n and in those cases, it is better to use a Gradient descent algorithm.

That’s all from my side. Hope everything makes sense.

Reference —

[Andrew Ng’s Machine Learning Course](https://www.coursera.org/learn/machine-learning/home/welcome)

Thanks for reading!


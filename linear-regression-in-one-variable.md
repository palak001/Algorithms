# Linear Regression in one variable

![Source: Pinterest](https://cdn-images-1.medium.com/max/1400/0*7yKppqbQTKqx8XzG.jpg)

Linear Regression is probably the very first learning algorithm that one encounters in their early machine learning journey.  
It is the oldest and widely used supervised learning algorithm.

#### What’s Supervised Learning?

Well, any machine learning problem can be assigned to one of the two broad classifications:  
Supervised learning and Unsupervised learning

In Supervised learning, we are given with a data set and already know what our output should look like. All our algorithm does is, figure out a relationship between the input and the output and using that relationship predict even more correct answers for test inputs.

Supervised learning problems are further categorized into **Regression** and **Classification** problems.  
In Regression problems, we map our input variables to some continuous function. For eg: Given the data about size of the house, predict their prices. So the price of a house is the function of its size. And clearly it’s a continuous function.

In Classification problems, we map our input variables to a discrete function. For eg: Given the data about favorite colors of different people, predict whether it’s a girl or a boy. Now, definitely it is a discrete function, you are mapping all inputs to either a boy or a girl.

Linear Regression is a Regression algorithm.  
\(Well, if this sounds like common sense then let me tell you Logistic Regression is a Classification algorithm!\)

So over with the background story, Let’s dive deep into Linear Regression Algorithm.

#### Linear Regression Algorithm

![From Andrew Ng&#x2019;s Machine learning course](https://cdn-images-1.medium.com/max/1400/0*TH2NQ9uJx7I-mBG3)

The above diagram conveniently gives a brief overview of Linear Regression Algorithm. We feed our learning algorithm with some data set\(Training set\), which then outputs a functions called Hypothesis.   
Hypothesis approximates a target function for mapping inputs to outputs.  
For linear regression in one variable, our hypothesis function is of the form —

```text
h(x) = θ0 + θ1x
where θ0 and θ1 are the parameters.
```

![Image by author](https://cdn-images-1.medium.com/max/1400/1*6egMs9kaw3HFwtQiANtoaQ.png)

The line seen in the graph is the Hypothesis function. This line is the best fit that passes through most of the points and reduces the error which is the average squared vertical distances of the scattered points from the line as shown below.

![Source: Internet](https://cdn-images-1.medium.com/max/1400/0*fRC_65Zpkl9SZtaS.gif)

Now one thing is for sure, we can’t tell the hypothesis function by merely looking at the graph! We need some systematic way to figure it out. Here is when Cost function comes for our rescue.

#### Cost Function

Cost function helps us to figure out which hypothesis best fits our data. Or more formally, It helps us to measure the accuracy of our hypothesis.

Hypothesis —

```text
h(x) = θ0 + θ1x
```

```text
θ0 and θ1 are the parameters.
```

![From Andrew Ng&#x2019;s Machine Learning YouTube course](https://cdn-images-1.medium.com/max/1400/1*fQutqEuFCRsiPTriKLWOFw.png)

You can clearly see how the hypothesis function changes on changing _θ_0​ and _θ_1.

So main idea —   
Given certain _θ_0​ and _θ_1, Cost function helps us to find the accuracy of our hypothesis.

Mathematically, Cost function —

![Cost function from Andrew Ng&#x2019;s ML course](https://cdn-images-1.medium.com/max/1400/1*xXr2YaMcE0KnFAimpT2kHA.png)

```text
(h(x) — y)² : Squared vertical distances of the scattered points from the hypothesis
∑(h(x) — y)²/2m: Average Squared vertical distances of the scattered points from the hypothesis, i.e Mean Squared error
```

You might be wondering what’s 2 doing in the equation? Well, the mean is halved as a convenience for the computation of the gradient descent, as the derivative term of the mean square function will cancel out the half term.

_J_\(_θ_0​,_θ_1​\) is the cost function, often called squared error function.

So now we have our hypothesis function and we have a way of measuring how well it fits into the data\(with help of cost function\). All we need to do is estimate the value of parameters in hypothesis function for which the cost function is minimum. That’s where gradient descent comes into picture.

#### Gradient Descent

Gradient Descent is an algorithm to minimize a function.   
It turns out that in case of Linear regression, the cost function is a convex function i.e it has only one global minima as shown in the following figure.

![Source: Internet](https://cdn-images-1.medium.com/max/1400/0*OHYVpB111n4tr80y)

Above figure shows a graph with cost function on z-axis, θ0 on x-axis and θ1 on y-axis.   
The way we look for minimum point in the graph is —

* Choose any random point on the graph.
* Then look around and move in the direction of steepest descent\(which can be calculated with help of Gradient of a function\) i.e direction which helps in decreasing the function’s output most quickly.
* The length of the step is determined by the parameter, alpha which is called the learning rate.

**Gradient descent algorithm**

So the algorithm to minimize the function is to compute the direction of steepest descent and then take a small step downhill and just repeat that over and over again, until you find the function’s minima.

Mathematically,

![where j = 0, 1 from Andrew Ng&#x2019;s course](https://cdn-images-1.medium.com/max/1400/1*ds12X6AoA2AbOd-me-quBA.png)

```text
i) := means assigning RHS to LHS
```

```text
ii) α is the learning rate i.e the length of the steps taken to reach downhill which is always positive.
```

```text
iii) The derivative term gives us the direction of steepest descent.
```

Let θ0 = 0, it’ll help us in understanding Gradient descent function better.

![Source: Internet](https://cdn-images-1.medium.com/max/1400/0*iMwnisDlNsr8_IGb.JPG)

**Gradient Descent for a single parameter —**

![](https://cdn-images-1.medium.com/max/1400/1*bJ5Tq9bCv2D87iYZfo87BQ.png)

From above equation, following things can be inferred —

**Derivative term**

* When the derivative term is positive i.e when slope is increasing, θ1 will decrease.
* When the derivative term is negative i.e when the slope is decreasing, θ1 will increase. So it’s clear that the derivative term gives us the direction to move towards.

**Learning Rate**

The size of each step is determined by α, known as the Learning rate. The value of α should be selected with care to ensure that the gradient descent algorithm converges in a reasonable time.

* If α is too small, gradient descent can be slow.
* If α is too large, gradient descent can overshoot the minimum and may even diverge.

Another thing to notice is that,  
Gradient Descent can converge to a local minimum even with fixed α. This is because as we approach local minima, the slope automatically starts decreasing, thus gradient descent will automatically take smaller steps. So no need to change α over time.

With help of Gradient Descent Algorithm we can find the appropriate parameters for our hypothesis.

So this is all from my side. Hope every thing makes sense.

Reference:   
[Machine Learning — Andrew Ng’s course](https://www.youtube.com/playlist?list=PLLssT5z_DsK-h9vYZkQkYNWcItqhlRJLN)

Thanks for reading!


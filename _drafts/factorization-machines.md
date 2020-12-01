Title: An Illustrated Guide to Factorization Machines
Date: 2020-04-17 03:19
Modified: 2020-04-17 03:19
Category: illustration
Slug: factorization-machines-illustrated
Summary: Learn about the working mechanism of Factorization Machines with visual examples.
Status: draft
Authors: Madan Baduwal

Factorization machines is a popular techniques used in building recommendation systems.


## Scenario

Assume we need to build a recommendation system for a TV-series streaming service. You are provided a historical dataset of ratings by users for different series.  

![](https://upload.wikimedia.org/wikipedia/en/thumb/3/33/Silicon_valley_title.png/250px-Silicon_valley_title.png){.img-center}

|User|Game of Thrones|Silicon Valley|
|---|---|---|
|A	|2	|5|
|B	|4	|2|
|C| |5|

# Problem with existing models
We start with simple linear regression model to predict rating using user and series as features. 
To use categorical data like user and series in regression, we perform one hot encoding on it.

|A|B|C|Game Of Thrones|Silicon Valley| |Rating|
|---|---|---|---|---|---|---|
|**1**|0|0|**1**|0| |2|
|**1**|0|0|0|**1**| |5|
|0|**1**|0|**1**|0| |4|
|0|**1**|0|0|**1**| |2|
|0|0|**1**|0|**1**| |5|

So, the rating y(x) is predicted by the linear combination of weight for user and the series.
<pre class="math">
rating = y(x) = w_0 + \sum_{i=1}^{n} w_i x_i
</pre>

We can predict the rating of 5 given by user "A" for "Silicon Valley" as:

|*A*|B|C|Game Of Thrones|*Silicon Valley*|
|---|---|---|---|---|
|**1**|0|0|0|**1**|


<pre class="math">
w_0 + w_{A}*1 +w_{B}*0 + w_{C}*0 + w_{game of thrones}*0 + w_{silicon valley}*1  
</pre>
<pre class="math">
y(x) = w_0 + w_{A} * 1 + w_{silicon valley}*1
</pre>
<pre class="math">
y(x) = w_0 + w_{A} + w_{silicon valley}
</pre>

We can see this takes into account only the user and series individually but doesn't consider their interaction. So, model predictions will not be very good.

## Polynomial Regression
To fix this, we can switch to polynomial regression. For that, we add interactions to the linear regression model.
<pre class="math">
rating = y(x) = w_0 + \sum_{i=1}^{n} w_i x_i + \sum_{i=1}^{n} \sum_{j=i+1}^{n} w_{i,j} x_i x_j
</pre>

So, for user A rating 'Silicon Valley', the interaction features would be:  

|*A*|B|C|Game Of Thrones|*Silicon Valley*|
|---|---|---|---|---|
|**1**|0|0|0|**1**|

- A * B = 1 * 0 = 0
- A * C = 1 * 0 = 0
- A * Game of Thrones = 1 * 0 = 0
- A * Silicon Valley = 1 * 1 = 1
- B * C = 0 * 0 = 0
- B * Game of Thrones = 0 * 0 = 0
- B * Silicon Valley = 0 * 1 = 0
- C * Game of Thrones = 0 * 0 = 0
- C * Silicon Valley = 0 * 0 = 0
- Game of Thrones * Silicon Valley = 0 * 1 = 0

All of the interactions will result to zero on multiplication and we will be left with:  
<pre class="math">
A * Silicon\ valley = 1*1 = 1
</pre>

<pre class="math">
\sum_{i=1}^{n} \sum_{j=i+1}^{n} w_{i,j} x_i x_j = w_{A, silicon valley} * A * silicon valley = w_{A, silicon valley}
</pre>

So, our model will predict the rating based on user, tv-series and it's interaction.
<pre class="math">
y(x) = w_0 + w_{A} + w_{silicon valley} + w_{A, silicon valley}
</pre>
which can be generalized for user U and item i as:  

<pre class="math">
y(x) = w_0 + w_{u} + w_{i} + w_{u,i}
</pre>



## Problem 1: Explosion in dimensions
As you saw above, using even a polynomial regression drastically increases the number of weights we need to learn for the model. The example we took was just of 3 users and two tv-series. If we had 1000 users and 1000 series, the number of interaction weights to learn would be:  


| |Series 1|Series 2|Series ...|Series 1000|
|---|---|---|---|---|
|**User 1**|...|...|...|...|
|User 2|...|...|...|...|
|User ...|...|...|...|...|
|**User 1000**|...|...|...|...|
  
Interactions = Users * Series = 1000 * 1000 = 1 million

This causes a explosion in the number of features.

## Problem 2: Sparsity
A user rates only a few series and so most of the user-series interaction is not present in training data. Without having seen the training data, polynomial regression can't infer the weights for unseen interaction.


# Proposed Solution
Author of the paper **Steffen Rendle** proposed a novel idea of extending polynomial regression with the ideas inspired by matrix factorization to solve the problems stated above.

Matrix factorization models are already popular in field of recommendation systems. Let's say we have a user-series ratings matrix as show below.

|User|Game of Thrones|Silicon Valley|Flash|
|---|---|---|---|
|A	|2	|5|4|
|B	|4	|2||
|C| |5|3|
  
We can break this matrix into two smaller matrix.broken into  
 
|User|Feature 1|Feature 2|
|---|---|---|
|A	|...|...|
|B |...|...|
|C|... |...|


|Series|Game of Thrones|Silicon Valley|Flash|
|---|---|---|---|
|Feature 1	|...|...|...|
|Feature 2|...|...|...|

From the two matrices, we can determine the ranking using the dot product for a specific user and specific series. 
Even when we don't have the user-series interaction in the training data, we can infer the rating a user would give for a new series by multiplying the corresponding feature vectors for user and series.

Though factorization models solve the problems of polynomial regression, it is specific to only 2 dimensions user and series. What if we want to introduce extra features that can be helpful in the recommendation like time, user attributes, series attributes? We can't include those in the two dimensional matrix allowing factorization. 

Factorization machines solve this problem by modeling the problem like a polynomial regression but learning latent factors for the interactions instead of the weights. So, the weight

## References
- [Factorization Machines](https://cseweb.ucsd.edu/classes/fa17/cse291-b/reading/Rendle2010FM.pdf) [pdf]


--- Paper reading notes ---
Factorization Machines (September 6, 2019)

Abstract:

Motivation:
- Parameter interaction capture, sparse data
- Drawback of other models: specific data, 
- Difference from collaborative: ALS, extra features hard to specify, 
- SVM can't work for sparse data

Introduction:
- Criticized SVM but haven't shown empirically

Advantage:
- SVM fail it works, also has to store support vector, FM doesn't have to
- Scalable: linear time complexity
- General predictors

Problem formulation:
- Figure
- To imporve upon matrix form, switched to feature vector approach to be able to add domain knowledge
- Normalized other movies in feature vector to indicate activity
- Equation (1) -> weight factorized into factors
- Why j=i+1 -> take above diagonal

Expressiveness:
- How to choose k: more sparse, lower 'k' gives dimension of v
- lower k -> limit expressiveness, more generalization

estimation under sparsity:


positive definite matrix: -> symmetric, 
- <vi, vj> -> figure for weights of polynomial vs FM
- 

Reducing complexity from O(kn**2) to O(p*k) with linear in k


O(k*n) this is not O(n**2) because k is constant, e.g. O(2*n) ~= O(n) so linear

Model:
- Each column -> converted to k size vector
- 

Error:
- Regression: MSE
- Binary classification: sign used and hinge/logit loss
- Ranking: sort by score of y(x)

Optimizer:
- SGD
Later: bayesian



- Future work:

# References
https://www.jefkine.com/recsys/2017/03/27/factorization-machines/
https://www.slideshare.net/SessionsEvents/steffen-rendle-research-scientist-google-at-mlconf-sf
---
title: "ISL"
permalink: /projects/ISL/CH8
---

# 7. Tree Based Methods

## VIDEO OUTLINE

[Lecture Slides](https://courses.edx.org/assets/courseware/v1/62c570de505d28b78e8e4ea932daddf2/asset-v1:StanfordOnline+STATSX0001+1T2020+type@asset+block/trees-handout.pdf)

### 8.1 Tree-based Methods

### 8.2 More details on Trees

- Bushy trees have high variance -- they are overfitting the data and likely not going to predict well

#### PRUNING:

- A good strategy is to build a large tree and PRUNE it back to obtain a SUBTREE
- Cost Complexity Pruning, aka weakest link pruning
  - Similar to LASSO in regression
  - We use Cross Validation to help us choose alpha

Cross Validation is what we use to help us prune our tree -- it will show us where our error is reduced (look at baseball example, and we can see the cv is lowest at 3) so we can tell our tree to have three terminal nodes.

### 8.3 Classification Trees

If response is a _categorical variable_, we call that a CLASSIFICATION TREE!!

#### How do we split?!

Binary (into two parts), recursively (meaning over and over until an end case is met)

#### What is the criteria for splitting?

We can't use RSS (like in regression), so we use classification error rate (which is just the fraction of the training data that does not match the classification criterion)

NEED TO VERIFY but if we have 8 cats and 1 turtle, our error rate would be 1/9 as we'd assume cats and we'd be wrong 1 out of the 9 times we were guessing which random household creature Colin was holding. (This is not including the fact that we hold Leo less because he is less "holdable" than a cat. Also, salmonella, apparently.)

Gini index: if it is small, one class is favored and the rest are all really small.

PROS OF DECISION TREES!

- Easy to understand by non subject matter experts
- Trees often mimic normal human decision making!
- Trees can easily handle categorical variables without having to use dummy variables

CONS OF DECISION TREES:

- Not great at predictability

![trees vs linear models](IISL_CH8_TREES.png "Trees")

#### QUIZ!

You have a bag of marbles with 64 red marbles and 36 blue marbles.

What is the value of the Gini Index for that bag? Give your answer to the nearest hundredth:

.64(1-.64) + .36(1-.36)

NOTE: I was close but forgot the plus :(

##### Gini Index = .64*(1-.64) + .36*(1-.36) = .4608

##### Cross Entropy = -.64*ln(.64) - .36*ln(.36) = .6534

BONUS!! I learned a little bit more about how to "read" the fun fancy equations. For every instance of thing, sum it up. That is what the episolon means and technically I knew this but I didn't KNOW this -- it meant nothing in the real world to me. So, if there is a minus sign before the episolon, it is `- (thing)- (thing)`

### 8.4 Bagging and Random Forests

#### BAGGING!!

Bagging stands for BOOSTRAP AGGREGATION.

Bootstrap + Aggregation = Bagging.

Bagging is basically averaging. It is used all across stats but we bring it up here as it is particularly useful in trees.

Bagging is the process of reducing variance by averaging a set of observations.

But, since we don't usually have many different samples, we take multiple samples of the same dataset -- this is called BOOTSTRAPPING -- we are faking our way to having "multiple" training datasets by simply resampling over and over

#### RANDOM FOREST!!

- Random Forest is an advanced form of bagging (which, to review, is just averaging a bunch of different iterations of experimentation)
- "Out of the bag" is a "free way" of doing LOOCV (leave one out Cross Validation)
- Wrapping up bagging -- we get LOO (Leave One Out) Cross-Validation for free!! Because when we are bootstrapping, we are leaving out 1/3 of the data... so we can get LOOCV "for free" by gathering all of the instance where our observation isn't in the training data and average THAT!

* Adding trees in Random Forest will never hurt you. At a certain point, it levels off and the "help" it gives you (a reduced error rate) stops increasing in helpfulness
* Random forest is slightly counter-intuitive in that it takes only SOME of the predictors. Specifically, the squareroot of the number of predictors -- so if we have 100 predictors, random forest chooses 10.

* What can we do with high dimensional data? We can remove some of the predictors with low variance. Not in comparison to one another (the other predictors), but in comparison to itself. Because we're looking at overall variance without regard to the label, it is not cheating.

#### QUIZ

Suppose we produce ten bootstrap samples from a data set containing red and green classes. We then apply a classification tree to each bootstrap sample and, for a specific value of X, produce 10 estimates of P(Class is Red|X):

0.1,0.15,0.2,0.2,0.55,0.6,0.6,0.65,0.7, and 0.75
There are two common ways to combine these results together into a single class prediction. One is the majority vote approach discussed in the notes. The second approach is to classify based on the average probability.

What is the final classification under the majority vote method?:

##### ANSWER: Red! (simply take the majority)

What is the final classification under the average probability method?:

##### ANSWER: Green! (simply take the average)

### 8.5 Boosting

Boosting is similar to bagging, except where bagging just independently creates a bunch of trees, BOOSTING is sequential, meaning it builds trees off of what it learns from previous trees.

---

#### QUIZ

In order to perform Boosting, we need to select 3 parameters: number of samples B, tree depth d, and step size 𝜆 .

How many parameters do we need to select in order to perform Random Forests?:

##### ANSWER: 2 -- To perform Random Forests we need to select 2 parameters: number of samples B and m= number of variables sampled at each split.

### 8.R -- Tree-Based methods in R

### Chapter 8 Quiz

Examine the plot on pg 23. Assume that we wanted to select a model using the one-standard-error rule on the Cross-Validated error. What tree size would end up being selected?:

Explanation

Cross-Validated error is minimized at tree size 3. The error for Tree size 2 is within one standard error of the minimum, but the error for tree size 1 is not. Thus, the one-standard-error rule selects tree size 2.

QUESTION: Suppose I have two qualitative predictor variables, each with three levels, and a quantitative response. I am considering fitting either a tree or an additive model. For the additive model, I will use a piecewise-constant function for each variable, with a separate constant for each level. Which model is capable of fitting a richer class of functions:

ANSWER: Tree

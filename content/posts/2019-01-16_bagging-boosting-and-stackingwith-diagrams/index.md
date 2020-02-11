---
title: "Bagging / Boosting and Stacking — with diagrams"
author: "Jordi Coscolla"
date: 2019-01-16T08:28:07.219Z
lastmod: 2020-02-11T21:51:05+01:00

description: ""

subtitle: "As you already know, the way to get the best results using Machine Learning is to use multiple models and combine them to create better…"

image: "/posts/2019-01-16_bagging-boosting-and-stackingwith-diagrams/images/1.jpeg" 
images:
 - "/posts/2019-01-16_bagging-boosting-and-stackingwith-diagrams/images/1.jpeg" 
 - "/posts/2019-01-16_bagging-boosting-and-stackingwith-diagrams/images/2.png" 
 - "/posts/2019-01-16_bagging-boosting-and-stackingwith-diagrams/images/3.png" 
 - "/posts/2019-01-16_bagging-boosting-and-stackingwith-diagrams/images/4.png" 


aliases:
    - "/bagging-boosting-and-stacking-with-diagrams-80fa3ef2af95"
---

As you already know, the way to get the best results using Machine Learning is to use multiple models and combine them to create better models that each single models alone.

Mainly there are three types of ways of combining them, but yeah… the names are just horrible and always lead to confusion… WTF does **Bagging** means? and yeah! sure I want to **Boost** my model but how?!




![image](/posts/2019-01-16_bagging-boosting-and-stackingwith-diagrams/images/1.jpeg)

I’m so confused!



Bagging and stacking are the ones that are easy to understand let’s go!

### Bagging

Is as easy as get multiple similar models, meaning normally the same models with slightly different hyper-parameters or use different parts of the data (bootstrapping), and average them at the end.

The rationale is that, since you are averaging different models, you are not just lucky to find a random seed that give a really nice score in validation, but that the validation score is generalized between all the models.

Also since you are lowering the possibilities to overfit, you can use more complex models and don’t overfit that much.



![image](/posts/2019-01-16_bagging-boosting-and-stackingwith-diagrams/images/2.png)

### Stacking

Stacking is just create a new dataset, with the values of your different models predictions. And then use a final model that get this dataset of predictions and creates the final one.

The idea is that if you got diversity in the individual models, since each one is capturing different patterns, we can leverage a final model that combines everything and knows that when a KNN and the NN predicts the same thing is probably correct but also, when they diverge maybe is a good idea to look a third prediction indicator.

Normally the model that combines the stacked dataset is a linear models since the patterns should already be captured in the individual models.



![image](/posts/2019-01-16_bagging-boosting-and-stackingwith-diagrams/images/3.png)

### **Boosting**

Boosting the technique was harder to understand… the idea is that you create different models depending on the how well the other the previous model performed.

For example, imagine you had a dataset and create a model that predicts the target variable… pretty normal so far you have your _model_1_… then you clone the dataset but change the target column with the error of the prediction of the _model_1_. So basically the model_2 have to predict how much error the did the first model.

In a way, if we can predict how much error a previous model did, we can **correct the previous values** and create a better prediction right.



![image](/posts/2019-01-16_bagging-boosting-and-stackingwith-diagrams/images/4.png)

Basically the final prediction is something like:

pred = model1_pred * 0.7 + model2_pred * 0. 25 + model3_pred * 0.05

### **Conclusion**

Ensembling is a powerful tool that can increase your model perfomance, and depending on issues in the model.

Your current model is really good but overfits → try to use **bagging**

None of your models captures the different kind of patterns in the data → use **stacking**

You want to have even more powerful models able to capture hidden patterns → go for **boosting**.

And don’t let the horrible naming stop from using this techniques most of them are already implemented in sklearn.

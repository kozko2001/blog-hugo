
---
title: Weight Decay
date: 2020-07-13
---


Weight decay is a way to make sure the models don't overfit, how? easy, for a model to overfit, it has to have crazy values in the model.... I mean if all the values were small it would be really hard to create weird folds in space. So what if in the loss function we add a new term, this term will be the **sum of all parameters in the model squared**! that will give an incentive to the NN to have small values in the model. the weight decay is a factor of this summ


loss L will became     L = old_loss +  weight_decay * (sum(model_parameters) ** 2)





---
title: Naive Bayes
date: 2020-08-11 00:00:00
---
---

### Naive Bayes


On Naive Bayes we estimate the probability for each class by using the joint probability of the words in classes. The Naive Bayes formula is just the ratio between these two  probabilities, the products of the priors and the likelihoods


Why is Naive Bayes, named naive? {{c1:: Cause it makes the assumption that features used for classification are independent }} {{id: 8783b050-b91d-4f7d-a1b7-48563a7b0695 }} [[FlashCard]]


Algorithm:
	-  Get the frequency of each word in each class `freq(word, class)`
	-  Also get the total number of words in each class `countWords(class)`
	-  Now we can calculate `P(class | word appeared)` as $$\frac {freq(word, class)} {countWords(class)}$$
	-  Now to infer what is the probability of a sentence being of a class or another we can
	-   $$\frac {P(positive)}{P(negative} \prod_{i}^{m} \frac {P(w_i  | positive)} {P(w_i | negative )}$$
	-  If the values is > 1, meaning that overall that the sentence is positive
	-  `prio` is $$\frac {P(positive)}{P(negative}$$ 
	-  `likelihood` is $$\prod_{i}^{m} \frac {P(w_i  | positive)} {P(w_i | negative )}$$ 


Log Likelihood
	-  Why we use Log Likelihood {{c1:: for numeric stability, preventing underflow }} {{id: 70f6e5af-a4af-448d-9849-a35707d7df74 }} [[FlashCard]]
	-   $$log(\frac {P(positive)}{P(negative} \prod_{i}^{m} \frac {P(w_i  | positive)} {P(w_i | negative )})$$
	-  how you can decompose $$log(a * b)$$ {{c1:: $$log(a) + log(b)$$}} {{id: b3a764f7-9a8d-422a-bad9-4da27f66a3be }} [[FlashCard]]


We can rewrite naive bayes using log likelihood as... $$log(\frac {P(positive)}{P(negative}) + log(\prod_{i}^{m} \frac {P(w_i  | positive)} {P(w_i | negative )})$$, Since now is the logarithm a sentence will be positive if log likelihood is > 0


Assumptions
	-  Naive Bayes assumes that features are independent, in NLP specifically means that there is no overlap of meaning in the words, which is not true. For example `It is sunny and hot today` sunny and hot are not independent, they appear often together. This can bias the probabilities.
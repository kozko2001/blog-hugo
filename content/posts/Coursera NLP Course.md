
---
title: Notes on NLP Course on Coursera
date: 2020-08-09 00:00:00
---
---

### Week 1:
* One easy way to convert a text to an array of numbers is by using a technique named {{c1:: Bag of Words}} which consist of {{c2:: converting every word in the vocabulary into an index, and then a sentence is 0 or 1 depending if the word exist }} {{id: 00094e21-2a39-459c-ba66-4dfdaa60eee9}} [[FlashCard]] 
* this is a sparse representation, for each tweet you will need a vector of size == your vocabulary
* with a lot of features equals to 0
* With an spare representation a logistic regression model will need to learn {{c1:: n+1}} parameters where n is the size of the vocabulary {{id: 42c5aae1-b1e1-4321-84f8-920c9d80175f }} [[FlashCard]]
* this is problematic for big vocabulary, becoming longer than need to train
* We can build a frequency table for each category (inn sentimental analysis is would be one for positive and one for negative). So basically count how many time each word appears in a positive tweet, and how many times a word appears in a negative tweet
* With a frequency table we can create a frequency representation of the tweet as {{c1:: [1 <- bias, sum of positive frequencies, sum of negative frequencies] }} {{id: 32681a27-db31-45e7-9853-148cb304f8a1 }} [[FlashCard]]
	* ![[./coursera nlp/FrequencyTable.png]]
* Preprocessing:
	* Eliminate [[Stop Words]] and punctuation characters.
 	* ![[Stemming]]
* ![[Logistic Regression- Cost]]

### Week 2: Naive Bayes


What P(A | B ) means?  {{c1:: frequency of happening A if we know that B already happened  }} {{id: b45287f1-2711-4bae-82f8-7afb8f9a7eff }} [[FlashCard]]


How do you express the probability of A, once we already now event B happened {{c1:: P(A | B)  }} {{id: ebcfb3d7-e93e-486b-a368-a99054df14d1 }} [[FlashCard]]


![[Bayes Rule]]
	-  how can you rewrite $$P(A | B)$$ using Bayes Rule? {{c1::  $$P(A | B) = P(B | A) * \frac {P(A)} {P(B)}$$ }} {{id: 531ecec2-509d-4d73-9799-a774d4f52a8a }} [[FlashCard]]


What does $$P(Positive | "happy")$$  mean? {{c1:: It means, probability of being of class "positive" given that it contains the word "happy"  }} {{id: abcfad02-0b85-4fa0-8b3c-ee9fd01cfa4e }} [[FlashCard]]



Naive Bayes
	-  Why is Naive Bayes, named naive? {{c1:: Cause it makes the assumption that features used for classification are independent }} {{id: 8783b050-b91d-4f7d-a1b7-48563a7b0695 }} [[FlashCard]]
	-  Get the frequency of each word in each class `freq(word, class)`
	-  Also get the total number of words in each class `countWords(class)`
	-  Now we can calculate `P(class | word appeared)` as $$\frac {freq(word, class)} {countWords(class)}$$
	-  Now to infer what is the probability of a sentence being of a class or another we can
	-   $$\frac {P(positive)}{P(negative} \prod_{i}^{m} \frac {P(w_i  | positive)} {P(w_i | negative )}$$
	-  If the values is > 1, meaning that overall that the sentence is positive
	-  `prio` is $$\frac {P(positive)}{P(negative}$$ 
	-  `likelihood` is $$\prod_{i}^{m} \frac {P(w_i  | positive)} {P(w_i | negative )}$$ 
	- Log Likelihood
		-  Why we use Log Likelihood {{c1:: for numeric stability, preventing underflow }} {{id: 70f6e5af-a4af-448d-9849-a35707d7df74 }} [[FlashCard]]
		-   $$log(\frac {P(positive)}{P(negative} \prod_{i}^{m} \frac {P(w_i  | positive)} {P(w_i | negative )})$$
		-  how you can decompose $$log(a * b)$$ {{c1:: $$log(a) + log(b)$$}} {{id: b3a764f7-9a8d-422a-bad9-4da27f66a3be }} [[FlashCard]]
	-  We can rewrite naive bayes using log likelihood as... $$log(\frac {P(positive)}{P(negative}) + log(\prod_{i}^{m} \frac {P(w_i  | positive)} {P(w_i | negative )})$$, Since now is the logarithm a sentence will be positive if log likelihood is > 0
	-  
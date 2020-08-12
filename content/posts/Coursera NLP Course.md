
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



![[Naive Bayes]]

### Week 3: Vector spaces


---
title: Notes on NLP Course on Coursera
date: 2020-08-09 00:00:00
---
---

### Week 1:
* One easy way to convert a text to an array of numbers is by using a technique named Bag of Words which consist of converting every word in the vocabulary into an index, and then a sentence is 0 or 1 depending if the word exist   
* this is a sparse representation, for each tweet you will need a vector of size == your vocabulary
* with a lot of features equals to 0
* With an spare representation a logistic regression model will need to learn n+1 parameters where n is the size of the vocabulary  
* this is problematic for big vocabulary, becoming longer than need to train
* We can build a frequency table for each category (inn sentimental analysis is would be one for positive and one for negative). So basically count how many time each word appears in a positive tweet, and how many times a word appears in a negative tweet
* With a frequency table we can create a frequency representation of the tweet as [1 <- bias, sum of positive frequencies, sum of negative frequencies]  
	* ![](.././images/FrequencyTable.png)
* Preprocessing:
	* Eliminate [[Stop Words]] and punctuation characters.
 	* ![[Stemming]]
* ![[Logistic Regression- Cost]]

### Week 2: Naive Bayes


What P(A | B ) means?  frequency of happening A if we know that B already happened  


How do you express the probability of A, once we already now event B happened P(A | B)  


![[Bayes Rule]]
	-  how can you rewrite $$P(A | B)$$ using Bayes Rule? $$P(A | B) = P(B | A) * \frac {P(A)} {P(B)}$$  


What does $$P(Positive | "happy")$$  mean? It means, probability of being of class "positive" given that it contains the word "happy"  



![[Naive Bayes]]

### Week 3: Vector spaces
 - How you calculate the vector norm (euclidean distance) in numpy? `np.linalg.norm(a - b)`  
 


What is the problem of using euclidean distance for word vector representation? depending on number of occurrence of the words, the distance can be different and what we can use to overcome this problem? Cosine similarity  
 


![](.././images/Screenshot 2020-08-12 at 11.33.22.png)
 
 ![[Cosine Similarity]]
 
 ![[Eigenvector]]

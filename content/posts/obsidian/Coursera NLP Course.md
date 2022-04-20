
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
	* ![](<../images/FrequencyTable.png>)
* Preprocessing:
	* Eliminate [Stop Words](../stop-words) and punctuation characters.
 	* 
* 

### Week 2: Naive Bayes
-  What P(A | B ) means?  frequency of happening A if we know that B already happened  
-   How do you express the probability of A, once we already now event B happened P(A | B)  
- 
	-  how can you rewrite $$P(A | B)$$ using Bayes Rule? $$P(A | B) = P(B | A) * \frac {P(A)} {P(B)}$$  
-  What does $$P(Positive | "happy")$$  mean? It means, probability of being of class "positive" given that it contains the word "happy"  

- > 

> ---

> title: Naive Bayes

> date: 2020-08-11 00:00:00

> ---

> ---

> 

> - On Naive Bayes we estimate the probability for each class by using the joint probability of the words in classes. The Naive Bayes formula is just the ratio between these two  probabilities, the products of the priors and the likelihoods

> -  Why is Naive Bayes, named naive? Cause it makes the assumption that features used for classification are independent  

> -  Algorithm:

> 	-  Get the frequency of each word in each class `freq(word, class)`

> 	-  Also get the total number of words in each class `countWords(class)`

> 	-  Now we can calculate `P(class | word appeared)` as $$\frac {freq(word, class)} {countWords(class)}$$

> 	-  Now to infer what is the probability of a sentence being of a class or another we can

> 	-   $$\frac {P(positive)}{P(negative} \prod_{i}^{m} \frac {P(w_i  | positive)} {P(w_i | negative )}$$

> 	-  If the values is > 1, meaning that overall that the sentence is positive

> 	-  `prio` is $$\frac {P(positive)}{P(negative}$$ 

> 	-  `likelihood` is $$\prod_{i}^{m} \frac {P(w_i  | positive)} {P(w_i | negative )}$$ 

> - Log Likelihood

> 	-  Why we use Log Likelihood for numeric stability, preventing underflow  

> 	-   $$log(\frac {P(positive)}{P(negative} \prod_{i}^{m} \frac {P(w_i  | positive)} {P(w_i | negative )})$$

> 	-  how you can decompose $$log(a * b)$$ $$log(a) + log(b)$$  

> -  We can rewrite naive bayes using log likelihood as... $$log(\frac {P(positive)}{P(negative}) + log(\prod_{i}^{m} \frac {P(w_i  | positive)} {P(w_i | negative )})$$, Since now is the logarithm a sentence will be positive if log likelihood is > 0

> -  Assumptions

> 	-  Naive Bayes assumes that features are independent, in NLP specifically means that there is no overlap of meaning in the words, which is not true. For example `It is sunny and hot today` sunny and hot are not independent, they appear often together. This can bias the probabilities.

### Week 3: Vector spaces
 - How you calculate the vector norm (euclidean distance) in numpy? `np.linalg.norm(a - b)`  
 
- What is the problem of using euclidean distance for word vector representation? depending on number of occurrence of the words, the distance can be different and what we can use to overcome this problem? Cosine similarity  
 
- ![](<../images/Screenshot 2020-08-12 at 11.33.22.png>)
 
 > 

> ---

> title: Cosine Similarity

> date: 2020-08-12 00:00:00

> ---

> ---

> -What is cosine similarity? is a metric to compare two vectors depending on the inner angle, and that way, it's not affected for the size of the vector  

> 

> 

> Cosine of two vectors is: $$cos(Beta) = \frac {\vec(v) * \vec(w)} {\|\vec(v)\| * \|\vec{w}\|} $$  

> 

> 

> if the angle is orthogonal, the cos of 90 is 0, meaning if the cosine similarity is 0, means that the vectors are orthogonal, meaning that the similarity is 0.

 
 > 

> ---

> title: None

> date: 2020-08-13 00:00:00

> ---

> ---

> 

>  What is an eigenvector? Eigenvectors is a decomposition of a matrix, where we multiply the matrix by a vector, and the result is the same vector multiplied by an scalar $$A*\vec{v} = \lambda * \vec{v}$$  

>  

>  What is the geometric explanation of eigenvectors? it will tell you, which directions while not change when using the transformation matrix `A`, the eigenvectors will not change direction, they will only stretch by the factor of the eigenvalue ($$ \lambda $$)  




---
title: Mutation Testing
date: 2020-08-21 00:00:00
---
---

Mutation testing is a technique to know how well your tests are saving you from deploying mistakes. The goal is very similar to [Code Coverage](../code-coverage), to have a metric that guide us to know how confident we can be with our code.

They differ in the way you define the metric


in [Code Coverage](../code-coverage) you execute the tests, and check which statements where executed during the test suite execution


in Mutation testing, the library is going to execute the tests multiple times, but slightly changing the code. 

If changing the code (possible bug) does not trigger test failure, we say the mutation survived. The metric is the number of mutations that survived.

I never tried to use this, but really eager to test how it works!

#### references


https://hackernoon.com/mutmut-a-python-mutation-testing-system-9b9639356c78


https://codeascraft.com/2020/08/17/mutation-testing-a-tale-of-two-suites/

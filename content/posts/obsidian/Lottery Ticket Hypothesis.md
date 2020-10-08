
---
title: Lottery Ticket Hypothesis
date: 2020-08-24 00:00:00
---
---

The lottery ticket hypothesis says:

> A randomly initialized, dense neural network contains a sub-network that is initialized such that, when trained in isolation, can match the test accuracy of  the original network after training for at most the same number of iterations.

This hypothesis can be used for [Network pruning](../network-pruning), by doing the following.

1. Train the big network
2. Detect the sub-network of the lottery ticket, we can do that by pruning, once pruned we will have a smaller network but our accuracy would have also decreased
3. Get the random initialized values for the subnetwork.
4. Train again, this time only the subnetwork, but it's important, with the same random values the big one had.
5. Voila! you have a smaller network that has an accuracy similar to the first one.


You can check the https://www.youtube.com/watch?v=LXm_6eq0Cs4 for more information.


### Conclusions:
- Initialization plays a key role in Neural networks
- 
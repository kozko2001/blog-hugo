
---
title: Circuit break
date: 2020-09-08 00:00:00
---
---

When working on micro services, you do some remote calls as if they were in your code base. This has benefits, but if the service is not available, it can throw an error cascade in your service

Circuit breaks is a way to mitigate this, the iddea is very simple, if a service is not available on a threshold, you open the circuit break. 

In the open circuit, you always execute a piece of code that doesn't depend on the service. That could be an exception saying the service is not available. 

After a while you move to the half open state. Basically trying a request to go through the real service. if the service is available again, great we close the circuit and the system is working. if not we move to the open circuit state.

![](<../images/circuit-break.png>)

The benefit we get, is to limit the damage that a single service down could lead to the whole system down.


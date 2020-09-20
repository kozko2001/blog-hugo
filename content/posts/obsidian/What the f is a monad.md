
---
title: What the f is a monad
date: 2020-09-20 00:00:00
---
---

#### What is a functor

Given that you have a normal function **f** that convert a type **A** to a type **B**

```
f :: A -> B
```

and some kind of wrapper, T. a functor have to be able to go from **T[A]** to **T[B]** given **f :: A - > B**.

so basically it allows you to apply normal functions to wrapped objects.

This operation is named **map**, is the lift operator.

For example Option is a functor (well is a monad as well...), you can use map to apply transformations to an already existing optional, as if it was not an optional.

```
Optional<Int> initialvalue = Optional(0);

def isEven(Int a) = a % 2 == 0

init.map(isEven)
```

```
f :: A -> B
map :: (A -> B) -> F[A] -> F[B]
map(f) :: F[A] -> F[B]
```

### What is a monad




Reference: https://www.youtube.com/watch?v=OSuu8zBBNAA
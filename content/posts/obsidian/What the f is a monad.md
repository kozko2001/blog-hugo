
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

Monads are similar, but **f** instead of converting from **A** to **B**, f converts from **A** to **M[B]**, M being a generic wrapper

```
f :: A -> M[B]
```

given that we have f, we want to be able to transform from **M[A]** to **M[B]**. if we have a Functor and apply it will happen is:

```
map ::  (A -> B) -> M[A] -> M[B]

map(f) :: M[A] -> M[M[B]]
```

but we don't want `M[M[B]]` we want `M[B]`. so we need a new function `flatten` that converts `M[M[_]]` to `M[_]`

normally we use the flatmap function, which does the map of the functor and then the flatten.

Finally, a monad needs also to be able to wrap the object so `Option(0)` which in haskell is named `return` function

```Mondad = Functor + flatmap /bind + return```

Why is the monad useful? it allow us to compose functions.

Reference: https://www.youtube.com/watch?v=OSuu8zBBNAA

### Questions!
Which is the type of a Functor Map? `f :: (a -> b) -> T[A] -> T[B]`  

When to use Functors?  When we don't need to extend the type, for example in option, when we have to work with an option, but we don't have any possible error computation  


What functions a Monad need ? flatten, map and result  
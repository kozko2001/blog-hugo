
---
title: Referential transparency
date: 2020-09-24 00:00:00
---
---

means I can substitute variables, by their definition and the program is still the same.

we can compare the following two programs

```
const a = 2
const b = 3


cosnt sum = (a, b) => a + b

const result = sum(a, b)
```

and, if we substitute everything with the definition...

```
const result = 2 + 3
```

and they are equivalent, in this case referential transparency exist, but what if the function has an effect?

```

const sum = (a, b) => a + b;

const n = Math.random();

const result = sum(n, n)
```

and, if we substitute....

```
const result = Math.random() + Math.random()
```

Now the program are not equivalent, why? Cause `Math.random()` is not a pure function.

A pure function, given the same input, always return the same output. 

::: anki 07e9ef6e-180a-445b-a8f8-cb277f8decd3
What is referential transparency? means I can substitute variables, by their definition and the program is still the same. #Flashcard
:::
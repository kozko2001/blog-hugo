
---
title: GraalVM
date: 2020-08-10 00:00:00
---
---

## GraalVM

GraalVM is an alternative to the JVM (but is not a runtime), but with special thought for performance and polyglot.

When executing java in the JVM, you can tweak the the JAVA_PATH dynamically, this way the java compiler can not apply the optimization and tricks that compiled languages can do (GCC, LLVM)

GraalVM actually is more like a java compiler, compiles the java code to binary, jumping the step of bytecode. You lose the compile once, run everywhere. but you have a lot more performance.

How does GraalVM achieve more performance than the JVM removing the linker phase in runtime (JAVA_PATH) and jumping the step of bytecode. This wayit can apply good optimization at the expense of {{c2: Loosing some reflection capabilities and the compile once and run everywhere}}  

GraalVM also improves the interoperability between java and other languages, like javascript,  python or ruby.  Using An abstract syntax tree interpreter called Truffle. Which allows you to easily implement languages on top of GraalVM. With the performance of compiled languages but using an interpreter.

 What is Truffle is an abstract syntax tree interpreter that allow to build frontend for GraalVM  

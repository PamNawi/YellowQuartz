---
tags:
  - ConstraintProgramming
  - ProceduralGeneration
  - ComputerScience
---
Constraint programming is a way of instructing computers, you enter  rigorously defined problem, and then the compute uses built in algorithms to find the solution.

**Variables:** A unknown value that we want to find a solution for. 
**Domain:** A set of values that it's possible for each variable to take.
**Constraint:** Rules that relate variables together.

Its common for constraint programming languages have a pre-existing constraint function call "all_distinct(..)", which requires that the variables passed in have to be distinct.

**Constraint propagation:** A information propagates from one variable to another via constraints.
The objective is to discover if a variable <mark style="background: #FFB8EBA6;">must</mark> be some value from the domain and use the new information discovered to infers recursively more variables values.

In more complex problems is common that, at some point on the problem solving, that no variable can have their value determined and they have more than 1 possible final result. If it was a human doing some deduction is common to try have do have more increasingly sophisticated logical inferences, but <mark style="background: #FFF3A3A6;">computers can just be dumb and guess the solution</mark>. They randomly pick a possible solution for any open variable and try to continue to find the solution. If the solution is valid, all the variables have a valid outcome, it finished. If not, the algorithm does a backtrack where he did the guessing, removes the guessing value as a possible solution and try again.

Every time that the algorithm does a backtrack, it reduces the domain for at least one variable, so if there's a solution, eventually will be terminating.

# References
- [Boris the brave - Wave Function Collapse Explained](https://www.boristhebrave.com/2020/04/13/wave-function-collapse-explained/)
- There's a open source library on GitHub that can be used for this: [DeBroglie](https://github.com/BorisTheBrave/DeBroglie)
- On Unity we can use Tessera: [Tessera](https://assetstore.unity.com/packages/tools/level-design/tessera-procedural-tile-based-generator-155425)


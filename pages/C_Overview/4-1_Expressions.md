---
title: "Expressions in C"
keywords:
tags:
sidebar: C_Overview_sidebar
permalink: C_4-1_Expressions
summary:
---

### Expression Statements
- Expressions in C can be used as standalone statements.
- Example : ```i--;```

### Arithmetic Operators
- Arithmetic operators are quite straightforward : ```+, -, *, /, %```, which represent addition, substraction, multiplication, division, and remainder respectively.

### Assignment Operators
- The assignment operator is ```=``` in C.
- Several assignments can be chained together : ``` i = j = k = 0```, although it might lead to issues, especially if the variables being assigned are of different type.
- Example of a compound assignment : ```i = i+ 2```.

### Increment and Decrement Operators
- Considering that two of the common operations on a variable are incrementing and decrementing, it is possible to perform these tasks using specific operators.
- Example of Increment Operator : ```i += 1```
- Example of Decrement Operator : ```i -= 1```
- It is also important to know the differencebetween the **postfix** and the **prefix** operators (```i++/i--``` vs ```++i/--i```).
- There are also variant which allow us to multiply or divide values by a certain constant/variable : ```i *= 1``` or ```i /= 1```

### Expression Evaluation
Here's a complete table to understand the order of precedence with all operators in C :

| Precedence | Operator Symbol |
| -----------  |  ---------------- |
| 1 | (postfix) ++, -- |
| 2 | (prefix) ++, -- |
| 3 | \*, /, % |
| 4 | +, - |
| 5 | =, \*=, /=, %=, +=, -= |

### Implementation-Defined Behavior

- The C standard deliberately leaves parts of the language unspecified, leaving the compiler to 'implement' these unspecified parts. This leads to some differences from one machine to another. It is best to avoid implementation-defined behaviour, but it is sometimes not possible if we want to build the fastest possible programs for specific hardware.

### Undefined Behaviour

- When have complex operation using all types of operators, we risk having undefined behavior. Undefined behavior might cause the program to act erratically, produce different output from a machine to another, or completely crash. All cases of undefined behavior should be avoided at all cost.

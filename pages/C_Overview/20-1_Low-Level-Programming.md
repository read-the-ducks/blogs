---
title: "Low-Level Programming in C"
keywords:
tags:
sidebar: C_Overview_sidebar
permalink: C_20-1_Low-Level-Programming
summary:
---

Some programs require us to perform operations at the bit level, which are possible thanks to C's support for bit level operations.

### Bitwise Operators
- C provides six bitwise operators, which are summarized in the following table :

| Symbol | Meaning |
| --- | --- |
| ```<<``` | Left shift |
| ```>>``` | Right shift |
| ```~``` | Bitwise complement |
| ```&``` | Bitwise 'and' |
| ```^``` | Bitwise 'exclusive or' |
| ```|``` | Bitwise 'inclusive or' |

### Bit-Fields in Structures
- We can use Structures whose members represent bit-fields. Each member can be assigned a specific number of bits. It's better to declare these members as unsigned integers because some machines might misinterpret integers with the sign bit cut off. Example in code :

```c
struct date {
    unsigned int day: 5;
    unsigned int month : 4;
    unsigned int year : 7;
}
```

### Other Low-Level Techniques
- Using the **volatile** keyword lets you specify that a variable is volatile (i.e. variable stored at a certain address might be modified by external factors), and must be fetched from memory every time its needed.
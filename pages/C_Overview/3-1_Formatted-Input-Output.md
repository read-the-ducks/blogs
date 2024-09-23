---
title: "Formatted Input & Output in C"
keywords:
tags:
sidebar: C_Overview_sidebar
permalink: C_3-1_Formatted-Input-Output
summary:
---

### Using the printf statement
- ```printf``` allows us to print formatted output to standard output or *stdout*. 
- If we'd like to print out a variable using printf, we must have a conversion specification, which tells our program how the value shoulld be converted from its internal form (binary) to printed form (characters). Conversion Specification usually begins with the *%* character. A more complete definition of the conversion specification is *%m.pX*. *m* is the **minimum field width**, which specifies the minimum number of characters to print, *p* is the precision, whose meaning varies from a type to another, and *X* is the conversion specifier, which indicates which conversion should be applied for the value before it is printed.
- ```printf``` can used to print text (e.g ```printf("Hello World")```), to print integer variables (e.g. ```printf("%d", myInt)```), to print floating-point numbers in exponential format (e.g. ```printf("%e", myFloatingExponentialFormat)```), to print floating-point numbers in 'fixed decimal' format (e.g. ```printf("%f", myFloatingFixedDecimal)```), to print character variables (e.g. ```printf("%c", myChar)```), to print float variables (e.g. ```printf("%f", myFloat)```), to print string variables (e.g. ```printf("%s", myString)```), to print double variables (e.g. ```printf("%lf", myDouble)```), to print hexadecimal variables (e.g. ```printf("%x", myHex)```),  to print unsigned variables (e.g. ```printf("%u", myUnsigned)```), and to print octal variables (e.g. ```printf("%o", myOctal)```).
- We can print out multiple variables using a single ```printf``` call : ```printf("i = %d, j = %d", i, j)```. Be aware that the C compilers do not check that the number of specifications in string format matches the number of variables we want to print.
- A set of escape sequences can also be used with ```printf()```. These include the Alert ```\a```, the backspace ```\b```, the new line ```\n```, and the horizontal tab ```\t```. To print a backslash character, you must write two consecutive backslashes to avoid it being picked up as the beginning of an escape sequence. Same idea with percent symbols.


### Using the scanf statement
- ```scanf``` allows us to take user input in a formatted manner from the standard input or *stdin*. User input is not read directly by the program, but rather stored in a hidden buffer to which scanf has access.
- It can used to input integer variables (e.g. ```scanf("%d", &myInt)```), to input character variables (e.g. ```scanf("%c", &myChar)```), to input float variables (e.g. ```scanf("%f", &myFloat)```), to input string variables (e.g. ```scanf("%s", &myString)```), to input double variables (e.g. ```scanf("%lf", &myDouble)```), to input hexadecimal variables (e.g. ```scanf("%x", &myHex)```),  to input unsigned variables (e.g. ```scanf("%u", &myUnsigned)```), and to input octal variables (e.g. ```scanf("%o", &myOctal)```)..
- We can let the user input multiple variables using a single ```scanf``` call : ```scanf("%d%d%f%f", &i, &j, &x, &y)```
- Integers in base 10 are matched using the conversion specification *%d*, while integers in base 8 are matched using conversion specification *%i*. *%i* can also be used to read hexadecimal values.
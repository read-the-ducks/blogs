---
title: "The C-Standard Library"
keywords:
tags:
sidebar: C_Overview_sidebar
permalink: C_21-1_C-Standard-Library
summary:
---

- The standard *C89* standard library is divided into 15 parts, with the standard *C99* adding 9 additional parts.
### Using the Library
- Files that include the standard header must obey a set of rules : (1) They cannot use the names of macros defined in the header for any other purpose, (2) library names with file scope cannot be redefined at the file level, (3) Identifiers that begin with an underscore followed by an upper-case letter or a second underscore are reserved for use within the library, (4) Identifiers that begin with an underscore are reserved for use as identifiers and tags with file scope, (5) Every identifier with external linkage in the standard library is reserved for use as an identifier with external linkage. Failing to abide by these rule leads to portability issues.
### C89 & C99 Standard Library Overview

| Library Reference | Name |
|-------------------|--------------|
| ```assert.h``` | Diagnostics |
| ```ctype.h``` | Character Handling |
| ```errno.h``` | Errors |
| ```float.h``` | Characteristics of Floating Types |
| ```limits.h``` | Sizes of Integer Types |
| ```locale.h``` | Localization |
| ```math.h``` | Mathematics |
| ```setjmp.h``` | Nonlocal Jumps |
| ```signal.h``` | Signal Handling |
| ```stdarg.h``` | Variable Arguments |
| ```stddef.h``` | Common Definitions |
| ```stdio.h``` | Input/Output |
| ```stdlib.h``` | General Utilities |
| ```string.h``` | String Handling |
| ```time.h``` | Date and Time |
| ```complex.h``` | Complex Arithmetic |
| ```fenv.h``` | Floating-Point Environment |
| ```inttypes.h``` | Format Conversion of Integer Types |
| ```iso646.h``` | Alternative Spellings |
| ```stdbool.h``` | Boolean Type and Values |
| ```stdint.h``` | Integer Types |
| ```tgmath.h``` | Type-Generic Math |
| ```wchar.h``` | Extended Multibyte and Wide Character Utilities |
| ```wctype.h``` | Wide Character Classification and Mapping Utilities |
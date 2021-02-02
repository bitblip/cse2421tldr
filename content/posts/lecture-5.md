---
title: "Lecture 5"
date: 2020-01-19T02:30:11-05:00
description : "C part 2"
tags: ["precedence", "c"]
---

# Lecture 5
**Video** : [C Part 2 Op Precedence](https://urldefense.com/v3/__https:/osu.zoom.us/rec/share/TOseZgZqF0qNFydNS0PBvNqIPif4TZqJmi7rb58xYdshMGCTy00HWibGQ-33hScO.quk08hSkuRVRr366__;!!KGKeukY!kJb8MKc4ohhqGJkrNc_CmcB9dCidl_gvd28-UKnKM-qjBs8Le2FFIUHN-CRTcJc5$)

**Slides** : [C Part 2 Op Precedence](https://osu.instructure.com/courses/95904/files/folder/Zoom%20classes?preview=28650848)

# Lvalue
Must be modifiable. Represents a register/memory location.

# Rvalue
Constants, expressions, return value from a function, etc.

# Operator
Operators operate on operands. Operands are expressions that have a type and have return a value that is a type.

## Precedence and Associativity (P&A)
Between two operators, which takes precedence. Binary relation, defined relative to two adjacent operators. When two operators have equal precedence, associativity and left/right order. ()s can override precedence and associativity.

## Associativity of `/`
Left to right (LR) associativity. Common to binary mathematical operators.

Suppose a=1, b=3, and c-5.
``` c
d = ++a * c + b++;
```

Choose the highet binary precdence first. Evaluating left hand expression first, then right. Unary expressions are done only when necessary.

Parenthesize unary operators
``` c
d = (++a) * c + (b++);
```

Mathematic precedence
``` c
d = ((++a) * c) + (b++);
```

## Prefix
`++a` increments, then returns.

$$ Postfix
`b++` increments, but returns the pre-increment value.

Finally we have.
``` c
d = (2 * 5) + 3;
```

## Assignment Operator
Assignments are expressions. The value is the rightmost expression. Do not say "equals", instead say "is assigned". `==` is read "equals".

This expression is evaluated as 1.
``` c
a = b = 1;
```

> Warning, cgg will not warn about the misuse of `=` in a logical expression, `==`.
---
title: "Text: Pointers On C (4_C_Part_1)"
date: 2020-01-19T03:30:11-05:00
description : "Chapter 5 through 5.1.3; 5.3 to end of chapter"
tags: ["operators", "c"]
---

# Assignment
Read chapter 5 through 5.1.3; 5.3 to end of chapter

# Operators and Expressions
C has numerous operators, many unavailable in other languages.

## Arithmetic
`+` `-` `*` `/` `%`

Work one floating-pont and integers types, except `%`.

`/` truncates when both operands are integers, floating-point otherwise..

`%` divides the left integer operand by the right integer operand and returns the remainder.


## Shifting
Slide the bits in a value left or right. The number of shifts is specified by the argument following the operator.

``` c
a << 5;
```

### Left Shift
`<<` The left most bits is discarded and a zero is placed into the right most bit.

### Right Shift
Two kinds of right shifts that differ for negative values.

**logical shift** The right most bit is discarded and a zero is placed into the left most bit.

**arithmetic shift** The right most bit is discarded and the sign bit is placed into the left most bit.

 > No standard for shifts using signed values, maybe be **logical** or **arithmetic**. No guarantees across compilers. Thus, `a << -5` is inherently non-portable.

 ## Bitwise
 Logical AND `&`, OR `|`, and XOR `^` (exclusive-OR) operations. Bitwise operands are integers and are compared one pair of bits at a time.

 `&` returns one if both operands are one, zero otherwise.

 `|` returns zero if both operands are zero, one otherwise.

 `^` returns one if both operands are different, zero otherwise.

 ``` c
 00101110 & 01011011 /* 00001010 */
 00101110 | 01011011 /* 01111111 */
 00101110 ^ 01011011 /* 01110101 */
 ```

 ## Bit Manipulation
 Set the specified bit to one
``` c
value = value | 1 << bit_number;
```

Tests the specified bit and is nonzero if the bit is set.
``` c
value & 1 << bit_number
```

# L-values and R-values
**L-value** is something that can appear on the left side of an `=` sign and **R-values** appear on the right.

# Expression Evaluation
The order of expression evaluation depends on precedence, associativity, and type conversion.

## Implicit Type Conversion
Integer arithmetic at least defaults to the default, `integer`. `char` and `short` are converted to `integer`.

## Arithmetic Conversion
Operands of different types must be converted to the same type. The operand who's type is lower in this list is converted to the higher type.

- `long double`
- `double`
- `float`
- `unsigned long int`
- `unsigned int`
- `int`

## Precedence and Order of Evaluation
> The order of evaluation of two adjacent operators is determined by their precedence. If they have the same precedence, the order is determined by their associativity. Otherwise, the compile is free to evaluate expressions in any order that does not violate the order of evaluation imposed by parenthesis or by the comma, `&&`, `||`, or `?:` operators.
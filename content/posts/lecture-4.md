---
title: "Lecture 4"
date: 2020-01-19T02:30:11-05:00
description : "C part 1"
tags: ["build", "c"]
---

# Lecture 4
**Video** : [C Part 1](https://urldefense.com/v3/__https:/osu.zoom.us/rec/share/Jj2iU3dMQcLFDfLXr4Z51XlWgMRZov_ziixoHpSon7D0rBmNsVZCUF4_iJa_F5_-.X8OlDXjS_OoEfRVW__;!!KGKeukY!isQP2wVmp9bUuofGZ9Mj-jmnROV7FIZejaUehGHaTN3c6IStDzp6oN9lsXQVKElk$)

**Slides** : [C Part 1](https://osu.instructure.com/courses/95904/files/folder/Zoom_Lectures/Class%20slides?preview=28361906)

# Compilation
The way c programs are built.

- Source file
  - $ `gcc -o hello hello.c`
- Preprocessor
  - Collects `.c` and `.h` into `.i` file.
- Compiler
  - Converts `.i` file into assembly language file `.s`.
- Assembler
  - Converts `.s` into object file `.o`. Encoded instruction and data bit strings. Contains unresolved symbols. 
- Link Editor
  - Resolves unresolved symbols. e.g. `printf()`. Creates c executable file specified by `-o` argument **"hello"** or `a.out` (default name).
- Run program
  - $ `hello`

> `printf()` remains resolved by the assembler to prevent assembling the same object multiple times.

# Basic Data Types
Only Integer and Floating Point are define. Same as available to the machine. Variable sizes can vary by system but are listed in strictly increasing size.

- Integer Types
  - `char` (1 byte)
  - `short` (2 bytes)
  - `int` (4 bytes) (default)
  - `long` (8 bytes)
  - `long long` (8 or 16 bytes) (>= C99)

- Floating Point Types
  - `float` (4 bytes)
  - `double` (8 bytes) (default)
  - `long double` (16 bytes) (>= C99)

> Only char is guaranteed to always be one byte, Others can vary by system.

|type|example|
|---|---|
|char|`'A'` `'B'`|
|int|`123` `-1` `15348564158` `040` `0xab`|
|unsigned int|`123u` `2107433648` `040U` `0X02`|
|long|`123L` `0x1FFFl`|
|unsigned long|`123ul` `0777UL`|
|float|`1.23F` `3.15e+0f`|
|double|`1.23` `2.718281828`|
|long double|`1.23L` `9.99E-9L`|

## Derived Types
Potentially infinite kinds of derived types built from Integer and Floating Point types.

- `arrays`
- `pointers`
- `structures` - sequence of various objects, variables, and or derived types 
- `unions` - not sure about this one

## Constants
Defined with keyword `const`. Limited variable that can only be assigned once where variable assignment is allowed.


``` c
float const PI = 3.141593f; /*double is default, use f for float*/
const float PI = 3.141593f;
```

### Symbolic Constants
A name that substitutes for a value that cannot be changed. Convent is all upper case.

``` c
#define PI 3.141593
#define AREA (PI*r*r)
#define TRUE 1
```

## Variable Declarations
Valid identifiers are a-z, A-Z, 0-9, _. Beginning with _ is conventionally for system variables. Camel case is acceptable, historically _ word separators were used. Be consistent. Only 32 character identifiers are guaranteed to be supported, longer identifiers may be truncated.

You can declare and assign multiple variables in the same statement.
``` c
int i,j = 5,k;
char code, category;
int i = 123;
```

> Be consistent, be consistent, be consistent

## Type conversion
Explicit cast with (type). Avoid casting large types to smaller types. See Basic Data Types for size ordering.

``` c
int i = 65;
char ch = (char)i; /* ch = "A" */
```

> Use descriptive variable names that imply types and purpose. C is already demanding enough to code without adding ambiguous variable names. e.g. i, j, ch.

# Keywords
The follow are reserved identifiers that cannot be used as identifiers.

||
|---|---|---|---|
|auto|double|int|struct|
|break|else|long|switch|
|case|enum|register|typedef|
|char|extern|return|union|
|const|float|short|unsigned|
|continue|for|signed|void|
|default|goto|sizeof|volatile|
|do|if|static|while|

## Assignment
**Read** : Pointers on C, Chapter 5 through 5.1.3 and 5.3 to the end of the chapter.

**Read** : Computer Systems, Chapter 1 through 1.3.
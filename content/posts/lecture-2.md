---
title: "Lecture 2"
date: 2020-01-14T02:30:11-05:00
description : "Intro To C"
tags: ["static", "dynamic", "c"]
---

# Intro To C
**Video** : [Intro To C](https://urldefense.com/v3/__https:/osu.zoom.us/rec/share/ws3bspK8yzMjb-NlMEJDh6LZNb4tdm657bvCIxvqgnuMkFI3nMboYtQgb76x3JXC.LZQ9m3T8JMKWAHTQ__;!!KGKeukY!lMqjUxTjampWIGtCQnFftnubkj4mz4mC2FcdUJ3Nqh_IpkUxvXU-0055zai5l00L$)

**Slides** : [Intro To C](https://osu.instructure.com/courses/95904/files/folder/Zoom_Lectures/Class%20slides?preview=28368861)

C is **procedural**, compiles to machine code that runs directly on the hardware. Direct manipulation of memory, no garbage collection. Memory leaks occur when memory is mismanaged.

RAM is finite. 64 bit address spaces,  use 42 bits, 2^42 bytes (~4TB) of max RAM.

## C does NOT
- Classes/Objects (n the OOP sense)
- Encapsulation
- Inheritance
- Not object oriented

Features *ARE* approximated by writing code in a disciplined way.

## ANSI C
Standardized in 1989. Also known as C89, C90, "Standard C"

## Dynamic *(run time)*
- Dynamic memory
- Dynamic error

Error that occur at **run time** are `semantic errors`

## Static *(compile time)*
- Static error
- Static identifier class

Errors that occur at **compile time** are `syntax errors`

## Categories of computer languages
- Declarations
- Data Movement
- Arithmetic/Logical Operations (ALU)
- Control-Flow

## Hello World
``` C
#include <stdio.h>
#include <stdlib.h>

int main() {
    printf("Hello, World!\n");
    printf(EXIT_SUCCESS);
}
```

### Preprocessor
Prepares a C source code file for compilation. Strips **comments**, replaces preprocessor directives with contents of **header** file, replace MACROs.

Preprocessor directives begin with a **#** character, `#include <stdio.h>`. First step when compiling, e.g. `gcc`.

Outputs a <filename>.i file.

### Headers
Library file on disk. Often define **function prototypes**. Header files do not contain code for functions, only prototypes.

Standard includes such at `stdio.h` are found in `/usr/include/

### Comments
Must be of the form `/**/`, `//` not permitted.

### Macros
Fragments of code defined in source or header file. `EXIT_SUCCESS` is a macro defined in `stdlib.h`

``` c
#define string1 string2
```
string1 cannot contain white spaces, string2 can.

### Statements
End in a semi-colon (`;`). Preprocessor directives are **NOT** statements, do not end with a semi-colon.

## C Programs Are
- case sensitive
- zero or more
  - preprocessor directives
  - declarations
  - definitions
    - one or more functions
  - variables

Every C program must have exactly one `main` function, execution begins here.


### Functions
A number of statements grouped into a single logical unit (**block**). Pass by value, except in the case of pointers.

> we have no methods, only functions. Please pay attention to this distinction. It makes you look bad to other computer science professionals to talk about a “method” in a C program 

A **block** is enclosed by braces, `{` ... `}`, has zero or more **variable declarations**, and zero or more **non-declarative statements**

All declarations in a block must precede the first non-declarative statement. The loop control variable `i` for example.

``` c
{
    int i;
    for(i = 0; i < 10; i)) {
    }
}
```

Functions cannot be nested.

All functions have file scope and can be called anywhere in the file after the declaration.

### Function prototype
Informational only.
- number of arguments
- type of arguments
- name of arguments (optional)
- return type

``` c
float add_floats(float a, float b);
float add_floats2(float, float);
```

## Declaration
Type information only.
- Variable, can only be declared once in a block.
  - must be declared before being referenced in a non-declarative statement.

``` c
float new_float;
```

- Function
  - Known as the **prototype**
  - can be declared multiple times. When compiling multiple files, definitions must exist per file, thus multiple declarations of the same function.
  - must be declared before being referenced in a non-declarative statement. (before called/invoked)


## Definition
Type information and value
- Variable, can only be defined once per block
``` c
float new_float = 2
```

- Function, can only be defined once.
  - return type, argument types, and statements.

``` c
float add_floats(float a, float b) {
    return a + b;
}
```

## Assignment
**Read** : Pointers on C, Chapter 14, *The Preprocessor* (omit 14.5)
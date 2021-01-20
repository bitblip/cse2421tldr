---
title: "Text: Pointers On C (3_Intro_To_C)"
date: 2020-01-15T02:30:11-05:00
description : "Chapter 14, The Preprocessor (omit 14.5)"
tags: ["preprocessor", "c"]
---

# The Preprocessor
First step in compiling. Removes comments, inserts #include contents, substitutes #define symbols, and processes conditional compilation directives.

## Predefined symbols

| Symbol | Sample Value | Meaning
|---|---|---|
|\_\_FILE\_\_|"name.c"|Name of the source file being compiled.|
|\_\_LINE\_\_|25|Line number of the current line in the file.|
|\_\_DATE\_\_|"Jan 1 2020"|Date the file was compiled.|
|\_\_TIME\_\_|"18:04:30"|Time that the file was compiled.|
|\_\_STDC\_\_||1 if conforming to ANSI C, else undefined.|

## #define
All occurrences of `name` are replaced with `stuff`. `name` cannot contain white space characters but `stuff` can be anything.
``` c
#define name stuff
```

``` c
#define SOME_LOOPS for (i = 0; i < 10; i += 1>) { \
                      sum += 1;                   \
                   }
```
> Don't misuse this. Prefer functions for statement reuse.

### Macros
Define but with a comma delimited list of arguments. Remember, `name` cannot have spaces.

``` c
#define name(parameter-list) stuff
```

Macro replacements are textual, think carefully about the result of the text swap. Not only the insertion of the macro text into code, but also the argument text into the macro.
``` c
#define DOUBLE(x) ( (x) + (x) )
```

> Macro's that evaluate numeric expressions should be parenthesized to avoid unexpected interactions.

> Avoid macros that obscure C syntactical standards. It hinders other developers who know C, but not necessarily your macros.

### Substitution
`#define` statements may contain the invocation of other `#define` statements. Macros may not be recursive. Every uses of a macro is a direct text replacement and can massively bloat the size of the file to be compiled. This will execute marginally faster at the cost of code readability. By convention, all macro's should be defined in all upper case to differentiate from functions.

C will concatenate adjacent strings. Consider a macro that reports the formatted value of a statement. This will only work if a string literal, `"%d"`, is given as the macro argument.
``` c
#define PRINT(FORMAT,VALUE)                   \
  printf( "The value is " FORMAT "\n", VALUE) \
...
PRINT( "%d", 3 * 3);
/* The value is 9 */
```

For concatenating non string literals, we must use the preprocessor to convert the argument into a string. `#VALUE` will be replaced with a string representation of the argument. e.g. `"3 * 3 "`.
``` c
#define PRINT(FORMAT,VALUE)       \
  printf( "The value of " #VALUE  \
    " is " FORMAT "\n", VALUE)
...
PRINT( "%d", 3 * 3);
/* The value of 3 * 3 is 9 */
```

#### ## construct
`##` causes the token on their side of `##` to be concatenated. Note this bizarre method of dynamically assigning a variable ending in a number.
``` c
#define WEIRD_DYNAMIC_VAR_ASSIGNMENT(var_num, value)  \
                       var ## var_num = value
...
WEIRD_DYNAMIC_VAR_ASSIGNMENT(5, 100);
/* var5 = 100 */
```

### undef
Remove a definition. Usefully for re-defining a definition.
``` c
#undef name
```

### Command line define
Define definitions can come from the command line arguments to the compiler. `-U` will undefine.
``` bash
gcc -D name=definition
```

### 14.3 Conditional Compilation
Conditionally include and exclude sections of code. If the value of `constant-expression` is zero (false), the preprocessor will remove the block. `#else` and `#elsif` are valid as expected. Preprocessor statements may be nested.
``` c
#if constant-expression
  ...
#endif
```
A typical example of conditional compilation. DEBUG may be defined in any of the ways described.
``` c
#if DEBUG
  printf("debugging output");
#endif
```

#### If Defined
Testing for the presence of definitions is supported.
``` c
#if defined(symbol)
#ifdef symbol
#if !defined(symbol)
#ifndef symbol
```

### Library and local includes
Use angle brackets `<filename>` and double quotes `"filename"` to differentiate library and local includes.
``` c
#include <stdio.h>
#include "myFile.h"
```

Included files may themselves contain include statements. The Standard requires at least 8 levels of nested `#include` statements but does not specify a maximum. Convention dictates that there is little reason for more than two.

Complex programs may inadvertency cause the same file to be included multiple times. Use conditional compilation as a work around.
``` c
#ifndef _SOMEHEADER_H
  #define _SOMEHEADER_H
  #include ...
#endif
```
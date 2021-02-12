---
title: "Lecture 14"
date: 2021-02-09T02:30:11-05:00
description : "Strings in C"
tags: ["strings", "c"]
---

# Lecture 14
**Video** : [Strings In C](https://urldefense.com/v3/__https:/osu.zoom.us/rec/share/L-MbhY-DUc96mzoY7BhH58Go9D0euRmH1xN1WCIimE5ot5z0aFuO53Z6VPKy2vVw.3PwLXsmIRBf3Yjzg__;!!KGKeukY!jgKo13_VVjD40j7DbyNS3_YI9ORZBYN4Aj7urAT6Xp8HAmcs8SPmMsYocT35bXK3$)

**Slides** : [Linked Lists](https://osu.instructure.com/courses/95904/files/folder/Class%20slides?preview=29393509)

# Strings
ANSI C does not have a string data type. Strings are stored as contiguous bytes in memory, as an array. Include `string.h` and or `strings.h` to access library string functions. Character will be encoded to memory as ASCII.

To manipulate strings, use `char` arrays. Character arrays must end with the **NULL** character `\0`. The null character is a critical differentiation between strings and other kinds of arrays.

> If the `\0` is missing, your code will not behave correctly.

> String length `strlen()` is undefined without a null byte.

``` c
char string1[] = "Some string";
char string2[12] = {'S', 'o', 'm', 'e', ' ', 's', 't', 'r', 'i', 'n', 'g', '\0'};
```

## Ending null trick
Define the array size to be one larger than the desired string length. The default behavior of the compiler is to initialize undefined elements in the initializer as `NULL`.
``` c
char string3[12] = {'S', 'o', 'm', 'e', ' ', 's', 't', 'r', 'i', 'n', 'g'};
```

## Pointers
Strings are character arrays and all of the pointer things apply, including pointer arithmetic.

``` c
char *stringA = "start";
char stringB[] = "stop";
```

`stringA` is only a pointer to the constant `"start"` stored in read only memory. Trying to modify any character in stringA, `stringA[0] = 'S'`, will result in a segmentation fault.

Be aware, you cannot assign `stringA = stringB`. This will cause an **incompatible type** compiler error.

## printf
When printing strings, `printf()` should be passed the address of the start of the string. Do not dereference the pointer.

``` c
printf("%s\n", stringA);
```

## Character Classification
Classify characters using `ctype.h` prototypes. Such as spaces `ispace()`, numbers `isdigit()`, lower case `islower()`, and many others.

## Character Modifications
Modify character using `ctype.h` prototypes. Such as converting a lower case character to an upper case character `toupper()`.
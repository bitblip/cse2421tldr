---
title: "Lecture 9"
date: 2020-01-26T02:30:11-05:00
description : "C pointers Part 1"
tags: ["pointers", "c"]
---

# Lecture 6
**Video** : [C Pointers 1 Part A](https://urldefense.com/v3/__https:/osu.zoom.us/rec/share/1cH0fwe-6AaW6vblfsNwSgH8ecfA5YTHiY-aDQh73KWvlhW7-wrY7Zb5OY9-ujWL.NlyWX9aexZfwF0vh__;!!KGKeukY!g0HVicmbD96-kMBf6C0Y6yeIBc6PxYEnXHwqREwc2_xHUHentdY3mZguAaV9ofIi$)
**Video** : [C Pointers 1 Part B](https://urldefense.com/v3/__https:/osu.zoom.us/rec/share/jHawEDCjBdpIoDa8Z-hTOtSFMjuV08B6Zvh72uakOt-t1cyK60tUU_oDdqZN3EK9.oJcDVykGNjeBAhsH__;!!KGKeukY!jJ1CqAWnDNR1E4qfBxZ2Px7AooNk-vvhjAWMgVGoEqeYijyVP3y-zrKFlv6cy8_p$)

**Slides** : [C Pointers Part 1](https://osu.instructure.com/courses/95904/files/folder/Zoom%20classes?preview=28800173)

# Pointers
All variables have an address. This identifies the location in memory of the value of the variable. On 64bit systems, the address is an 8-byte integer. Memory addresses can range from 0 up to the size of memory in bytes - 1.

A variable name is known as the identifier and the value is stored at the identifiers address. The mapping is maintained by the `symbol table`.

A `pointer` is a variable or constant that contains the address of another variable. `pointer` is not a type.

> This address can be called `a reference` but is usually not so in C terminology.

Pointers are denoted by the deference operation `*` prefix. Addresses are retrieved from variables by the address operator `&` prefix. These operators are part of the identifer, **NOT** the type. A pointer expression can be read as "dereference". For example, `char *c;` can be read as `char dereference c`.

``` c
int b;
int *int_ptr;
int_ptr = &b;
```

Pointer types, `int*`, `byte*`, `char*`, ... etc, are critical in informing the compiler how the bytes at an address are encoded. Type mismatches will have very unpredictable behaviors.

> The compiler is horrible at guessing types of data.

# Printing the value a pointer references.
Use indirection `*C`. This is an indirect way to access the value of B.

``` c
int B = 8;
int *C = &B;

printf("%i", B)
printf("%i", *C) /* *C is a variable, not a pointer operator? */
```

A way to think about `&` and `*`.

`&` = GetAddressOfIdentifier(var)
`*` = GetValueAtAddress(var)
`*` = SetValueAtAddress(var)

# Pointers to pointers
An integer pointer to an integer pointer, or more simply said, an int pointer pointer.

``` c
int **x;
```

# Pointer Castings
Pointer types can be recast. Remember that pointer type determine memory size operations. `char` is 1 byte and `int` is 4 bytes.

``` c
int i = 5;
char *y = (char *)(&i);
```
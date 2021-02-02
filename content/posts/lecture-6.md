---
title: "Lecture 6"
date: 2020-01-19T02:30:11-05:00
description : "C part 3 IO"
tags: ["i/o", "formatting", "c"]
---

# Lecture 6
**Video** : [C Part 3 IO](https://urldefense.com/v3/__https:/osu.zoom.us/rec/share/0f8G4pQm7Ho5pLZjxA1k6nCHo2wDT5wcvVM8ZyUM_xhpQk_i080V6Rim2mvlVo3u.YWJFqolIRfzRWXUg__;!!KGKeukY!nuphLDQ-092N_K34ykIVfiw4HD0en7muOJU3ZmYokBG7wDmSd7LGVVdkW-xpuJHD$)

**Slides** : [C Part 3 IO](https://osu.instructure.com/courses/95904/files/folder/Zoom%20classes?preview=28650853)

# Assignment
Read Pointers on C, 15.8, 15.8.1, 15.10 through 15.10.4 inclusive.

* I/O
No standard Input/Output defined in language, use `<stdio.h>`. Linux/Unix use ASCII, course will also use ASCII.

## Character I/O
Return integer ASCII characters. Must be cast to `char` or printed with `"%c"`. Can return `EOF`.
``` c
int getchar(void)
int putchar(int)
int scanf(char const *format, $params...)
```

## Formatted I/O
f indicates a required formatted strings. `"%..."`

Inputs "standard in" according to format, assign values to n-arg addresses.
``` c
int scanf(format, &params...)
```

## Address operator
`&` operator returns the memory address of the parameter. Not needed for arrays, array references are already the address for the start of the array.

Outputs "standard out" according to format. outputs n-arg values.
``` c
int printf(char const *format, params...)
int fprintf(FILE *stream, char const *format, params...)
int sprintf(char *buffer, char const *format, params...)
```

## Formatted output
 Each sequential `%` is paired with the n+1 argument.  See `codes`, `modifiers`, `quantifiers`, `alternate forms`, and `optional fields` for complete formatting options. God speed.

 ``` c
 printf("%d %d", fahrenheit, celsius);
 printf("%3d %6d", fahrenheit, celsius);
 ```

 Escape `%` with `%%`. Matched, but not converted.

 `scanf` ignores leading white space, not trailing.

 ## Complete code
For this course, only p is need to know.

 `"%-+ Ow.pmc"`
- - left justify
- + print with sign
- _space_ print space if no sign
- O pad with leading zeros (field width)
- w min field width
- p precision
- m conversion character
    - h short, l long, L long double
- c conversion character
    - all the rest

Default precision is 6 digits.

 Need to know format characters.
 |character|displayed|
 |---|---|
 |%c|character|
 |%d|signed decimal|
 |%i|signed decimal (int)|
 |%f|signed float|
 |%s|NULL terminated string|

 `%d` is ideal for most cases.
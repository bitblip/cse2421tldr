---
title: "Lecture 16"
date: 2021-02-11T02:30:11-05:00
description : "C Function Pointers"
tags: ["function", "pointer", "c"]
---

# Lecture 16
**Video** : [C_Function_Pointers Part A](https://osu.zoom.us/rec/play/8lboG9poUPLHXz_wdn-H26I2NH9QhofscX7ukV_CYlDo8nvKviTNyrQT2BaBcNOIPNdFHWosVxo1Oue7.EEYKXdYDQeJ2sA-m?continueMode=true&_x_zm_rtaid=jYBsbZNzRiaip23fAVhx3w.1613330917299.3536075cb21fcb7509065f857b904aeb&_x_zm_rhtaid=767)
**Video** : [C_Function_Pointers Part B](https://osu.zoom.us/rec/play/PJL3Jy9wf4dn8yhIa0IGFstO2aKLPkJxipodB0ZtcFBmfyp01Rtbv18TWj0zgs4nzuccvMP2_9QRB9dZ.lVjCEk46zjnQsrts?continueMode=true&_x_zm_rtaid=jYBsbZNzRiaip23fAVhx3w.1613330917299.3536075cb21fcb7509065f857b904aeb&_x_zm_rhtaid=767)

**Slides** : [C_Function_Pointers](https://osu.instructure.com/courses/95904/files/folder/Class%20slides?preview=29492072)

> If you thought pointers were strange, function pointers are stranger.

Declare a function which returns a pointer. Find an int value in `array` and return a pointer to the found value.
``` c
int *findValue(int value, int size, const int *array);
```

## Function Pointer
Function statements are stored in memory. We can find this location in memory.  This is a pointer to a function (pointer function) which returns an int, named `funcP`. The location of the parenthesis `()` in the following example are critical to differentiate this statement from the example `*findValue` above.
``` c
int (*funcP)();
```

Initialize and use such a pointer. The identifier name `fp` is kind of hard to spot.
``` c
int returnMax(int size, const int *array);
...
int (*fp)(int, const int*);
fp = &returnMax;
```

We can combine the declaration and assignment into a single statement.
``` c
int (*fp)(int, const int*) = &returnMax;
```

A function pointer must declare all type information. As a counter example. The following assignment is invalid. The second argument `upper` is a mismatch between `int` and `const int *`. Argument 3 is missing entirely.

``` c
long returnLow(int lower, int upper, char *values);
...
int (*fp)(int, const int *);
fp = &returnLow; /* Any mismatch is an invalid assignment. */
```

The address operator is optional when getting function addresses and normally omitted.
``` c
fp = &returnMax;
fp = returnMax;
```

## Calling a function with a function pointer
Again the use of parenthesis here is critical to get the correct behavior.
```  c
int i = (*fp)(argument1, argument2);
```

Like the optional address operator `&` for function pointers, the dereference operator `*` is also optional.

``` c
int i = fp(argument1, argument2);
```

## Uses of function pointers
Advanced techniques such as **callbacks** and **run-time-binding** which are outside the scope of those course.

### Replace switch/if statements
We can select functions to call like accessing elements of an array. By the nature of arrays, an array of function pointers must all be of the same return type and have the same type and order of parameters.

Suppose we wish to display a menu of math commands that a user can choose to execute.
``` c
float add(float a, float b);
float subtract(float a, float b);
float multiply(float a, float b);
float divide(float a, float b);
```

Declare an array of function pointers and store the addresses of these functions.
``` c
float (*fp_array[4])(float, float) = {add, subtract, multiply, divided }
```

Get user input, likely `scarf` but how isn't important.
``` c
return fp_array[userOption](userValue1, userValue2));
```

It's likely desirable to want to access fp_array outside the scope where it was declared. Pass the command array as a pointer, which becomes a pointer to a pointer. The deference operator is still not required because the array accessor `[]` handles the outer dereference.
``` c
float doCommand(float (**fp_array(float,float)), int command, float value1, float value2) {
  return fp_array[command](value1, value2));
}
...
doCommand(fp_array, 0, 1, 1);
```
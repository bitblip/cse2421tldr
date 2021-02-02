---
title: "Lecture 10"
date: 2020-01-26T02:30:11-05:00
description : "C Pointers Part 2"
tags: ["pointers", "memory management", "c"]
---

# Lecture 10
**Video** : [C Pointers 2 Part A](https://urldefense.com/v3/__https:/osu.zoom.us/rec/share/WZvVx2zl6V9HnHvMRhGh5wYCW-JrYk1sbO1Gc_ameCTbJbCjMRHixyuANxr16Ck.oE8IxmgUYIfWW0Ib__;!!KGKeukY!kA4SNYv_c1kvvDef8vv0W5hm8DH64nfNH9SVKKK8qjKMnIeP5cMZ9LqifSmmlT8S$)
**Video** : [C Pointers 2 Part B](https://urldefense.com/v3/__https:/osu.zoom.us/rec/share/vOJVxqTeYidFIcPSzRaUIvcn4RqTD-t5gczkvalD4JEQDqq0JRzKv1VGRgtHJzpV.rGHOn0z00gdp5WGa__;!!KGKeukY!j7l0foPN46l1RAc-0hbrp4fR_wBnNR-MVXil6abd_lRDgXyTTFSPH9TzDqB8NZ38$)

**Slides** : [C Pointers Part 2](https://osu.instructure.com/courses/95904/files/folder/Zoom%20classes?preview=28902214)

# Pointers part 2
Relationship between arrays and pointers, void pointers, dynamic memory, pointer arithmetic, and passing pointers.

## Arrays
Arrays can only be accessed by pointers. Static arrays are allocated by the compiler, dynamic arrays must be allocated with `malloc` at runtime and will be referenced by a void pointer.

Except for strings, there is no library function to giv teh size of an array. Size must tracked in your own code.

> Take care to not access elements outside the bounds of an array. This will produce a segmentation fault or modify memory you did not intend.

An array constant is the same as the address of the first element
``` c
int scores[3] = {1,2,3};
```

|Element|Address*|Value|
|~~~|~~~|~~~|
|scores[0]|0x600020|1|
|scores[1]|0x600024|2|
|scores[2]|0x600028|3|

`scores` is the same as `&scores[0]`. `&scores` is something completely different.

### Pointer Arithmetic
Pointers can be added to and subtracted from by integers, and by each other. This is how move a pointer around and can be used like indexing.

> Does not apply to pointers to functions.

Work with arrays without using the index notation.
``` c
#define SIZE 15
long l_array[SIZE];
long *l_array_ptr = l_array;
int i;
for (i=0; i<SIZE; i++>) {
    *l_array_ptr++ = i; /* Assign each element value i */
}

long thirdValue = *(l_array + 3) /* same as l_array[3] */
```

This works because arrays are stored contiguously in memory and the compiler knows the elements are `long`s. Adding 1 to a float pointer is in fact adding `(1 * (sizeof(long)))`.

The size of types is taken into account when adding and subtracting pointers. `int *p1 = fooArray;` and `int *p1 = fooArray+1;` are separated by 4 bytes `sizeof(int)`, however `p2-p1` is 1.

To get the actually number of bytes, cast to `unsigned long`. `((unsigned long)p2 - (unsigned long)p1)` is 4.

Pointers can be compared. `p2 > p1` is 1. `p1 > p2` is 0.

### Pointers to void
Address any kind of data however dereferencing must be cast to the correct pointer type. Makes typeless parameters possible but this is outside the scope of the course.

``` c
void *pVoid;
int var1 = 1;
pVoid = &var1;
printf("cast to dereference pVoid %d", *(int*)pVoid);
```

> You must cast first `(int*)` then dereference `*(int*)`.

Dynamic allocations return a void pointer because `malloc` is made generic for all data types.

## Dynamic Allocation
Include stdlib.h

- `void *malloc(size_t size);`
- `void *calloc(site_t nmemb, stize_t size);`
- `void free(void *ptr);`
- `void *realloc(void *ptr, size_t size);`

> Always check the value of the returned void pointer. `null` indicates a failed `malloc` or `calloc` operation.

> IMPORTANT - You will loose points for not checking for `null`.

### malloc()
Returns a void pointer to as much allocated memory as specified by the argument. Memory will contain garbage values, values are not initialized.

``` c
int *p;
p = malloc( 4 * sizeof(int) ); /* 4 * 4 bytes, probably */
```

> Always use `sizeof(type)`, In the example, `int` may not be 4 bytes.


### calloc()
Returns a void pointer to as much allocated memory as specified by type and number arguments. Data is initialized.
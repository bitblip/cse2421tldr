---
title: "Lecture 12"
date: 2021-01-04T02:30:11-05:00
description : "Structures in C"
tags: ["structures", "c"]
---

# Lecture 12
**Video** : [Structures in C Part A](https://osu.zoom.us/rec/play/e24m9bFixu0j1aqBjUMicc_K4KQsl3kfX-feEDOz8mVxby-1osBgjWIgtEO5jHPNG6yQR7nu2e3Nd1ti.yCXnMRpifBHNfI0-?continueMode=true&_x_zm_rtaid=-TWha3VKT8KsS_LliFbwLw.1612734115477.eaa04ae0e2c9d8ea90808a799fd75234&_x_zm_rhtaid=276)
**Video** : [Structures in C Part A](https://osu.zoom.us/rec/play/CxBlkW8KC64SvBvOf1Kk2hnGBgwS9dkqVLo5CdNUpV281j24n-43fT8L5BkXv0FyBNor31Plo2oUfDZ6.qawAHFgoua3Rcju6?continueMode=true&_x_zm_rtaid=QnanR12eTGeMm7jaSafqzQ.1612742401686.41ef499faa518ddc2dadc72e0ff1bdc0&_x_zm_rhtaid=688)

**Slides** : [Structures in C Part A](https://osu.instructure.com/courses/95904/files/folder/Class%20slides?preview=29100219)

# Structures
Collection of members (values) that can be of various types. Since members may be of different sizes, indexing cannot be used to access members of a structure. Members can be any type including Arrays, Pointers, Structures, User-defined data, and primitive types.

> A structure is **NOT** an array of its members.

Structures of the same type can be assigned to one another. Array members are copied.

``` c
struct Tag {
  type name;
  ...
};
struct Tag x, y, *z;
```

`Tag` can be any valid identifier.

Structures can also be declared without a tag but it's not recommended.

``` c
struct {
  type name;
  ...
} x, y[10], *z;
```

## typedef
Create a new data type that is a structure. Note `struct` is not used when declaring the variables `x`, `y`, and `*z`.

``` c
typedef struct {
  type name;
  ...
} Tag;

Tag x, y[10], *z;
```

> Programmer preference as whether to use the `struct tag` or `typedef` approach. Be constant and apply the DRY principle by placing `typedef` or `struct tag` declarations at the top of your source file or a header file as needed.

## Member Access
Use the **dot** operator to access members. The dot operator has left to right associativity, meaning changing dots is possible.

``` c
x.name;
y.name;
*z.name;
foo.bar.bam;
```

### Indirect Member Access
Accessing structure members using a pointer. Dereferencing works as expected but it's annoying `(*foo_ptr).member`. The **arrow** operator is a solution to this. Note this must be used on a structure pointer. Dereferencing is built into the arrow operator.

``` c
(*foo_ptr).member;
foo_prt->member;

(*(*foo_ptr).member).nested_member;
foo_ptr->member->nested_member;
```

Concerning an array of structs (struct pointer), pointer arithmetic is still valid. `foo_ptr++`.

## Self-Referential Structures
Structures can not be declared recursively (illegal in ANSI C). Consider that the `c` member must allocate memory for 3 things. Two integers and another `Self_Ref1`. This will consume infinite memory.

``` c
struct Self_Ref1 {
  int a;
  int b;
  struct Self_Ref1 c;
}
```

Declare using pointers to fix this.
``` c
struct Self_Ref1 {
  int a;
  int b;
  struct Self_Ref1 *c;
}
```

## Initializing
Structs are initialized in a similar fashion to arrays. Values are separated by commas int he order they are defined in the struct.

``` c
struct Struct_Example {
  int a;
  short b[10];
  Some_Struct c;
} x, y = {
  10,
  {1,2,3},
  {20, 2.2}
}
```

## Passing Structures
Structures can be passed by value however they can be arbitrarily large. Use a pointer to pass a structure to a function.

> Only structures which are not much larger than a pointer should be passed by value.

As usual with read only functions, pass structure pointers as constants. `float func2(const struct *structPtr);`
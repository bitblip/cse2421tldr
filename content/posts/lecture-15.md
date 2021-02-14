---
title: "Lecture 15"
date: 2021-02-09T02:30:11-05:00
description : "Storage Class Scope Linkage"
tags: ["command line", "args", "c"]
---

# Lecture 15
**Video** : [Storage Class Scope Linkage](https://urldefense.com/v3/__https:/osu.zoom.us/rec/share/U81rLYMxE5KA71BWlJ5GrgMF28_hDPKU7WyGsh3ZVlvElDhmakuuzcpUPFjUurlv.s1ucP0zcTpLrXOh___;!!KGKeukY!jdSMX82dOc5FNhn_5xTZE8dDGji5AzkV9eN9VoGMjMLiU2Eax8LD8rtoKq1YmEzd$)

**Slides** : [C_Storage_Class_Scope_Linkage](https://osu.instructure.com/courses/95904/files/folder/Class%20slides?preview=29393517)

# Memory types
Kinds of storage common to all programs.

> If you know what kind of storage a part of your program is held in, this is valuable information.

* Stack
* Heap
* Registers
* Disk

## Memory Segments
Divided into 3 parts. Stack and Heap memory start as distant as possible from one another and grow towards each other.

* Stack
  * Highest memory address, begins (the bottom) at the highest address and grows down (lesser addresses).
* Heap
  * Between stack and code, grows upward.
* Code
  * Lowest memory addresses, begins at 0. Does not grow and read only.

> As long as Stack and Heap don't run into one another, everything will be fine.

## Important Terms
Emphasis on remembering these, expect to be tested. This `class` has no relationship with classes in c++ or java.

* Storage class
  * static
  * automatic (or auto)
  * register (inside the processor)
  * external (this is linkage)
* Scope
  * block
  * file
  * prototype
  * function (limited use, not covered)
* Linkage
  * internal
  * external
  * none (no linkage)

## Storage class
Determines the storage **type** and **lifetime** of a variable and it's **initialization**. Determines if a variable will be initialized by the compiler (loader) or by program code. The default storage class for a variable depends on where it is declared.

### Static
On the heap. Declarations that occur outside of any block. Allocated for as long as the program runs and cannot be stored anywhere else. Initialized to default values by the loader.

Using `static` outside of a block, modifies the **linkage** from external to internal.

### Automatic
On the stack. Declared within a block and do not persist outside the block. No default value, must be initialized by code. Function arguments also have automatic storage and the class cannot be changed.

Declarations inside a block can be declared `static` to modify their default `automatic` storage class. Direct access to this variable will be lost when the block exits.

### Register
A sub-type of *automatic*. Use on automatic variables to store variables on the CPU (maybe). Space may not be available on the hardware. Used on frequently accessed variables such as loop indices to improve performance. Other **automatic** constraints apply.

> If your variable is accessed 1,000 times, it probably wont improve it much. If it's accessed a million times, it will improve it a little more.

## Scope
Area in memory available to a `block`, `file`, and `prototype` for **Direct** variable access. Direct meaning by the variable name as opposed to using a pointer.

### Block scope
List of statemented inclosed in braces `{}`. Nested blocks will have independent scope and can have identifiers of the same name as an outer block without conflict because each block has it's own scope.

> Do not obscure variables in a nested scope by re-purposing an existing variable name in an outer scope, this is bad practice.

### File scope
Declarations that occur outside any block. Accessible anywhere in the file after the declaration. Incorrectly referred to in C as "Global". Prototype identifiers are file scope. Note this is different from the scope inside the prototype (prototype scope).

### Prototype Scope
Parameter names given in a function prototype.

``` c
void function1(int var1, int var2);
void function2(int var1, int var2);
```

Because scope is unique to the prototype, `var1` and `var2` can be reused in different scopes.

## Linkage
Given an identifier, if this identifier appears in many scopes, does the identifier refer to the same thing? Mostly dealing with function prototypes that appear in multiple files. Only file scope variables "have" linkage.

We wish to control what identifiers in our file are and are not in common with identifiers in other files.

### None (no linkage)
Block and function parameters are always given their own unique scope and can never be linked. Doubly so because only file scope identifiers can participate in linking.

### Internal Linkage
Identifiers that should be isolated and not in common with any other file. Identifiers of this type with the same name in separate files are not the same thing.

### External Linkage
Identifiers that are in common with identifiers of the same name in other files.

## Stack
Place in memory allocated for a function when it is called. This memory is Deallocated when the function returns. Recursive functions eat up Stack space.

`functions` and `auto` occur here.

## Heap
Heap space is allocated for the process. The operating system will reclaim this space when the program exits.

`calloc`, `malloc`, and `static` occur here.

# Exercises
``` c
static char varB = 103;

void func_1() {
    static float varD = 6.7;
}

static int varA = 21;
void func_2() {
    int varC = 42;

}
```

1) Static, File
2) none, File
3) none, Prototype
4) none, File
5) Automatic, Block
6) Automatic Static, Block
7) Automatic, Block
8) Register, Block

6 is Automatic and Static?
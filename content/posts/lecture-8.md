---
title: "Lecture 8"
date: 2020-01-21T02:30:11-05:00
description : "C part 5 Control Structures"
tags: ["loops", "c"]
---

# Lecture 6
**Video** : [C Part 5 Control Structure](https://osu.zoom.us/rec/share/cByZb6Vvbbz8KwBxferZilhsaroeyEtk2szJPnXlf6BjjUuuThcBCmEFRg9bKVIW.3TXAttqUH2Wb9ZO4?startTime=1611238622000)

**Slides** : [C Part 5 Control Structure](https://osu.instructure.com/courses/95904/files/folder/Zoom%20classes?preview=28650858)

# Loop Constructs
Best practice is to always use `{}` for clarity. 1 line loop bodies without `{}` will be deducted points.

``` c
for (expression1, expression2; expression3) {
    ...
}
```
> Variables cannot be initializes in expression1. i.e. `int i = 0`. Only `i = 0` is allowed in expression1.

``` c
while (expression) {
    ...
}
```

`do while` will always execute at least once.
``` c
do {
    ...
} while(expression);

## Break
`break` will exit the innermost loop or switch statement.

``` c
while(1) {
    if(expression) {
        break;
    }
}
```

## Continue
`continue` will stop execution of the current loop iteration and begin the next.

``` c
for(...; ...; ...;) {
    if(expression) {
        continue;
    }
}
```
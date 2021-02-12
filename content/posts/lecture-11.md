---
title: "Lecture 11"
date: 2021-02-02T02:30:11-05:00
description : "Software Design Principles in C"
tags: ["design", "c"]
---

# Lecture 11
**Video** : [Software Design Principles in C](https://urldefense.com/v3/__https:/osu.zoom.us/rec/share/4PLhs0qyCrStxs8WKzwFWPUkn-6lgDLqWimym7WwFMN0aqdtLqfSvXCX8XCCc8U.0tJqfRGpjvbMzP_6__;!!KGKeukY!ksPATqlS_HQ4CSjDiXkTp_EoMtcq1xu5u9HdPOa6myqAa6ocTSUq9e5Wnryov3xj$)

**Slides** : [Software Design Principles in C](https://osu.instructure.com/courses/95904/files/folder/Class%20slides?preview=29100209)

# Communication
Give users precise prompts such as type and formatting such as spaces, tabs, and new lines. Describe outputs with good labels.

# Structure
- \# include directives
- \# define directives
- Function prototypes
- `main`
  - Variable declarations
  - Calls to other functions
  - No work should occur inside `main`.
- Function definitions

# Reusable components
Functions should provide a single piece of functionality that is reasonably likely to be useful in other programs. This results in code that is inherently easier to test and debug since each function can be tested in isolation.

> If there could be a program where we would want to do x without doing y, then x and y should not be combined.

# Communication between components
Functions should only communicate at their interfaces. That is functions should only be given access to data passed to the function as opposed to data in the calling environment. This implies that "Global" (file scope) variables should be not used and is in fact not allowed in this course.

Rules for passing parameters. Let A and B be functions such that A calls B and passes variables to B.
- If B never needs to modify the value its arguments, then A should be the parameter as a value (if possible).
  - IF A must pass a pointer, then A should pass a pointer to a const value (read only access).
- If B needs to modify the value of its arguments, then A should pass the variable by reference.
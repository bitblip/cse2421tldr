---
title: "Lecture 1 and 2"
date: 2020-01-12T02:30:11-05:00
description : "Intro to course and Unix vs Linux."
tags: ["certification", "stdlinux", "c"]
---

# Lecture 1

## Intro
{{<video label="label" mp4="https://nv.instructuremedia.com/fetch/QkFoYkIxc0hhUVNZTjRNSE1Hd3JCMm5sQldBPS0tZjRmMzkyNDY4NjE4NDg2ZjJiYzlmOWIyNmIwOTU2OTZhY2ViNmU0NA.mp4">}}

**Slides** : [Intro To Course](https://osu.instructure.com/files/28363022/download?download_frd=1)

**Email** : Mike green.15@osu.edu

**Text** : Computer Systems: A Programmer’s Perspective, 3rd Edition, by Randall E. Bryant and David R. O’Hallaron, (Required)

**Text** : Pointers on C, by Kenneth Reek 1997

Always include the following certification text when submitting assignments. Either in a readme or in a code file as a comment.

> BY SUBMITTING THIS FILE TO CARMEN, I CERTIFY THAT I HAVE STRICTLY ADHERED TO THE TENURES OF THE OHIO STATE UNIVERSITY’S ACADEMIC INTEGRITY POLICY WITH RESPECT TO THIS ASSIGNMENT.

Connect remotely to [stdlinux](https://cse.osu.edu/about/remote-access)

Why study C?
[https://osu.instructure.com/courses/95904/files/folder/Zoom_Lectures/Class%20slides?preview=28363022](https://osu.instructure.com/courses/95904/files/folder/Zoom_Lectures/Class%20slides?preview=28363022)

Advantages
- Explicit, does only what you tell it
- Manual memory management
- Pointers
- Compiled to machine code
- No overhead, raw power/speed

## Unix/Linux
{{<video label="label" mp4="https://nv.instructuremedia.com/fetch/QkFoYkIxc0hhUVF2azRrSE1Hd3JCM1RvQldBPS0tMWZhYzI1Yjg0OGUxMTg1MjJmYTdlNDcwYThjODVjMmZiMGRkNGNjOA.mp4">}}

**Slides** : [Unix Linux](https://osu.instructure.com/files/28363025/download?download_frd=1)

Unix developed in C from 1069-1971 at AT&T Bell Laboratories. Proprietary, modular, unfired file system, portable.

Linux developed in C in 1991. Unix clone, re-implemented as open source. Has many distributions.

Compiling your program.
```
% gcc -ansi -pedantic -g -o <executable> <filename.c>
```

Compiling C programs is done with the `gcc` command. Use `-ansi` to use the ANSI C standard and `-pedantic` for warnings. The `-g` flag will allow debugging with `gdb`.

## Assignments
**Read** : https://tldp.org/LDP/intro-linux/html/sect_01_01.html [^1]

**Read** : https://www.diffen.com/difference/Linux_vs_Unix [^1]

**Lab** : [Lab1](https://osu.instructure.com/courses/95904/files/folder/Lab?preview=28328652)

[^1]: Expect questions from these readings
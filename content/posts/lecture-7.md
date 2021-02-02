---
title: "Lecture 7"
date: 2020-01-21T02:30:11-05:00
description : "C part 4 Redirection"
tags: ["c"]
---

# Lecture 6
**Video** : [C Part 4 Redirection](https://urldefense.com/v3/__https:/osu.zoom.us/rec/share/SmP0313jzBbpvkY3b43vqQHIjz87t53Ta9_wa_lwf9ncAkois1aZgfj2qWJVt5D6.LVf-CM9JsGSnSzF-__;!!KGKeukY!lm_C1baWRZjwPkyLKBJCghfVg-ggssz2ujRxreVrj04kpMwdB_uk10W1lADFdk_w$)

**Slides** : [C Part 4 Redirection](https://osu.instructure.com/courses/95904/files/folder/Zoom%20classes?preview=28650854)

# Redirection
3 distinct data streams: `stdin(0)` `stdout(1)` `stderr(2)`. Unix/Linux default to keyboard, screen, and screen respectively. 

This can be changed with the command line.
- `<` input
- `>` output
- `2>` error

``` bash
prog1 < infile > outfile 2> outErrorFile
```

> Input files must end with `EOL`. This is a blank line at the end of the file.

> Standard Input, Output, and Error streams cannot be changed mid execution.

> File paths are current directory unless a full path is used.

For output file overwriting use a single `>`, to append to the file use `>>`.
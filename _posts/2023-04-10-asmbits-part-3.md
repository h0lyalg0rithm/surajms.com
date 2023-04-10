---
layout: post
title: Asmbits Part 3
date: 2023-04-10 16:59 +0200
---
Today I continue with the two next problems in asmbits.The first question is more interesting than the second one.Here we go.


##### Write a function to return the absolute value of argument
The way this works is we compare if the value is less than 0 and if its less than 0 we subtract the value from 0, which converts it back to a positive number.
```
.global _start
_start:
    mov r0, #10
    bl abs
    b _start

.global abs
abs:
    cmp r0, #0
    neglt r0, r0
    bx lr
```

##### Write a function that returns the sum of its two parameters.

```
.global _start
_start:
    mov r0, #1
    mov r1, #1
    bl add
    b _start

add:
    add r0, r0, r1
    bx lr
```
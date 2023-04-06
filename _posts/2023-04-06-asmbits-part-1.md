---
layout: post
title: Asmbits Part 1
date: 2023-04-06 23:58 +0200
---
From the last two days I have been learning arm assembly, when I came across this website [asmbits](https://asmbits.01xz.net/).
You can answer the questions and run them on the website without the hassle of installing an arm emulator on your x86 machine.

Here are the first two questions.
- Write the assembly to return from a function

```
.global _start
_start:
    bl func

    1: b 1b

func:
    cmp r0, #0
    neglt r0, r0
    bx lr
```

- Return the value 123 from the function

```
.global _start
_start:
    b1 func
    1: b 1b

func:
    mov r0, #123
    bx lr
```
The best resource I found on arm assembly was their own reference manual.You can find it here [https://developer.arm.com/documentation/ddi0406/cd/](https://developer.arm.com/documentation/ddi0406/cd/)
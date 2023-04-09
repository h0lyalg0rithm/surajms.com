---
layout: post
title: Asmbits Part 2
date: 2023-04-09 02:00 +0200
---
Today I gave asmbits a try, this time the questions were simple like the ones I solved the other day.

##### Write a function that returns the bitwise inversion of its parameter. 

We need to invert the bits that make up the integer.
```
.global _start
_start:
    mov r0, #1
    bl invert
    1: b 1b

.global invert
invert:
    mvn r0, r0
    bx lr
```

##### Write a function that returns the whether its parameter is odd. Return 1 if odd, 0 if even.
This question was more interesting as there were multiple ways to solve it, the slower solution would involve runnig the following code
```
bool is_odd(int n){
    return n % 2 > 0;
}
```
This solution will result in multiple assembly instructions including a branch instruction.
A faster solution would be the following, where we mask all the bits except for the least significant one.
```
.global _start
_start:
    mov r0, #1
    bl odd
    1: b 1b

.global odd
odd:
    AND r0, r0, #0x00000001
    bx lr
```
Here is another alternative solution 
```
.global _start
_start:
    mov r0, #1
    bl odd
    1: b 1b

.global odd
odd:
    BIC r0, r0, #0xFFFFFFFE
    bx lr
```
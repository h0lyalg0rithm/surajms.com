---
layout: post
title: Intel Parallelism Fundamentals
date: 2021-01-29 01:17 +0100
---
As part of my Masters program, I have to complete some online courses to receive extra credits and complete my degree much faster.The university shared a list of approved courses which I could take.I decided to go with the [Fundamentals of Parallelism on Intel Architecture](https://www.coursera.org/learn/parallelism-ia/home/welcome) course.

I was able to complete the course in a couple of days.It was my first online course that I completed from start to finish moreover in a week.
Here is my [certificate](https://www.coursera.org/account/accomplishments/records/33VT29CE29MT) for completing the course.

Here are my learns from the course
- Vector Arithmetics is cheap, Memory Access is expensive.
- Compiler flags: Compiling the code for the specific target brought in a lot of improvements to the performance.In the case specifically we were using Intel Phi, using SIMD instructions helped a lot.
- Loop interchange: Loop interchange involves switching the inner loop with the outer loop allowing the compiler to optimize the code for SIMD instructions and cache locality. 
- Combining OpenMP and MPI: The combination of the MPI and OpenMP can greatly improve performance.

![](/wp-contents/uploads/2021/01/perf.png)
Using the techniques mentioned above we were able to scale code to more than 1100 times faster on a single machine, with more machines we could make it run even faster.

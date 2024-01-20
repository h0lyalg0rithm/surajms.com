---
layout: post
title: Using LD_PRELOAD to hijack library calls
date: 2024-01-20 23:02 +0100
---
My masters project was based on writing a allocator which would allocate memory to either the DRAM or a persistent memory device(Intel Optane), which is controlled at compile time.It was supposed to be an alternative to an existing runtime based allocator.
This runtime allocator makes use of a feature of the dynamic linker which tries to resolve the symbol (function names/external variables etc) and connect it to the function calls in the application.

Using this feature you can track all of the malloc/free calls used by the application and decide where the memory needs to be allocated.
Here is how you can hijack all the malloc calls made by the application.

~~~C
// _GNU_SOURCE enables the RLD_NEXT handle used in the dlsym
#DEFINE _GNU_SOURCE

// Provides the prototype for dlsym
#include <dlfcn.h>
#include <stddef.h>

// Create a function pointer to hold the location of the malloc call
static void* (*real_malloc)(size_t size);

// __attribute__((constructor)) tells the loader to run this function once the library is loaded
void* __attribute__((constructor)) lib_init() {

    // dlsym looks for the symbol malloc which appears after
    real_malloc = (void*(*)(size_t))dlsym(RLD_NEXT, "malloc");
}

// We hijack all the malloc calls from the application
void* malloc(size_t size) {
    return real_malloc(size);
}
~~~
We then need to build the code as a shared library using `gcc -shared -fPIC -o libmalloc.so main.c`

Then to use the library all you need to do is `LD_PRELOAD=libmalloc.so ./app` where app is the application you want to hijack

---
layout: post
title: Pthread setspecific segfault
date: 2023-04-27 00:24 +0200
---
During the last week I was stuck trying to figure out why openfoam was segfaulting when I run the application with the shared library that I built.
The shared library that I built would interpose itself over all the memory allocation calls that were made by the application.The library then decides to allocate the object to the appropriate memory device.
However to acheive this, the library depends on `dlsym` which looks for the next symbol for malloc/realloc/calloc and it returns the function pointer to allow us to invoke later.

Here is the error I encountered while running gdb.
```
_dlerror_run (operate=operate@entry=0x7ffff7bd20b0 <dlsym_doit>, args=args@entry=0x7fffffffbfe0)
    at dlerror.c:154
154	  if (result->errstring != NULL)
Missing separate debuginfos, use: dnf debuginfo-install libunwind-1.2.1-3.fc27.x86_64 libxml2-2.9.8-4.fc27.x86_64 numactl-libs-2.0.11-5.fc27.x86_64 xz-libs-5.2.3-4.fc27.x86_64 zlib-1.2.11-4.fc27.x86_64
(gdb) backtrace
#0  _dlerror_run (operate=operate@entry=0x7ffff7bd20b0 <dlsym_doit>, args=args@entry=0x7fffffffbfe0)
    at dlerror.c:154
#1  0x00007ffff7bd2141 in __dlsym (handle=handle@entry=0xffffffffffffffff, 
    name=name@entry=0x7ffff7878bf0 "malloc") at dlsym.c:70
#2  0x00007ffff77bdb6c in xxxxx::uninitialized_malloc (size=168) at ../../xxxxx.cxx:44
#3  0x00007ffff77bf14d in malloc (size=168) at ../../xxxxx.cxx:225
```
When we look at the source of glibc we see the following block
```
int
internal_function
_dlerror_run (void (*operate) (void *), void *args)
{
  struct dl_action_result *result;

  /* If we have not yet initialized the buffer do it now.  */
  __libc_once (once, init);

  /* Get error string and number.  */
  if (static_buf != NULL)
    result = static_buf;
  else
    {
      /* We don't use the static buffer and so we have a key.  Use it
	 to get the thread-specific buffer.  */
      result = __libc_getspecific (key);
      if (result == NULL)
	{
	  result = (struct dl_action_result *) calloc (1, sizeof (*result));
	  if (result == NULL)
	    /* We are out of memory.  Since this is no really critical
	       situation we carry on by using the global variable.
	       This might lead to conflicts between the threads but
	       they soon all will have memory problems.  */
	    result = &last_result;
	  else
	    /* Set the tsd.  */
	    __libc_setspecific (key, result);
	}
    }

  if (result->errstring != NULL)
    {
      /* Free the error string from the last failed command.  This can
	 happen if `dlerror' was not run after an error was found.  */
      if (result->malloced)
	free ((char *) result->errstring);
      result->errstring = NULL;
    }

  result->errcode = _dl_catch_error (&result->objname, &result->errstring,
				     &result->malloced, operate, args);

  /* If no error we mark that no error string is available.  */
  result->returned = result->errstring == NULL;

  return result->errstring != NULL;
}
```
Looking at the following line `result = __libc_getspecific (key);` we see that result is set to the value based on the value in the thread.
While debugging with gdb the value of `key` was 0 and the value returned from _libc_getspecific was not NULL but the value returned was not a valid `dl_action_result`, resulting in the segfault in the following line `if (result->errstring != NULL)`.

With the help of my colleague in BSC I was able to debug why the value was invalid.In the library we used a thread specific value for each pthread using the following api.
`int pthread_setspecific(pthread_key_t key, const void *value); `
The main issue with the usage of this api was that I didnt initialize the pthread_key_t struct, hence libc would set the key to value of 0 and the value was set to the second argument passed.

Looking back at the libc internal we can now see that value returned to `__libc_getspecific(key)` returned the value based earlier resulting in the segfault.
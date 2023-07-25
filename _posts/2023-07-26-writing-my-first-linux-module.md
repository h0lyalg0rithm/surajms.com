---
layout: post
title: Writing my first linux module
date: 2023-07-26 00:56 +0200
---
Last year I was watching an online course on operating systems on youtube,and one of the videos was on writing a kernel module.
I have been using a linux box for a while now but whenever I heard about a kernel, I always assumed that it was something complicated and way out of my league.

However since I had some time, I decided to give it a try.To write a barebones kernel module, here I how I went about it.
```
#include <linux/init.h>
#include <linux/module.h>
#include <linux/kernel.h>

MODULE_DESCRIPTION("Simple module");
MODULE_AUTHOR("Suraj Shirvankar");
MODULE_LICENSE("GPL");

static int init_module(void) {
  printk("Loaded kernel module");
  return 0;
}

static void exit_module(void) {
}

module_init(init_module);
module_exit(exit_module);
```
Then I had to create a `Makefile` to build the final kernel module

```
obj-m += test.o

all:
  make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules

clean:
  make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean
```
I had to make sure that the name of the object file matched the name of the file which contained the kernel code.
All this kernel module does is to print out in the log that it was loaded.

Next I tried to create a kernel module that would create a new proc file which would let us know the number of processes that are running.
This would allow us to run the following in the terminal.
```
#bash cat /proc/proc_count
40
```

Here is how I went about writting it.
```
#include <linux/module.h>
#include <linux/init.h>
#include <linux/kernel.h>
#include <linux/proc_fs.h>
#include <linux/seq_file.h>
#include <linux/sched.h>

MODULE_DESCRIPTION("Process count module");
MODULE_LICENSE("GPL");
MODULE_AUTHOR("Suraj Shirvankar");

struct proc_dir_entry *proc_entry;

static int proc_count(struct seq_file *seq, void *offset) {
	printk("Couting processes");
	struct task_struct *task_struct;
	int process_count = 0;
	for_each_process(task_struct){
		process_count += 1;
	}
	seq_printf(seq, "%d\n", process_count);
	return 0;
}
static int init_mod(void){
	printk("Loaded module to count processes");
	proc_entry = proc_create_single("proc_count", 0, NULL, proc_count);
	return 0;
}

static void exit_mod(void) {
    proc_remove(proc_entry);
}

module_init(init_mod);
module_exit(exit_mod);
```
Now if i run the following I get this as the result
```
cat /proc/proc_count 
625
```


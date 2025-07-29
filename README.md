# LINUX-SYSTEM-PROGRAMING_NOTES
## 1.Overview of Linux System

The complete Linux system is divided into 5 subsytems:

**i.Process Management Subsystem**
**ii.File Management Subsystem**
**iii.Device (Driver) Management Subsystem**
**iv.Memory Management Subsystem**
**v.Network Management Subsystem**

The single program that controls all these subsystems is called **Linux Kernal**.
## i.Process Management Subsystem
 **What is a Process?**
-A **Process** is a program in execution.For example:
-gcc file.c compiles source code gives a.out(binary file).
-When a.out is run, it becomes a **process**.
##### Memory layout of a process
When a process is loaded into **User Space RAM**, it occupies specific memory segments:Stack:-Top of memory(Function calls,local variables)
         Heap:-Dynamic memory allocation
         BSS:-Uninitialized global/static variables
         Data:-Initialized global/static variables
         Text:-Program code(binary)(Bottom of Memory)
## **User Space Vs Kernal Space**
**User Space**: Memory area where user applications run.
**Kernal Space**: Memory area where the Linux kernel executes and provides services.
## **Process Control Block **
Each process has a PCB (Process Control Block) created in kernel space. PCB contains information about the process:
i)PID (Process ID)
ii)PPID (Parent Process ID)
iii)File Descriptor Table
iv)Signal Disposition Table
V)Page Table
## **Creating a Process with `fork()`**
The `fork()` system call is used to create a new process. It creates a child process which is a copy of the parent process.
### Code Example:
```c
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>

int main() {
    pid_t pid = fork();
    if (pid == 0) {
        printf("This is the child process\n");
    } else {
        printf("This is the parent process\n");
    }
    return 0;
}
```
##### What happens during fork()

A new PCB is created for the child process.Memory (code, data, etc.) is logically duplicated (using Copy-On-Write).

-fork() returns:
-0 to the child process.
-PID of child to the parent process.




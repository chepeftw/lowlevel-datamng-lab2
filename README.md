# Laboratory 2

## Excercise 1

An operating system's *pid manager* is responsible for managing process identifiers. When a process is first created, it is assigned a unique pid by the pid manager. The pid is returned to the pid manager when the process completes execution, and the manager may later reassign this pid. Process identifiers are discussed more fully in Section 3.3.1. What is most important here is to recognize that process identifiers must be unique, no two active processes can have the same pid. 

Use the following constants to identify the range of possible pid values: 
```c
#define MIN_PID 300 
#define MAX_PID 5000
```
You may use any data structure of your choice to represent the availability of process identifiers. One strategy is to adopt what Linux has done and use a bitmap in which a value of 0 at position i indicates that a process id of value i is available and a value of 1 indicates that the process id is currently in use. 

Implement the following API for obtaining and releasing a pid:
```c
int allocate_ map (void)
```
- Creates and initializes a data structure for representing pids; returns -1 if unsuccessful, 1 if successful.

```c
int allocate_ pid (void)
```
- Allocates and returns a pid; returns -1 if unable to allocate a pid (all pids are in use) 

```c
void release_ pid (int pid)
```
- Releases a pid 


## Excercise 2

Write a multithread program that tests your solution of the previous excercise. You will create a numer of threads (e.g. 100) and each thread will request a pid, sleep for a random period of time, and then release the pod. On UNIX and Linux systems, sleeping is accomplished through the sleep() function, which is passed an integer value representing the number of seconds to sleep.

This program should test two cases:
- That all pids are used and unique.
- That pids rotate once you go beyond the maximum amount of available pids.

## Excercise 3

Modify the lab by ensuring that the data structure used to represent the availability of the pids is safe from race conditions. Use Pthreads mutex locks.

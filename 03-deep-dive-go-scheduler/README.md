# Deep Dive - Go Scheduler

- Go scheduler is part of the go runtime
- It is also known as M:N Scheduler
- Go runtime is part of the executable
- Go scheduler uses OS threads to schedule goroutines
- Goroutines run in context of OS Threads (they run on top of OS threads)
- Go runtime creates `GOMAXPROCS` no. of OS threads
- Scheduler schedules goroutines on those threads
- At any time, N no. of goroutines could be scheduled on M no. of OS threads

## Asynchronous Preemption
Go scheduler implements Asynchronous Preemption

### What is Asynchronous Preemption? /  Why do we need Preemption in Go?

- Without Preemption, if there are long-running goroutines in our program
- They would just hog the CPU and prevent other goroutines from being executed
- Preemption enables the scheduler to distribute running time among goroutines
- Asynchronous Preemption is triggered based on a time condition

### States of Goroutines
Just like OS Threads, goroutines have states:

1. Runnable State (When it is created)
2. Executing State (When it is scheduled in the OS thread)
3. If the goroutine is preempted, it's state becomes Runnable (it goes back the waiting queue)
4. Waiting State (If the goroutine is blocked because of some event)
5. Once the even which is causing the block is completed, goroutine moves back the runnable state

- Number of OS threads depend on the value of `GOMAXPROCS`
- Go runtime creates a logical processor and associates the OS thread with it
- The context switching between the goroutines is managed by the logical processor 

### How does context switching work when the goroutine makes a synchronous system call?
- A new OS Thread is created and the logical processor is detached from the previous OS thread to the new one

### How does context switching work when the goroutine makes an asynchronous system call?
- Go uses `netpoller` to handle asynchronous system calls
- `netpoller` uses the interface provided by the operating system to poll on the file descriptor and notifies the
goroutine to try I/O operation when it is ready
- This Application complexity of managing the asynchronous system calls is moved from the application to go runtime
- And it is managed efficiently

## Work Stealing
- If there are no goroutines in the local run queue
- Try to steal goroutines from the other logical processors
- If there are no goroutines found from the other logical processors, try to steal goroutine form global runnable queue
- If not found, then check the `netpoller`

Work stealing helps in better distribution of the goroutines across all logical processors

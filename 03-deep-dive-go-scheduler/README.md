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

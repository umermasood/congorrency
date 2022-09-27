# Goroutines
1. How does Go implement concurrency?
2. How does it overcome limitations of threads?

## Threads have their limitations
- The no. of threads we can create is limited
- Sharing memory among concurrent tasks leads to problems like race conditions and deadlocks



## Concurrency in Go is based on CSP
- Each process is built for sequential execution
- We do not share memory if have to share data among multiple processes
- We communicate data, by sending the copy of the data to other processes
- Since there is no sharing of memory, hence there is no deadlock or race conditions
- Scale more

Concurrency tools in Go:
1. Goroutines - Concurrently executing functions
2. Channels - are used for communicating data among goroutines
3. Select - is used to multiplex the channel
4. The `sync` package - provides classical synchronization tools

>**Go runtime is part of the executable. It is built-in to the executable of application**


## What are Goroutines?
1. Independently executing functions
2. Lightweight Threads
3. Run on top of actual OS threads
4. Greater than no. of OS threads
5. Go runtime optimally schedules goroutines

- The operating system schedules actual OS threads
- The go runtime schedules goroutines in the OS threads

---
## Start a goroutine
1. Use `go` keyword to start a function in a new goroutine
2. `go f(x)` starts a new goroutine which runs the function `f(x)`
3. Function `f` and value `x` are evaluated in the new goroutine
4. Goroutines share the same address space

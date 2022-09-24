# Goroutines

1. Independently executing functions
2. Lightweight Threads
3. Run on top of actual OS threads
4. Greater than no. of OS threads
5. Go runtime optimally schedules goroutines

---
## Start a goroutine
1. Use `go` keyword to start a function in a new goroutine
2. `go f(x)` starts a new goroutine which runs the function `f(x)`
3. Function `f` and value `x` are evaluated in the new goroutine
4. Goroutines share the same address space

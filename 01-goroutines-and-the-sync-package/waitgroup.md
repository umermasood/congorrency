# The sync.WaitGroup

What if we want to wait for other goroutines to finish their execution and then do something?

- We use sync.WaitGroup to wait for other goroutines to finish

## Three methods of sync.WaitGroup
1. `func (wg *WaitGroup) Add(delta int)`
2. `func (wg *WaitGroup) Wait()`
3. `func (wg *WaitGroup) Done()`

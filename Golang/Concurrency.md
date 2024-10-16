## Go concurrency
- Concurrent execution is the main draw of Golang
- We have stuff like `goroutines`, with are threads managed by the runtime
    - `goroutines` are extremely lightweight
- Goroutines are started as such:
```
go funcName() 

// This starts running the function funcName on a separate thread while the handler of this function runs on the original thread
// That is, the execution of funcName() happens in the new goroutine and the evaluation happen in the current goroutine
```
- We have mutexs, ie, *mutual exclusion*, to acquire locks and unlocks on any sort of data structures that needs to be thread-safe
    - Methods are `Lock()` and `Unlock()`
    ```
    / SafeCounter is safe to use concurrently.
    type SafeCounter struct {
        mu sync.Mutex
        v  map[string]int
    }

    // Increments the counter for the given key.
    func (c *SafeCounter) Inc(key string) {
        c.mu.Lock()
        // Lock so only one goroutine at a time can access the map c.v.
        c.v[key]++
        c.mu.Unlock()
    }

    // Value returns the current value of the counter for the given key.
    func (c *SafeCounter) Value(key string) int {
        c.mu.Lock()
        // Lock so only one goroutine at a time can access the map c.v.
        defer c.mu.Unlock()
        return c.v[key]
    }
    ```
- We also have something called `atomics` that is illustrated in this short video: https://www.youtube.com/shorts/iM06_ceOMQo
    - `atomics` are seeming used for int values while mutexs are used for others, such as struct, and is more common (Read comments)
    - Also, ***What is a race condition?***
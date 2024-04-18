# Goroutines

In Go, a goroutine is a lightweight thread of execution that allows concurrent execution of code. This tutorial covers goroutines in Go, including creating and using goroutines to run code concurrently.

## Creating Goroutines

To create a goroutine in Go, use the `go` keyword followed by a function call. Here's an example of creating and running a goroutine:

```go
package main

import (
    "fmt"
    "time"
)

func f(from string) {
    for i := 0; i < 3; i++ {
        fmt.Println(from, ":", i)
    }
}

func main() {
    // Run the function synchronously
    f("direct")

    // Run the function in a goroutine
    go f("goroutine")

    // Run an anonymous function in a goroutine
    go func(msg string) {
        fmt.Println(msg)
    }("going")

    // Wait for goroutines to finish (for demonstration purposes)
    time.Sleep(time.Second)
    fmt.Println("done")
}
```

In this example, the `f` function is called synchronously and in a goroutine. An anonymous function is also called in a goroutine.

## Concurrency with Goroutines

Goroutines enable concurrent execution of code, allowing multiple tasks to be performed simultaneously. Here's an example demonstrating the concurrent execution of multiple tasks:

```go
package main

import (
    "fmt"
    "time"
)

func task(id int) {
    for i := 0; i < 3; i++ {
        fmt.Printf("Task %d: %d\n", id, i)
        time.Sleep(time.Millisecond * 500)
    }
}

func main() {
    for i := 0; i < 3; i++ {
        go task(i)
    }
    time.Sleep(time.Second * 2) // Wait for goroutines to finish
    fmt.Println("All tasks completed")
}
```

In this example, the `task` function simulates a task with a delay. Three tasks are executed concurrently using goroutines.

## Concurrent Communication with Channels

Channels are a powerful mechanism for concurrent communication between goroutines. Here's an example demonstrating the use of channels for communication:

```go
package main

import (
    "fmt"
    "time"
)

func sender(ch chan<- int) {
    for i := 0; i < 5; i++ {
        fmt.Println("Sending:", i)
        ch <- i // Send value on channel
        time.Sleep(time.Millisecond * 500)
    }
    close(ch) // Close the channel after sending all values
}

func receiver(ch <-chan int) {
    for val := range ch {
        fmt.Println("Received:", val)
    }
}

func main() {
    ch := make(chan int) // Create an unbuffered channel
    go sender(ch)
    go receiver(ch)
    time.Sleep(time.Second * 3) // Wait for goroutines to finish
}
```

In this example, the `sender` function sends integers on a channel, and the `receiver` function receives them. Both functions run concurrently using goroutines.

## Conclusion

Goroutines in Go provide a powerful mechanism for concurrent programming. By running code in separate goroutines and communicating via channels, you can achieve concurrency and parallelism in your Go programs, improving performance and responsiveness.
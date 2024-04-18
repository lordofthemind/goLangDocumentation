# Concurrency Patterns

Concurrency patterns are essential for writing efficient and scalable concurrent programs in Go. This tutorial covers common concurrency patterns, including the worker pool pattern, fan-in/fan-out, and synchronization techniques.

## Worker Pool Pattern

The worker pool pattern involves creating a pool of worker goroutines to process tasks concurrently. Here's an example of implementing a worker pool pattern:

```go
package main

import (
    "fmt"
    "sync"
)

func worker(id int, jobs <-chan int, results chan<- int) {
    for j := range jobs {
        fmt.Println("Worker", id, "processing job", j)
        results <- j * 2 // Simulate processing the job
    }
}

func main() {
    const numJobs = 5
    const numWorkers = 3

    jobs := make(chan int, numJobs)
    results := make(chan int, numJobs)

    // Start worker goroutines
    var wg sync.WaitGroup
    for w := 1; w <= numWorkers; w++ {
        wg.Add(1)
        go func(workerID int) {
            defer wg.Done()
            worker(workerID, jobs, results)
        }(w)
    }

    // Send jobs to workers
    for j := 1; j <= numJobs; j++ {
        jobs <- j
    }
    close(jobs)

    // Collect results
    go func() {
        wg.Wait()
        close(results)
    }()

    // Print results
    for r := range results {
        fmt.Println("Result:", r)
    }
}
```

In this example, we create a pool of worker goroutines to process jobs concurrently. Each worker reads from a jobs channel, processes the job, and sends the result to a results channel.

### Worker Pool Pattern

In the worker pool pattern example:

1. We define a `worker` function that represents a worker goroutine. It takes an `id` to identify the worker, a `jobs` channel to receive tasks, and a `results` channel to send processed results.
2. Inside the `worker` function, we range over the `jobs` channel to receive tasks. For each task received, we process it (in this case, simply double the value of the task) and send the result to the `results` channel.
3. In the `main` function, we create channels for `jobs` and `results`.
4. We start multiple worker goroutines using a `WaitGroup` to coordinate their execution. Each goroutine processes tasks from the `jobs` channel and sends results to the `results` channel.
5. We then send tasks to the `jobs` channel and close it to signal that no more tasks will be sent.
6. We use another goroutine to wait for all worker goroutines to finish processing and close the `results` channel.
7. Finally, we range over the `results` channel to collect and print the processed results.


## Fan-in/Fan-out

Fan-in/fan-out is a pattern for parallelizing tasks by splitting work into multiple concurrent goroutines (fan-out) and then aggregating the results (fan-in). Here's an example of implementing fan-in/fan-out:

```go
package main

import (
    "fmt"
    "sync"
)

func producer(nums ...int) <-chan int {
    out := make(chan int)
    go func() {
        defer close(out)
        for _, num := range nums {
            out <- num
        }
    }()
    return out
}

func squareWorker(in <-chan int) <-chan int {
    out := make(chan int)
    go func() {
        defer close(out)
        for num := range in {
            out <- num * num
        }
    }()
    return out
}

func merge(cs ...<-chan int) <-chan int {
    var wg sync.WaitGroup
    out := make(chan int)

    // Start an output goroutine for each input channel in cs.
    output := func(c <-chan int) {
        defer wg.Done()
        for n := range c {
            out <- n
        }
    }
    wg.Add(len(cs))
    for _, c := range cs {
        go output(c)
    }

    // Wait for all the output goroutines to finish.
    go func() {
        wg.Wait()
        close(out)
    }()
    return out
}

func main() {
    nums := producer(1, 2, 3, 4, 5)
    sq1 := squareWorker(nums)
    sq2 := squareWorker(nums)

    // Fan-out: Two square workers processing the same input channel
    // Fan-in: Merging the results from both square workers
    results := merge(sq1, sq2)

    // Print results
    for r := range results {
        fmt.Println("Squared:", r)
    }
}
```

In this example, we use fan-out to create multiple square worker goroutines processing the same input channel concurrently. Then, we use fan-in to merge the results from all square workers into a single channel.

### Fan-in/Fan-out

In the fan-in/fan-out example:

1. We define a `producer` function that generates a stream of numbers and sends them to a channel.
2. We define a `squareWorker` function that receives numbers from a channel, squares them, and sends the squared results to a new channel.
3. We define a `merge` function that merges multiple input channels into a single output channel.
4. In the `main` function, we create a channel of numbers using the `producer` function.
5. We create two square worker channels (`sq1` and `sq2`) by passing the numbers channel to the `squareWorker` function twice. This demonstrates fan-out, where multiple goroutines process the same input concurrently.
6. We use the `merge` function to merge the results from `sq1` and `sq2` into a single channel (`results`). This demonstrates fan-in, where results from multiple goroutines are merged into a single channel.
7. Finally, we range over the `results` channel to collect and print the squared results.


## Conclusion

Concurrency patterns such as the worker pool pattern, fan-in/fan-out, and synchronization techniques are essential for writing efficient and scalable concurrent programs in Go. By understanding and applying these patterns, you can take full advantage of Go's concurrency features and build robust concurrent applications.
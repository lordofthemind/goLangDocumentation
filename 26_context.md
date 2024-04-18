# Using Context in Go

The `context` package in Go provides a powerful mechanism for managing deadlines, cancellation, and request-scoped values. In this tutorial, we'll cover how to use the `context` package effectively.

## Managing Deadlines

You can use contexts to set deadlines for operations and cancel them if they exceed the specified time limit.

```go
package main

import (
    "context"
    "fmt"
    "time"
)

func main() {
    ctx, cancel := context.WithTimeout(context.Background(), 3*time.Second)
    defer cancel()

    select {
    case <-time.After(2 * time.Second):
        fmt.Println("Operation completed successfully.")
    case <-ctx.Done():
        fmt.Println("Operation timed out:", ctx.Err())
    }
}
```

### Output

If the operation completes within 2 seconds:

```
Operation completed successfully.
```

If the operation exceeds the deadline (3 seconds):

```
Operation timed out: context deadline exceeded
```

## Cancellation

Contexts can be used to cancel operations when they are no longer needed, preventing unnecessary work.

```go
package main

import (
    "context"
    "fmt"
    "time"
)

func main() {
    ctx, cancel := context.WithCancel(context.Background())
    defer cancel()

    go func() {
        time.Sleep(2 * time.Second)
        cancel() // Cancel the operation after 2 seconds
    }()

    select {
    case <-time.After(3 * time.Second):
        fmt.Println("Operation completed successfully.")
    case <-ctx.Done():
        fmt.Println("Operation canceled:", ctx.Err())
    }
}
```

### Output

If the operation completes before cancellation:

```
Operation completed successfully.
```

If the operation is canceled:

```
Operation canceled: context canceled
```

## Request-Scoped Values

Contexts can carry request-scoped values across API boundaries, allowing you to pass request-specific data without modifying function signatures.

```go
package main

import (
    "context"
    "fmt"
)

type key string

func main() {
    ctx := context.WithValue(context.Background(), key("userID"), 123)

    // Retrieve the value from the context
    if userID, ok := ctx.Value(key("userID")).(int); ok {
        fmt.Println("User ID:", userID)
    } else {
        fmt.Println("User ID not found in context.")
    }
}
```

### Output

```
User ID: 123
```

## Conclusion

The `context` package in Go is a powerful tool for managing deadlines, cancellation, and request-scoped values. By understanding and utilizing contexts effectively, you can build more robust and scalable applications.
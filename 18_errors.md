# Errors

In Go, it's common to communicate errors via an explicit, separate return value. This approach makes it easy to handle errors using the same language constructs as other tasks. This tutorial covers error handling in Go, including returning errors, sentinel errors, wrapping errors, and checking errors.

## Returning Errors

In Go, errors are communicated via an explicit, separate return value. By convention, errors are the last return value and have type `error`, a built-in interface.

```go
package main

import (
    "errors"
    "fmt"
)

func f(arg int) (int, error) {
    if arg == 42 {
        return -1, errors.New("can't work with 42")
    }
    return arg + 3, nil
}
```

In this example, the `f` function returns an error if the input argument is equal to 42.

## Sentinel Errors

Sentinel errors are predeclared variables used to signify specific error conditions.

```go
var ErrOutOfTea = fmt.Errorf("no more tea available")
var ErrPower = fmt.Errorf("can't boil water")
```

In this example, `ErrOutOfTea` and `ErrPower` are sentinel errors used to represent specific error conditions.

## Wrapping Errors

Errors in Go can be wrapped with higher-level errors to add context. This is done using the `%w` verb in `fmt.Errorf`.

```go
func makeTea(arg int) error {
    if arg == 2 {
        return ErrOutOfTea
    } else if arg == 4 {
        return fmt.Errorf("making tea: %w", ErrPower)
    }
    return nil
}
```

In this example, the `makeTea` function returns wrapped errors to provide additional context.

## Handling Errors

Errors in Go are commonly handled using inline error checks.

```go
for _, i := range []int{7, 42} {
    if r, e := f(i); e != nil {
        fmt.Println("f failed:", e)
    } else {
        fmt.Println("f worked:", r)
    }
}
```

In this example, we handle errors returned by the `f` function using an inline error check.

```go
for i := range 5 {
    if err := makeTea(i); err != nil {
        if errors.Is(err, ErrOutOfTea) {
            fmt.Println("We should buy new tea!")
        } else if errors.Is(err, ErrPower) {
            fmt.Println("Now it is dark.")
        } else {
            fmt.Printf("unknown error: %s\n", err)
        }
        continue
    }
    fmt.Println("Tea is ready!")
}
```

Here, we use the `errors.Is` function to check for specific error conditions, such as `ErrOutOfTea` or `ErrPower`.

## Conclusion

In Go, error handling is straightforward and idiomatic. By following conventions and using language features like sentinel errors and error wrapping, you can write clean and reliable error-handling code.
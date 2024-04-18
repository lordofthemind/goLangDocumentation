# Testing in Go

Testing is an essential part of software development in Go. In this tutorial, we'll cover various aspects of testing, including writing unit tests, table-driven tests, and benchmarking.

## Unit Tests

Unit tests in Go are written using the built-in `testing` package. Let's start with a simple example of writing a unit test for a function.

### Example: Testing a Simple Function

Suppose we have a function `Add` that adds two integers:

```go
package math

func Add(a, b int) int {
    return a + b
}
```

We can write a unit test for this function as follows:

```go
package math

import "testing"

func TestAdd(t *testing.T) {
    result := Add(2, 3)
    if result != 5 {
        t.Errorf("Add(2, 3) = %d; want 5", result)
    }
}
```

In this test, we use the `testing.T` type to report test failures. We call the `Add` function with inputs `2` and `3` and check if the result is `5`. If the result is not as expected, we use `t.Errorf` to report the error.

### Output

```
$ go test ./math
PASS
```

The output indicates that the test passed successfully.

## Table-Driven Tests

Table-driven tests allow us to test a function with multiple inputs and expected outputs using a table of test cases. Let's extend the previous example with a table-driven test.

### Example: Table-Driven Test

```go
package math

import "testing"

func TestAdd(t *testing.T) {
    cases := []struct {
        a, b, want int
    }{
        {2, 3, 5},
        {0, 0, 0},
        {-1, 1, 0},
        {10, -5, 5},
    }
    for _, tc := range cases {
        got := Add(tc.a, tc.b)
        if got != tc.want {
            t.Errorf("Add(%d, %d) = %d; want %d", tc.a, tc.b, got, tc.want)
        }
    }
}
```

In this test, we define a slice of structs where each struct represents a test case. We iterate over the test cases and call the `Add` function with the input values. We then compare the result with the expected output for each test case.

### Output

```
$ go test ./math
PASS
```

The output indicates that all test cases passed successfully.

## Benchmarking

Benchmarking in Go is used to measure the performance of functions. Let's write a simple benchmark for the `Add` function.

### Example: Benchmarking

```go
package math

import "testing"

func BenchmarkAdd(b *testing.B) {
    for i := 0; i < b.N; i++ {
        Add(2, 3)
    }
}
```

In this benchmark, we use the `testing.B` type to run the benchmark `b.N` times. The benchmark measures the time taken to execute the `Add` function repeatedly.

### Output

```
$ go test -bench=.
BenchmarkAdd-8   	1000000000	         0.278 ns/op
```

The output shows the benchmark results, including the number of iterations (`1000000000`) and the time taken per iteration (`0.278 ns/op`).

## Conclusion

In this tutorial, we covered writing unit tests, table-driven tests, and benchmarking in Go. Testing is crucial for ensuring the correctness and performance of your code.
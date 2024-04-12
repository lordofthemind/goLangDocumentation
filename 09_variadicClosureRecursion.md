# Variadic Functions

Variadic functions in Go allow you to define functions that can accept any number of trailing arguments. This tutorial demonstrates how to define and use variadic functions in Go.

## Defining Variadic Functions

In Go, variadic functions are defined using the ellipsis (`...`) syntax before the type of the last parameter in the function signature. Here's an example of a variadic function `sum` that takes an arbitrary number of integers as arguments:

```go
func sum(nums ...int) {
    fmt.Print(nums, " ")
    total := 0
    for _, num := range nums {
        total += num
    }
    fmt.Println(total)
}
```

Within the function body, the type of `nums` is equivalent to `[]int`. This means you can treat `nums` like a slice, allowing operations such as finding its length (`len(nums)`) or iterating over it using `range`.

## Using Variadic Functions

Variadic functions can be called in the usual way with individual arguments. Here's how to call the `sum` function with different numbers of arguments:

```go
sum(1, 2)
sum(1, 2, 3)
```

If you already have multiple arguments stored in a slice, you can pass them to a variadic function using the `function(slice...)` syntax. Here's how to call the `sum` function with a slice of integers:

```go
nums := []int{1, 2, 3, 4}
sum(nums...)
```

The output of the above code will be:

```
[1 2] 3
[1 2 3] 6
[1 2 3 4] 10
```

## Conclusion

Variadic functions are a convenient feature in Go, allowing functions to accept any number of arguments. They are commonly used in standard library functions like `fmt.Println`. Understanding how to define and use variadic functions is essential for writing flexible and reusable code in Go.

# Closures

Closures are a powerful feature in Go that allows functions to capture and manipulate the variables from the surrounding context. This tutorial explores closures in Go, including how to define and use them effectively.

## Defining Closures

In Go, anonymous functions can form closures. These anonymous functions are useful when you want to define a function inline without naming it. Here's an example of defining a closure using an anonymous function within another function:

```go
func intSeq() func() int {
    i := 0
    return func() int {
        i++
        return i
    }
}
```

In the `intSeq` function, an anonymous function is defined and returned. This anonymous function captures the variable `i` from the outer scope to form a closure.

## Using Closures

Once a closure is defined, it can be called like any other function. Here's how to use the `intSeq` closure:

```go
nextInt := intSeq()
fmt.Println(nextInt()) // Output: 1
fmt.Println(nextInt()) // Output: 2
fmt.Println(nextInt()) // Output: 3
```

In the above code, the `nextInt` closure is called multiple times, and it maintains its own state, incrementing `i` with each call.

To confirm that the state is unique to each closure, you can create and test a new one:

```go
newInts := intSeq()
fmt.Println(newInts()) // Output: 1
```

## Conclusion

Closures in Go provide a powerful mechanism for encapsulating state within functions. They are particularly useful for creating functions with persistent local variables that retain their state between calls.

Understanding how closures work and how to use them effectively is essential for writing clean and idiomatic Go code.

# Recursion

Recursion is a programming technique where a function calls itself directly or indirectly to solve a problem. Go supports recursive functions, allowing you to write elegant and concise solutions to certain types of problems. This tutorial explores recursion in Go, including classic examples and considerations for using recursive functions.

## Classic Example: Factorial Function

A classic example of recursion is the factorial function, which calculates the factorial of a non-negative integer. Here's an implementation of the factorial function in Go:

```go
func fact(n int) int {
    if n == 0 {
        return 1
    }
    return n * fact(n-1)
}
```

In this implementation, the `fact` function calls itself recursively until it reaches the base case `n == 0`, at which point it returns 1.

## Using Recursion

Once a recursive function is defined, it can be called like any other function. Here's how to use the `fact` function to calculate the factorial of a number:

```go
fmt.Println(fact(7)) // Output: 5040
```

## Recursive Closures

Closures in Go can also be recursive, but they require the closure to be declared with a typed variable explicitly before it's defined. Here's an example of a recursive closure for calculating Fibonacci numbers:

```go
var fib func(n int) int
fib = func(n int) int {
    if n < 2 {
        return n
    }
    return fib(n-1) + fib(n-2)
}
```

In this example, the `fib` closure is declared with a typed variable `fib` before it's defined. This allows the closure to call itself recursively.

## Conclusion

Recursion is a powerful technique in programming, allowing you to solve certain types of problems elegantly and efficiently. However, it's essential to use recursion judiciously, as it can lead to stack overflow errors if not used correctly.

Understanding how recursion works and when to use it is an important skill for any programmer. With practice and experience, you can leverage recursion to write clean and efficient code in Go.
# Example
## For Loop

`for` is Go’s only looping construct. Here are some basic types of `for` loops.

```go
package main

import "fmt"

func main() {
    // The most basic type, with a single condition.
    i := 1
    for i <= 3 {
        fmt.Println(i)
        i = i + 1
    }

    // A classic initial/condition/after `for` loop.
    for j := 0; j < 3; j++ {
        fmt.Println(j)
    }

    // Another way of accomplishing the basic “do this N times” iteration is to range over an integer.
    for i := range [3]int{} {
        fmt.Println("range", i)
    }

    // `for` without a condition will loop repeatedly until you break out of the loop or return from the enclosing function.
    for {
        fmt.Println("loop")
        break
    }

    // You can also continue to the next iteration of the loop.
    for n := range [6]int{} {
        if n%2 == 0 {
            continue
        }
        fmt.Println(n)
    }
}
```

Output when run:

```
1
2
3
0
1
2
range 0
range 1
range 2
loop
1
3
5
```

This program demonstrates various types of `for` loops in Go:

- The most basic type with a single condition.
- A classic initial/condition/after `for` loop.
- Using `range` over an integer for a fixed number of iterations.
- Using `for` without a condition to create an infinite loop.
- Using `continue` to skip the current iteration of the loop.

You can run this program using `go run for.go` in your terminal to see the output.

## If/Else

Branching with `if` and `else` in Go is straightforward. Here's a basic example:

```go
package main

import "fmt"

func main() {
    // Here’s a basic example.
    if 7%2 == 0 {
        fmt.Println("7 is even")
    } else {
        fmt.Println("7 is odd")
    }

    // You can have an if statement without an else.
    if 8%4 == 0 {
        fmt.Println("8 is divisible by 4")
    }

    // Logical operators like && and || are often useful in conditions.
    if 8%2 == 0 || 7%2 == 0 {
        fmt.Println("either 8 or 7 are even")
    }

    // A statement can precede conditionals; any variables declared in this statement are available in the current and all subsequent branches.
    if num := 9; num < 0 {
        fmt.Println(num, "is negative")
    } else if num < 10 {
        fmt.Println(num, "has 1 digit")
    } else {
        fmt.Println(num, "has multiple digits")
    }
}
```

Output when run:

```
7 is odd
8 is divisible by 4
either 8 or 7 are even
9 has 1 digit
```

This program demonstrates branching with `if` and `else` statements in Go:

- Basic `if` and `else` condition.
- `if` statement without an `else`.
- Usage of logical operators (`&&` and `||`) in conditions.
- Declaring variables in an `if` statement; these variables are available in the current and all subsequent branches.

You can run this program using `go run if-else.go` in your terminal to see the output.

Note that you don’t need parentheses around conditions in Go, but braces are required.

There is no ternary `if` in Go, so you’ll need to use a full `if` statement even for basic conditions.

## Switch

Switch statements in Go express conditionals across many branches. Here's an example:

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    // Here’s a basic switch.
    i := 2
    fmt.Print("Write ", i, " as ")
    switch i {
    case 1:
        fmt.Println("one")
    case 2:
        fmt.Println("two")
    case 3:
        fmt.Println("three")
    }

    // You can use commas to separate multiple expressions in the same case statement.
    // We use the optional default case in this example as well.
    switch time.Now().Weekday() {
    case time.Saturday, time.Sunday:
        fmt.Println("It's the weekend")
    default:
        fmt.Println("It's a weekday")
    }

    // Switch without an expression is an alternate way to express if/else logic.
    // Here we also show how the case expressions can be non-constants.
    t := time.Now()
    switch {
    case t.Hour() < 12:
        fmt.Println("It's before noon")
    default:
        fmt.Println("It's after noon")
    }

    // A type switch compares types instead of values.
    // You can use this to discover the type of an interface value.
    // In this example, the variable t will have the type corresponding to its clause.
    whatAmI := func(i interface{}) {
        switch t := i.(type) {
        case bool:
            fmt.Println("I'm a bool")
        case int:
            fmt.Println("I'm an int")
        default:
            fmt.Printf("Don't know type %T\n", t)
        }
    }
    whatAmI(true)
    whatAmI(1)
    whatAmI("hey")
}
```

Output when run:

```
Write 2 as two
It's a weekday
It's after noon
I'm a bool
I'm an int
Don't know type string
```

This program demonstrates various use cases of `switch` statements in Go:

- Basic `switch` statement with cases for different values.
- Using commas to separate multiple expressions in the same `case` statement.
- Using the optional `default` case.
- Switch without an expression as an alternate way to express if/else logic.
- A type switch to discover the type of an interface value.

You can run this program using `go run switch.go` in your terminal to see the output.
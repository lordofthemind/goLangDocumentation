# Methods

In Go, methods provide a way to associate functions with specific types, allowing you to define behavior that operates on instances of those types. This tutorial covers methods in Go, including method definitions, receivers, and embedded types.

## Part 1: Methods

Methods in Go are special functions associated with a particular type. They enhance the functionality of structs by allowing you to define behavior specific to those types.

### Method Definition

You can define a method for a struct like this:

```go
type Circle struct {
    x, y, r float64
}

func (c *Circle) area() float64 {
    return math.Pi * c.r * c.r
}
```

Here, `(c *Circle)` is the receiver, indicating that `area()` is a method of the `Circle` type.

### Calling Methods

You can call the method using the `.` operator:

```go
c := Circle{0, 0, 5}
fmt.Println(c.area())
```

### Embedded Types

Go supports embedded types, allowing you to create relationships between structs. For example:

```go
type Android struct {
    Person
    Model string
}
```

This defines an `Android` struct with an embedded `Person` type, enabling methods of `Person` to be directly called on `Android` instances.

## Part 2: Example

Here's an example illustrating methods in Go:

```go
package main

import "fmt"

type rect struct {
    width, height int
}

// Method with a pointer receiver
func (r *rect) area() int {
    return r.width * r.height
}

// Method with a value receiver
func (r rect) perim() int {
    return 2*r.width + 2*r.height
}

func main() {
    r := rect{width: 10, height: 5}

    // Calling methods
    fmt.Println("Area:", r.area())
    fmt.Println("Perimeter:", r.perim())

    // Using pointer receiver for method call
    rp := &r
    fmt.Println("Area (with pointer receiver):", rp.area())
    fmt.Println("Perimeter (with pointer receiver):", rp.perim())
}
```

In this example, we define methods `area()` and `perim()` for the `rect` type, demonstrating both pointer and value receivers.

Methods in Go provide a powerful way to extend the behavior of types and enhance code readability.
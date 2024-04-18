# Interfaces

In Go, interfaces provide a way to define collections of method signatures, allowing different types to implement those methods. This tutorial covers interfaces in Go, including interface definitions, implementations, and usage.

## Part 1: Interfaces

Interfaces in Go specify a set of method signatures that a type must implement. Let's explore how interfaces are defined, implemented, and used.

### Interface Definition

Here's a basic example of defining an interface for geometric shapes:

```go
package main

import (
    "fmt"
    "math"
)

type geometry interface {
    area() float64
    perim() float64
}
```

### Implementing Interfaces

Types in Go implement interfaces implicitly. Here, we implement the `geometry` interface for `rect` and `circle` types:

```go
type rect struct {
    width, height float64
}

func (r rect) area() float64 {
    return r.width * r.height
}

func (r rect) perim() float64 {
    return 2*r.width + 2*r.height
}

type circle struct {
    radius float64
}

func (c circle) area() float64 {
    return math.Pi * c.radius * c.radius
}

func (c circle) perim() float64 {
    return 2 * math.Pi * c.radius
}
```

### Using Interfaces

We can define functions that accept interface types as arguments, allowing them to work with any type that implements the interface:

```go
func measure(g geometry) {
    fmt.Println(g)
    fmt.Println(g.area())
    fmt.Println(g.perim())
}

func main() {
    r := rect{width: 3, height: 4}
    c := circle{radius: 5}

    measure(r)
    measure(c)
}
```

## Part 2: Interfaces Continued

Interfaces in Go allow you to define common behaviors that different types can implement. Let's continue exploring interfaces.

### Implicit Implementation

In Go, types implicitly implement interfaces if they define all the methods required by the interface. This allows for flexible usage of interfaces across different types.

### Using Interfaces in Functions

Functions can accept interface types as arguments, allowing them to work with any type that implements the interface. For example, a `totalArea` function can calculate the total area of multiple shapes:

```go
func totalArea(shapes ...Shape) float64 {
    var area float64
    for _, s := range shapes {
        area += s.area()
    }
    return area
}
```

### Using Interfaces as Fields

Interfaces can also be used as fields in structs. This allows for even more flexibility in defining composite types. For example, a `MultiShape` struct can contain shapes of different types:

```go
type MultiShape struct {
    shapes []Shape
}
```

### Conclusion

Interfaces in Go provide a powerful way to define common behaviors across different types, enabling flexible and modular code design.
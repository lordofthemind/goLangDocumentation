# Structs

In Go, a struct is a composite data type that groups together zero or more fields of arbitrary types. It allows you to create more complex data structures by combining simpler types. Let's explore structs and how to use them in Go.

## Definition of Structs

An example of defining a struct in Go:

```go
type Circle struct {
    x, y, r float64
}
```

Here, `Circle` is a struct type with three fields: `x`, `y`, and `r`, each of type `float64`.

## Initialization of Structs

There are multiple ways to initialize a struct in Go:

1. Using the `var` keyword:

```go
var c Circle
```

This creates a local `Circle` variable initialized with zero values for each field.

2. Using the `new` function:

```go
c := new(Circle)
```

This allocates memory for all fields, sets each of them to their zero value, and returns a pointer to the struct.

3. With field values:

```go
c := Circle{x: 0, y: 0, r: 5}
```

or without field names if the order is known:

```go
c := Circle{0, 0, 5}
```

## Accessing Struct Fields

Struct fields are accessed using the `.` operator:

```go
fmt.Println(c.x, c.y, c.r)
```

## Passing Structs to Functions

Functions can take structs as arguments. By default, arguments are passed by value in Go, meaning a copy of the struct is made. If modifications are needed, pass a pointer to the struct:

```go
func circleArea(c Circle) float64 {
    return math.Pi * c.r * c.r
}
```

Call the function like this:

```go
c := Circle{0, 0, 5}
fmt.Println(circleArea(c))
```

If modifications are expected, pass a pointer to the struct:

```go
func circleArea(c *Circle) float64 {
    return math.Pi * c.r * c.r
}
```

Call the function with the address of the struct:

```go
c := Circle{0, 0, 5}
fmt.Println(circleArea(&c))
```

Remember, structs in Go are passed by value, so modifying fields within a function will not affect the original struct unless passed by pointer.

This concludes our overview of structs in Go. Structs are versatile and powerful, allowing you to create complex data structures to suit your needs.
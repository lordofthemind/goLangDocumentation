# Generics

Starting from version 1.18, Go has introduced support for generics, allowing you to write more flexible and reusable code. This tutorial covers generics in Go, including generic functions and types.

## Generic Functions

In Go, generic functions can operate on values of any type. Here's an example of a generic function `MapKeys`, which takes a map of any type and returns a slice of its keys:

```go
package main

import "fmt"

func MapKeys[K comparable, V any](m map[K]V) []K {
    r := make([]K, 0, len(m))
    for k := range m {
        r = append(r, k)
    }
    return r
}
```

In this example, `K` and `V` are type parameters. `K` has the comparable constraint, ensuring that keys can be compared with `==` and `!=` operators. `V` has the any constraint, allowing any type.

## Generic Types

Go also supports generic types. Here's an example of a generic type `List`, which is a singly-linked list with values of any type:

```go
type List[T any] struct {
    head, tail *element[T]
}

type element[T any] struct {
    next *element[T]
    val  T
}
```

In this example, `T` is a type parameter, allowing the `List` type to hold values of any type.

## Generic Methods

You can define methods on generic types just like you do on regular types. Here's how you can define methods `Push` and `GetAll` on the `List` type:

```go
func (lst *List[T]) Push(v T) {
    // Method implementation
}

func (lst *List[T]) GetAll() []T {
    // Method implementation
}
```

## Using Generics

When invoking generic functions or methods, you can often rely on type inference. Here's how you can use the `MapKeys` function and `List` type:

```go
var m = map[int]string{1: "2", 2: "4", 4: "8"}
fmt.Println("keys:", MapKeys(m))

lst := List[int]{}
lst.Push(10)
lst.Push(13)
lst.Push(23)
fmt.Println("list:", lst.GetAll())
```

In this example, the compiler infers the types for `MapKeys` automatically based on the provided map. Similarly, when using methods on the `List` type, you can provide the type explicitly or rely on type inference.

## Conclusion

Generics in Go provide a powerful tool for writing more flexible and reusable code. By using generic functions and types, you can write code that works with a wide range of types, leading to cleaner and more concise programs.
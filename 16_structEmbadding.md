# Struct Embedding

In Go, struct embedding allows you to include one struct type within another, enabling composition of types and reusing their fields and methods. This tutorial covers struct embedding in Go, including embedding syntax, initialization, accessing embedded fields and methods, and interface implementation.

## Struct Embedding

Struct embedding in Go allows one struct type to be included within another struct type. This enables the embedding struct to inherit fields and methods from the embedded struct.

### Syntax

In Go, embedding a struct is achieved by declaring a field within a struct without specifying a name for the field. Here's an example:

```go
package main

import "fmt"

type base struct {
    num int
}

type container struct {
    base
    str string
}
```

In this example, the `container` struct embeds the `base` struct without specifying a field name.

### Initialization

When creating a struct with embedded fields, you need to explicitly initialize the embedded type. Here's how you can initialize a `container`:

```go
co := container{
    base: base{
        num: 1,
    },
    str: "some name",
}
```

### Accessing Embedded Fields

You can access the embedded fields directly on the embedding struct, or by specifying the full path using the embedded type name. For example:

```go
fmt.Printf("co={num: %v, str: %v}\n", co.num, co.str)
fmt.Println("also num:", co.base.num)
```

### Accessing Embedded Methods

Methods defined on the embedded struct become methods of the embedding struct. You can invoke these methods directly on the embedding struct. For example:

```go
fmt.Println("describe:", co.describe())
```

### Interface Implementation

Embedding structs with methods can be used to implement interfaces on other structs. In the example, the `container` struct implements the `describer` interface because it embeds the `base` struct, which implements the `describe()` method.

```go
var d describer = co
fmt.Println("describer:", d.describe())
```

## Conclusion

Struct embedding in Go provides a powerful mechanism for code reuse and composition. By embedding structs, you can create complex types that inherit behavior from other types, leading to cleaner and more maintainable code.
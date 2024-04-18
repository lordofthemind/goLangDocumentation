# Reflection in Go

Reflection is a powerful feature in Go that allows you to examine and manipulate the type, structure, and values of variables at runtime. While it's not commonly used in day-to-day programming, understanding reflection can be valuable for tasks like serialization, deserialization, and dynamic method invocation.

## Basics of Reflection

Reflection in Go is provided by the `reflect` package. Let's start with a simple example to demonstrate how reflection works.

```go
package main

import (
    "fmt"
    "reflect"
)

func main() {
    var x float64 = 3.14
    fmt.Println("Type of x:", reflect.TypeOf(x))
    fmt.Println("Value of x:", reflect.ValueOf(x))
}
```

In this example, we declare a variable `x` of type `float64`. Using reflection, we print the type and value of `x`.

### Output:

```
Type of x: float64
Value of x: 3.14
```

Here, `reflect.TypeOf(x)` returns the type of `x`, and `reflect.ValueOf(x)` returns the value of `x` as a `reflect.Value` struct.

## Accessing Struct Field Tags

Reflection is particularly useful when working with structs, as it allows you to access struct field tags dynamically. Let's see an example:

```go
package main

import (
    "fmt"
    "reflect"
)

type Person struct {
    Name string `json:"name"`
    Age  int    `json:"age"`
}

func main() {
    p := Person{Name: "John", Age: 30}

    t := reflect.TypeOf(p)
    for i := 0; i < t.NumField(); i++ {
        field := t.Field(i)
        fmt.Printf("Field: %s, Tag: %s\n", field.Name, field.Tag.Get("json"))
    }
}
```

In this example, we define a `Person` struct with `Name` and `Age` fields, each tagged with `json`. We then use reflection to iterate over the struct fields and print the field names along with their JSON tags.

### Output:

```
Field: Name, Tag: name
Field: Age, Tag: age
```

Here, `field.Tag.Get("json")` retrieves the value of the `json` tag associated with each struct field.

## Conclusion

Reflection in Go provides a powerful mechanism for inspecting and manipulating variables at runtime. While it should be used judiciously due to its potential performance overhead and complexity, it can be invaluable for certain tasks where dynamic behavior is required.
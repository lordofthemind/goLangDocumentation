# JSON Handling in Go

JSON (JavaScript Object Notation) is a popular format for data interchange. Go provides built-in support for marshaling (encoding) and unmarshaling (decoding) JSON data. In this tutorial, we'll cover how to handle JSON data in Go, including marshaling, unmarshaling, working with nested structures, and using JSON tags.

## Marshaling and Unmarshaling

### Marshaling

Marshaling is the process of converting Go data structures into JSON format. Go provides the `json.Marshal` function for this purpose.

```go
package main

import (
    "encoding/json"
    "fmt"
)

type Person struct {
    Name string
    Age  int
}

func main() {
    person := Person{Name: "John", Age: 30}
    jsonData, err := json.Marshal(person)
    if err != nil {
        fmt.Println("Error marshaling JSON:", err)
        return
    }
    fmt.Println(string(jsonData))
}
```

In this example, we define a `Person` struct and create an instance of it. We then use `json.Marshal` to convert the `person` struct into JSON format. The `string(jsonData)` converts the byte slice into a string for printing.

### Output

```
{"Name":"John","Age":30}
```

### Unmarshaling

Unmarshaling is the process of converting JSON data into Go data structures. Go provides the `json.Unmarshal` function for this purpose.

```go
package main

import (
    "encoding/json"
    "fmt"
)

type Person struct {
    Name string
    Age  int
}

func main() {
    jsonData := []byte(`{"Name":"Alice","Age":25}`)
    var person Person
    err := json.Unmarshal(jsonData, &person)
    if err != nil {
        fmt.Println("Error unmarshaling JSON:", err)
        return
    }
    fmt.Println("Name:", person.Name)
    fmt.Println("Age:", person.Age)
}
```

In this example, we have JSON data representing a person. We use `json.Unmarshal` to convert the JSON data into a `Person` struct.

### Output

```
Name: Alice
Age: 25
```

## Nested Structures

JSON data can represent nested structures, such as arrays and objects. Go supports handling nested structures easily.

### Example: Nested Structures

```go
package main

import (
    "encoding/json"
    "fmt"
)

type Address struct {
    City  string
    State string
}

type Person struct {
    Name    string
    Age     int
    Address Address
}

func main() {
    jsonData := []byte(`{"Name":"Bob","Age":35,"Address":{"City":"New York","State":"NY"}}`)
    var person Person
    err := json.Unmarshal(jsonData, &person)
    if err != nil {
        fmt.Println("Error unmarshaling JSON:", err)
        return
    }
    fmt.Println("Name:", person.Name)
    fmt.Println("Age:", person.Age)
    fmt.Println("City:", person.Address.City)
    fmt.Println("State:", person.Address.State)
}
```

In this example, we have JSON data representing a person with an address. We define nested structs (`Person` and `Address`) to represent this structure.

### Output

```
Name: Bob
Age: 35
City: New York
State: NY
```

## JSON Tags

JSON tags allow us to customize the JSON representation of Go struct fields. We can specify field names, omitempty, and other options using tags.

### Example: JSON Tags

```go
package main

import (
    "encoding/json"
    "fmt"
)

type Person struct {
    Name string `json:"fullName"`
    Age  int    `json:"years,omitempty"`
}

func main() {
    person := Person{Name: "Emily"}
    jsonData, err := json.Marshal(person)
    if err != nil {
        fmt.Println("Error marshaling JSON:", err)
        return
    }
    fmt.Println(string(jsonData))
}
```

In this example, we use JSON tags to customize the field names and specify the `omitempty` option for the `Age` field.

### Output

```
{"fullName":"Emily"}
```

## Conclusion

In this tutorial, we covered how to marshal and unmarshal JSON data in Go, handle nested structures, and use JSON tags. Understanding JSON handling in Go is essential for working with JSON data effectively.
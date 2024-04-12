# Range

The `range` keyword in Go is used to iterate over elements in various data structures. This tutorial demonstrates how to use `range` with different data structures in Go.

## Using `range` with Slices

The `range` keyword can be used to iterate over elements in slices. Here's an example of summing the numbers in a slice:

```go
nums := []int{2, 3, 4}
sum := 0
for _, num := range nums {
    sum += num
}
fmt.Println("sum:", sum)
```

In the above code, `range` iterates over each element in the `nums` slice, providing both the index and the value. We use `_` to ignore the index since we only need the value.

## Accessing Index and Value

If we need to access both the index and the value, we can modify the loop as follows:

```go
for i, num := range nums {
    if num == 3 {
        fmt.Println("index:", i)
    }
}
```

This will print the index of the element with the value `3`.

## Using `range` with Maps

In Go, `range` can also iterate over key/value pairs in maps. Here's an example:

```go
kvs := map[string]string{"a": "apple", "b": "banana"}
for k, v := range kvs {
    fmt.Printf("%s -> %s\n", k, v)
}
```

This code snippet prints each key/value pair in the `kvs` map.

We can also iterate over just the keys of a map using `range`:

```go
for k := range kvs {
    fmt.Println("key:", k)
}
```

## Using `range` with Strings

In Go, `range` can iterate over Unicode code points in strings. Here's how:

```go
for i, c := range "go" {
    fmt.Println(i, c)
}
```

This code snippet prints the index and Unicode code point of each character in the string "go".

## Output

When you run the code provided, you should see the following output:

```
sum: 9
index: 1
a -> apple
b -> banana
key: a
key: b
0 103
1 111
```

This output corresponds to the results of the iterations demonstrated in the code examples above.

# Functions

Functions play a central role in Go programming. This tutorial provides an overview of defining and calling functions in Go, along with examples.

## Defining Functions

In Go, functions are defined using the `func` keyword. Here's an example of a function that takes two integers and returns their sum:

```go
func plus(a int, b int) int {
    return a + b
}
```

Go requires explicit returns; it won’t automatically return the value of the last expression.

When you have multiple consecutive parameters of the same type, you may omit the type name for the like-typed parameters up to the final parameter that declares the type. Here's an example:

```go
func plusPlus(a, b, c int) int {
    return a + b + c
}
```

## Calling Functions

Functions are called by using the function name followed by the arguments in parentheses. Here's how to call the functions defined above:

```go
res := plus(1, 2)
fmt.Println("1 + 2 =", res)

res = plusPlus(1, 2, 3)
fmt.Println("1 + 2 + 3 =", res)
```

The output of the above code will be:

```
1 + 2 = 3
1 + 2 + 3 = 6
```

## Multiple Return Values

One of the features of Go functions is the ability to return multiple values. This allows functions to return more than one result.

# Multiple Return Values

Go supports multiple return values, which is a feature frequently used in idiomatic Go programming. This tutorial demonstrates how to define functions with multiple return values and how to utilize them in Go.

## Defining Functions with Multiple Return Values

In Go, functions can return multiple values. The return types are specified within parentheses. Here's an example of a function `vals()` that returns two integers:

```go
func vals() (int, int) {
    return 3, 7
}
```

The `(int, int)` in the function signature indicates that the function returns two integers.

## Using Multiple Return Values

Multiple return values can be utilized by assigning them to variables during the function call. Here's how to use the two different return values from the `vals()` function:

```go
a, b := vals()
fmt.Println(a) // Output: 3
fmt.Println(b) // Output: 7
```

If you only need a subset of the returned values, you can use the blank identifier `_` to ignore the others:

```go
_, c := vals()
fmt.Println(c) // Output: 7
```

## Conclusion

Multiple return values are a powerful feature in Go, allowing functions to return more than one result. This feature is commonly used, especially in scenarios where functions need to return both a result and an error value.

For more details and advanced usage of multiple return values in Go, refer to the official Go documentation.
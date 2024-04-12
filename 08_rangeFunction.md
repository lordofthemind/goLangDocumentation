## Range

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
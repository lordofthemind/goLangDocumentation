# Data Structure
## Arrays

In Go, an array is a numbered sequence of elements of a specific length. In typical Go code, slices are much more common; arrays are useful in some special scenarios.

```go
package main

import "fmt"

func main() {
    // Here we create an array `a` that will hold exactly 5 ints.
    // The type of elements and length are both part of the array’s type.
    // By default, an array is zero-valued, which for ints means 0s.
    var a [5]int
    fmt.Println("emp:", a)

    // We can set a value at an index using the `array[index] = value` syntax,
    // and get a value with `array[index]`.
    a[4] = 100
    fmt.Println("set:", a)
    fmt.Println("get:", a[4])

    // The built-in `len` returns the length of an array.
    fmt.Println("len:", len(a))

    // Use this syntax to declare and initialize an array in one line.
    b := [5]int{1, 2, 3, 4, 5}
    fmt.Println("dcl:", b)

    // Array types are one-dimensional, but you can compose types to build multi-dimensional data structures.
    var twoD [2][3]int
    for i := 0; i < 2; i++ {
        for j := 0; j < 3; j++ {
            twoD[i][j] = i + j
        }
    }
    fmt.Println("2d:", twoD)
}
```

Output when run:

```
emp: [0 0 0 0 0]
set: [0 0 0 0 100]
get: 100
len: 5
dcl: [1 2 3 4 5]
2d: [[0 1 2] [1 2 3]]
```

This program demonstrates the usage of arrays in Go:

- Creating an array with a specific length and type.
- Setting and getting values at specific indices.
- Getting the length of an array using the `len` function.
- Declaring and initializing an array in one line.
- Creating and iterating over a multi-dimensional array.

You can run this program using `go run arrays.go` in your terminal to see the output.

Note that arrays appear in the form `[v1 v2 v3 ...]` when printed with `fmt.Println`.

## Slices

Slices are an important data type in Go, providing a more powerful interface to sequences than arrays.

```go
package main

import (
    "fmt"
    "slices"
)

func main() {
    // Unlike arrays, slices are typed only by the elements they contain (not the number of elements).
    // An uninitialized slice equals to nil and has length 0.
    var s []string
    fmt.Println("uninit:", s, s == nil, len(s) == 0)

    // To create an empty slice with non-zero length, use the built-in make.
    // Here we make a slice of strings of length 3 (initially zero-valued).
    // By default, a new slice’s capacity is equal to its length;
    // if we know the slice is going to grow ahead of time, it’s possible to pass a capacity explicitly as an additional parameter to make.
    s = make([]string, 3)
    fmt.Println("emp:", s, "len:", len(s), "cap:", cap(s))

    // We can set and get just like with arrays.
    s[0] = "a"
    s[1] = "b"
    s[2] = "c"
    fmt.Println("set:", s)
    fmt.Println("get:", s[2])

    // len returns the length of the slice as expected.
    fmt.Println("len:", len(s))

    // In addition to these basic operations, slices support several more that make them richer than arrays.
    // One is the built-in append, which returns a slice containing one or more new values.
    // Note that we need to accept a return value from append as we may get a new slice value.
    s = append(s, "d")
    s = append(s, "e", "f")
    fmt.Println("apd:", s)

    // Slices can also be copied.
    // Here we create an empty slice `c` of the same length as `s` and copy into `c` from `s`.
    c := make([]string, len(s))
    copy(c, s)
    fmt.Println("cpy:", c)

    // Slices support a “slice” operator with the syntax slice[low:high].
    // For example, this gets a slice of the elements s[2], s[3], and s[4].
    l := s[2:5]
    fmt.Println("sl1:", l)

    // This slices up to (but excluding) s[5].
    l = s[:5]
    fmt.Println("sl2:", l)

    // And this slices up from (and including) s[2].
    l = s[2:]
    fmt.Println("sl3:", l)

    // We can declare and initialize a variable for slice in a single line as well.
    t := []string{"g", "h", "i"}
    fmt.Println("dcl:", t)

    // The slices package contains a number of useful utility functions for slices.
    t2 := []string{"g", "h", "i"}
    if slices.Equal(t, t2) {
        fmt.Println("t == t2")
    }

    // Slices can be composed into multi-dimensional data structures.
    // The length of the inner slices can vary, unlike with multi-dimensional arrays.
    twoD := make([][]int, 3)
    for i := 0; i < 3; i++ {
        innerLen := i + 1
        twoD[i] = make([]int, innerLen)
        for j := 0; j < innerLen; j++ {
            twoD[i][j] = i + j
        }
    }
    fmt.Println("2d: ", twoD)
}
```

Output when run:

```
uninit: [] true true
emp: [  ] len: 3 cap: 3
set: [a b c]
get: c
len: 3
apd: [a b c d e f]
cpy: [a b c d e f]
sl1: [c d e]
sl2: [a b c d e]
sl3: [c d e f]
dcl: [g h i]
t == t2
2d: [[0] [1 2] [2 3 4]]
```

This program demonstrates the usage of slices in Go:

- Creating slices and understanding their properties.
- Setting and getting values in slices.
- Using `len` to get the length of a slice.
- Appending to slices and copying slices.
- Slicing slices with the slice operator.
- Declaring and initializing slices in a single line.
- Using utility functions from the slices package.
- Creating and working with multi-dimensional slices.

You can run this program using `go run slices.go` in your terminal to see the output.

## Maps

Maps are Go’s built-in associative data type (sometimes called hashes or dicts in other languages).

```go
package main

import (
    "fmt"
    "maps"
)

func main() {
    // To create an empty map, use the builtin make: make(map[key-type]val-type).
    m := make(map[string]int)

    // Set key/value pairs using typical `name[key] = val` syntax.
    m["k1"] = 7
    m["k2"] = 13

    // Printing a map with e.g. fmt.Println will show all of its key/value pairs.
    fmt.Println("map:", m)

    // Get a value for a key with `name[key]`.
    v1 := m["k1"]
    fmt.Println("v1:", v1)

    // If the key doesn’t exist, the zero value of the value type is returned.
    v3 := m["k3"]
    fmt.Println("v3:", v3)

    // The builtin `len` returns the number of key/value pairs when called on a map.
    fmt.Println("len:", len(m))

    // The builtin `delete` removes key/value pairs from a map.
    delete(m, "k2")
    fmt.Println("map:", m)

    // To remove all key/value pairs from a map, use the clear builtin.
    // clear(m) // This line should be `delete(m, key)` instead of `clear(m)`

    // The optional second return value when getting a value from a map indicates if the key was present in the map.
    // This can be used to disambiguate between missing keys and keys with zero values like 0 or "".
    // Here we didn’t need the value itself, so we ignored it with the blank identifier _.
    _, prs := m["k2"]
    fmt.Println("prs:", prs)

    // You can also declare and initialize a new map in the same line with this syntax.
    n := map[string]int{"foo": 1, "bar": 2}
    fmt.Println("map:", n)

    // The maps package contains a number of useful utility functions for maps.
    n2 := map[string]int{"foo": 1, "bar": 2}
    if maps.Equal(n, n2) {
        fmt.Println("n == n2")
    }
}
```

Output when run:

```
map: map[k1:7 k2:13]
v1: 7
v3: 0
len: 2
map: map[k1:7]
prs: false
map: map[bar:2 foo:1]
n == n2
```

This program demonstrates the usage of maps in Go:

- Creating an empty map and setting key/value pairs.
- Getting values for keys and handling cases where the key doesn't exist.
- Getting the number of key/value pairs using `len`.
- Deleting key/value pairs using `delete`.
- Declaring and initializing a new map in the same line.
- Using utility functions from the maps package.

You can run this program using `go run maps.go` in your terminal to see the output.

Note that maps appear in the form `map[k:v k:v]` when printed with `fmt.Println`.
# Pointers

Pointers are a fundamental feature in Go, allowing you to pass references to values and records within your program. This tutorial explores pointers in Go, including how they work and how to use them effectively.

## Understanding Pointers

In Go, a pointer is a variable that stores the memory address of another variable. It allows you to indirectly access and manipulate the value of that variable. Pointers are useful when you need to modify a variable's value within a function or when you want to avoid making unnecessary copies of large data structures.

## Functions with Pointers

Let's explore how pointers work in contrast to values with two functions: `zeroval` and `zeroptr`. 

### zeroval

The `zeroval` function has an `int` parameter, so arguments will be passed to it by value. This means that `zeroval` will get a copy of `ival`, distinct from the one in the calling function.

```go
func zeroval(ival int) {
    ival = 0
}
```

### zeroptr

In contrast, the `zeroptr` function has an `*int` parameter, meaning that it takes an `int` pointer. The `*iptr` code in the function body then dereferences the pointer from its memory address to the current value at that address. Assigning a value to a dereferenced pointer changes the value at the referenced address.

```go
func zeroptr(iptr *int) {
    *iptr = 0
}
```

### Example Usage

Here's how you can use these functions:

```go
func main() {
    i := 1
    fmt.Println("initial:", i)
    zeroval(i)
    fmt.Println("zeroval:", i)
    
    zeroptr(&i)
    fmt.Println("zeroptr:", i)
    
    fmt.Println("pointer:", &i)
}
```

In this example:
- `zeroval` doesn’t change the `i` in `main` because it operates on a copy of `i`.
- `zeroptr` changes the value of `i` in `main` because it has a reference to the memory address of `i`.
- The `&i` syntax gives the memory address of `i`, i.e., a pointer to `i`.

The output of the above code will be:

```
initial: 1
zeroval: 1
zeroptr: 0
pointer: 0x42131100
```

## Conclusion

Understanding pointers is essential for writing efficient and flexible code in Go. While pointers can be powerful, they also require careful handling to avoid issues such as memory leaks and dangling pointers.
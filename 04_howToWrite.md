# How to Write Go Code

## Introduction

This document demonstrates the development of a simple Go package inside a module and introduces the `go` tool, the standard way to fetch, build, and install Go modules, packages, and commands.

## Code Organization

Go programs are organized into packages, which are collections of source files in the same directory that are compiled together. Each repository contains one or more modules, with a module being a collection of related Go packages released together. 

## Your First Program

To compile and run a simple program, first choose a module path (e.g., `example/user/hello`) and create a `go.mod` file that declares it:

```bash
$ mkdir hello
$ cd hello
$ go mod init example/user/hello
```

Create a file named `hello.go` containing the following code:

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, world.")
}
```

Now you can build and install the program with the `go` tool:

```bash
$ go install example/user/hello
```

This command builds the `hello` command, producing an executable binary. It then installs that binary as `$HOME/go/bin/hello`.

## Importing Packages from Your Module

Let's create a package named `morestrings` and use it from the `hello` program.

Create a directory named `morestrings` and a file named `reverse.go` inside it:

```go
package morestrings

// ReverseRunes returns its argument string reversed rune-wise left to right.
func ReverseRunes(s string) string {
    r := []rune(s)
    for i, j := 0, len(r)-1; i < len(r)/2; i, j = i+1, j-1 {
        r[i], r[j] = r[j], r[i]
    }
    return string(r)
}
```

Modify the `hello.go` file to use the `morestrings` package:

```go
package main

import (
    "fmt"

    "example/user/hello/morestrings"
)

func main() {
    fmt.Println(morestrings.ReverseRunes("!oG ,olleH"))
}
```

Install the `hello` program:

```bash
$ go install example/user/hello
```

## Importing Packages from Remote Modules

You can import packages from remote modules using their import paths. For example, to use `github.com/google/go-cmp/cmp`, modify your program like so:

```go
package main

import (
    "fmt"

    "example/user/hello/morestrings"
    "github.com/google/go-cmp/cmp"
)

func main() {
    fmt.Println(morestrings.ReverseRunes("!oG ,olleH"))
    fmt.Println(cmp.Diff("Hello World", "Hello Go"))
}
```

Run `go mod tidy` to download the required modules and update `go.mod`:

```bash
$ go mod tidy
```

## Testing

Go has a lightweight test framework composed of the `go test` command and the `testing` package.

Write a test by creating a file with a name ending in `_test.go` and containing functions named `TestXXX`.

For example:

```go
package morestrings

import "testing"

func TestReverseRunes(t *testing.T) {
    cases := []struct {
        in, want string
    }{
        {"Hello, world", "dlrow ,olleH"},
        {"Hello, 世界", "界世 ,olleH"},
        {"", ""},
    }
    for _, c := range cases {
        got := ReverseRunes(c.in)
        if got != c.want {
            t.Errorf("ReverseRunes(%q) == %q, want %q", c.in, got, c.want)
        }
    }
}
```

Run the test with `go test`:

```bash
$ go test
```
# Tutorial: Create a Go Module

This tutorial introduces the fundamental features of the Go language by creating a module. A module in Go is a collection of related packages that provide a discrete and useful set of functions. In this tutorial, you'll create two modules: a library intended to be imported by other applications, and a caller application that will use the library.

## Prerequisites

- Some programming experience. Basic knowledge of functions, loops, and arrays is recommended.
- A text editor to edit your code. Any text editor will work fine, such as VSCode, GoLand, or Vim.
- A command terminal to execute Go commands. Go works well with any terminal on Linux, Mac, PowerShell, or cmd in Windows.

## Start a Module That Others Can Use

1. **Open a command prompt and navigate to your home directory:**

   ```bash
   # On Linux or Mac:
   cd

   # On Windows:
   cd %HOMEPATH%
   ```

2. **Create a directory named `greetings` for your Go module source code:**

   ```bash
   mkdir greetings
   cd greetings
   ```

3. **Start your module using the `go mod init` command:**

   ```bash
   go mod init example.com/greetings
   ```

   This command initializes a Go module with the specified module path (`example.com/greetings`) and creates a `go.mod` file to track your code's dependencies.

4. **Create a file named `greetings.go` and paste the following code into it:**

   ```go
   package greetings

   import "fmt"

   // Hello returns a greeting for the named person.
   func Hello(name string) string {
       message := fmt.Sprintf("Hi, %v. Welcome!", name)
       return message
   }
   ```

   This code defines a simple function named `Hello` that returns a personalized greeting message.

With these steps, you've created a Go module named `example.com/greetings` containing a single package with a `Hello` function. In the next steps of the tutorial, you'll learn how to call this function from another module.

For more tutorials and resources, see the [official Go documentation](https://golang.org/doc/).
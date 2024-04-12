# Writing Web Applications with Go

## Table of Contents
- [Introduction](#introduction)
- [Getting Started](#getting-started)
- [Data Structures](#data-structures)
- [Introducing the net/http package (an interlude)](#introducing-the-nethttp-package-an-interlude)
- [Using net/http to serve wiki pages](#using-nethttp-to-serve-wiki-pages)
- [Editing Pages](#editing-pages)
- [The html/template package](#the-htmltemplate-package)
- [Handling non-existent pages](#handling-non-existent-pages)
- [Saving Pages](#saving-pages)
- [Error handling](#error-handling)
- [Template caching](#template-caching)
- [Validation](#validation)
- [Introducing Function Literals and Closures](#introducing-function-literals-and-closures)
- [Try it out!](#try-it-out)

## Introduction
This tutorial covers creating web applications in Go, focusing on:
- Creating data structures with load and save methods
- Using the `net/http` package to build web applications
- Utilizing the `html/template` package to process HTML templates
- Validating user input with regular expressions
- Using closures and function literals

Assumed knowledge:
- Programming experience
- Understanding of basic web technologies (HTTP, HTML)
- Some UNIX/DOS command-line knowledge

## Getting Started
After installing Go, follow these steps to create a new directory for the tutorial and set up the initial Go file:

```bash
$ mkdir gowiki
$ cd gowiki
$ touch wiki.go
```

Open `wiki.go` in your favorite editor and add the following code to start with:

```go
package main

import (
    "fmt"
    "os"
)
```

In this code snippet, we import the `fmt` and `os` packages from the Go standard library. We'll add more packages to this import declaration as we implement additional functionality.

## Data Structures
We'll start by defining the data structures. A wiki consists of interconnected pages, each with a title and body. Let's define a `Page` struct for this purpose:

```go
type Page struct {
    Title string
    Body  []byte
}
```

The `Page` struct represents a wiki page with a `Title` and `Body` fields. We use a `[]byte` type for `Body` because it's the type expected by the I/O libraries we'll use.

We also need methods to save and load pages from files. Let's define a `save` method for the `Page` struct:

```go
func (p *Page) save() error {
    filename := p.Title + ".txt"
    return os.WriteFile(filename, p.Body, 0600)
}
```

This method saves the page's body to a text file with the title as the filename. It returns an error to handle any issues that may occur during file writing.

Next, let's define a `loadPage` function to load pages from files:

```go
func loadPage(title string) (*Page, error) {
    filename := title + ".txt"
    body, err := os.ReadFile(filename)
    if err != nil {
        return nil, err
    }
    return &Page{Title: title, Body: body}, nil
}
```

This function reads the contents of the file into memory and returns a pointer to a `Page` struct. If the file doesn't exist or there's an error reading it, it returns an error.

Now, let's write a simple `main` function to test our code:

```go
func main() {
    p1 := &Page{Title: "TestPage", Body: []byte("This is a sample Page.")}
    p1.save()
    p2, _ := loadPage("TestPage")
    fmt.Println(string(p2.Body))
}
```

This `main` function creates a new page, saves it to a file, loads it back, and prints its body to the console.

Compile and run the program:

```bash
$ go build wiki.go
$ ./wiki
```

You should see the body of the test page printed to the console.

This concludes the initial setup and data structure definition. In the next sections, we'll explore serving wiki pages using the `net/http` package and implementing editing functionalities.
```

Let me know if you'd like to continue with the next sections or if there's anything specific you'd like to focus on!
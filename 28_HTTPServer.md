# Creating an HTTP Server in Go

In this tutorial, we'll cover how to create a basic HTTP server in Go, handle incoming requests, and serve static files.

## Creating a Basic HTTP Server

Let's start by creating a simple HTTP server that listens on port 8080 and responds with a "Hello, World!" message to every incoming request.

```go
package main

import (
    "fmt"
    "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello, World!")
}

func main() {
    http.HandleFunc("/", handler)
    fmt.Println("Server started on port 8080")
    http.ListenAndServe(":8080", nil)
}
```

### Explanation

- We define a handler function that takes an `http.ResponseWriter` and an `http.Request`.
- Inside the handler function, we use `fmt.Fprintf` to write "Hello, World!" to the response writer.
- In the `main` function, we register the handler function with the root path ("/") using `http.HandleFunc`.
- Finally, we start the HTTP server on port 8080 using `http.ListenAndServe`.

## Handling Requests

Let's enhance our HTTP server to handle different paths and methods by adding more handler functions.

```go
package main

import (
    "fmt"
    "net/http"
)

func homeHandler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Welcome to the Home Page!")
}

func aboutHandler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "About Us")
}

func contactHandler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Contact Us")
}

func main() {
    http.HandleFunc("/", homeHandler)
    http.HandleFunc("/about", aboutHandler)
    http.HandleFunc("/contact", contactHandler)

    fmt.Println("Server started on port 8080")
    http.ListenAndServe(":8080", nil)
}
```

### Explanation

- We define three new handler functions: `homeHandler`, `aboutHandler`, and `contactHandler`.
- Each handler function responds with a different message depending on the requested path.
- We register these handler functions with their respective paths ("/", "/about", "/contact") using `http.HandleFunc`.

## Serving Static Files

To serve static files such as HTML, CSS, or JavaScript files, we can use the `http.FileServer` handler.

```go
package main

import (
    "fmt"
    "net/http"
)

func main() {
    http.Handle("/", http.FileServer(http.Dir("./static")))
    
    fmt.Println("Server started on port 8080")
    http.ListenAndServe(":8080", nil)
}
```

### Explanation

- We use `http.FileServer` to create a handler that serves files from the specified directory (`./static` in this case).
- The `http.Handle` function registers the file server handler with the root path ("/").

## Conclusion

In this tutorial, we learned how to create a basic HTTP server in Go, handle incoming requests, and serve static files. With this knowledge, you can start building more complex web applications in Go.
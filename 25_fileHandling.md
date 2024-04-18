# File Handling in Go

File handling is a common task in programming, and Go provides robust functionalities to work with files. In this tutorial, we'll cover how to read from and write to files, handle errors, and manipulate file metadata.

## Reading from Files

### Reading Entire File

To read the entire contents of a file into memory, you can use the `ioutil.ReadFile` function.

```go
package main

import (
    "fmt"
    "io/ioutil"
)

func main() {
    data, err := ioutil.ReadFile("example.txt")
    if err != nil {
        fmt.Println("Error reading file:", err)
        return
    }
    fmt.Println("File content:")
    fmt.Println(string(data))
}
```

### Output

Assuming `example.txt` contains the text "Hello, world!":

```
File content:
Hello, world!
```

### Reading File Line by Line

If you need to process a file line by line, you can use a `Scanner` from the `bufio` package.

```go
package main

import (
    "bufio"
    "fmt"
    "os"
)

func main() {
    file, err := os.Open("example.txt")
    if err != nil {
        fmt.Println("Error opening file:", err)
        return
    }
    defer file.Close()

    scanner := bufio.NewScanner(file)
    for scanner.Scan() {
        fmt.Println(scanner.Text())
    }
    if err := scanner.Err(); err != nil {
        fmt.Println("Error reading file:", err)
    }
}
```

## Writing to Files

To write data to a file, you can use the `os.WriteFile` function.

```go
package main

import (
    "fmt"
    "os"
)

func main() {
    data := []byte("This is a test.")
    err := os.WriteFile("output.txt", data, 0644)
    if err != nil {
        fmt.Println("Error writing to file:", err)
        return
    }
    fmt.Println("Data written to file successfully.")
}
```

### Output

After running the above code, a file named `output.txt` will be created with the content "This is a test."

## File Metadata

Go provides functions to retrieve metadata information about files, such as size, permissions, and modification time.

```go
package main

import (
    "fmt"
    "os"
)

func main() {
    file, err := os.Stat("example.txt")
    if err != nil {
        fmt.Println("Error getting file info:", err)
        return
    }

    fmt.Println("File name:", file.Name())
    fmt.Println("File size:", file.Size(), "bytes")
    fmt.Println("Permissions:", file.Mode())
    fmt.Println("Last modified:", file.ModTime())
}
```

### Output

Assuming `example.txt` exists:

```
File name: example.txt
File size: 13 bytes
Permissions: -rw-r--r--
Last modified: 2022-04-06 14:30:00 +0000 UTC
```

## Conclusion

In this tutorial, we covered how to read from and write to files, handle errors, and manipulate file metadata in Go. Understanding file handling in Go is essential for many real-world applications.
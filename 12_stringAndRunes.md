# Strings and Runes

In Go, strings are treated specially as containers of text encoded in UTF-8. Unlike in some other languages where strings are composed of "characters", in Go, the equivalent concept is called a "rune", which is an integer representing a Unicode code point.

## Strings in Go

A Go string is essentially a read-only slice of bytes. Let's explore some basic operations with strings and runes.

```go
package main

import (
    "fmt"
    "unicode/utf8"
)

func main() {
    // Define a string containing the word "hello" in Thai
    const s = "สวัสดี"

    // Print the length of the string
    fmt.Println("Length of string:", len(s))

    // Print the raw byte values of each character in the string
    fmt.Print("Raw byte values:")
    for i := 0; i < len(s); i++ {
        fmt.Printf("%x ", s[i])
    }
    fmt.Println()

    // Count the number of runes in the string
    fmt.Println("Rune count:", utf8.RuneCountInString(s))

    // Iterate over each rune in the string along with its index
    for idx, runeValue := range s {
        fmt.Printf("%#U starts at index %d\n", runeValue, idx)
    }

    // Iterate over each rune using utf8.DecodeRuneInString
    fmt.Println("\nUsing DecodeRuneInString")
    for i, w := 0, 0; i < len(s); i += w {
        runeValue, width := utf8.DecodeRuneInString(s[i:])
        fmt.Printf("%#U starts at index %d\n", runeValue, i)
        w = width

        // Example function call using the rune value
        examineRune(runeValue)
    }
}

// Function to examine a rune
func examineRune(r rune) {
    // Compare rune values with rune literals
    if r == 't' {
        fmt.Println("Found 't'")
    } else if r == 'ส' {
        fmt.Println("Found 'ส'")
    }
}
```

This Go code snippet demonstrates various operations with strings and runes. Let's break it down:

1. **String Initialization**: We define a string `s` containing the Thai word for "hello".
2. **Length of String**: We print the length of the string, which counts the number of bytes.
3. **Raw Byte Values**: We print the raw byte values of each character in the string.
4. **Rune Count**: We count the number of runes in the string, which may differ from the byte count.
5. **Iterating Over Runes**: We use a range loop to iterate over each rune in the string, printing the rune along with its index.
6. **Using DecodeRuneInString**: We iterate over each rune using `utf8.DecodeRuneInString`, which handles multi-byte characters correctly.

That's a basic overview of strings and runes in Go! Feel free to explore further.
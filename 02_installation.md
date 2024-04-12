## Installation (Linux)

1. Open a terminal.
2. Update your package manager:
   ```bash
   sudo apt update
   ```
3. Download the Go tar file:
   ```bash
   wget https://go.dev/dl/go1.22.2.linux-amd64.tar.gz
   ```
4. Remove any existing Go installation:
   ```bash
   sudo rm -rf /usr/local/go
   ```
5. Extract the binary files to `/usr/local/go`:
   ```bash
   sudo tar -C /usr/local -xzf go1.22.2.linux-amd64.tar.gz
   ```
6. Add the Go binary directory to your PATH by adding the following line to your shell configuration file (e.g., ~/.bashrc, ~/.zshrc, or ~/.profile):
   ```bash
   export PATH=$PATH:/usr/local/go/bin
   ```
7. Restart your shell to apply the changes, then verify the installation by running:
   ```bash
   which go
   ```

## Writing and Running Your First Program

Now that you have Go installed, let's write a simple "Hello, World!" program.

1. Open a text editor or IDE.
2. Create a new file named `hello.go`.
3. Copy and paste the following code into `hello.go`:
   ```go
   package main

   import "fmt"

   func main() {
       fmt.Println("Hello, World!")
   }
   ```
4. Save the file.

To compile and run your `hello.go` program, follow these steps:

1. Open a terminal.
2. Navigate to the directory containing `hello.go`:
   ```bash
   cd /path/to/directory
   ```
3. Compile your program by typing:
   ```bash
   go build hello.go
   ```
   This will create an executable file named `hello`.
4. Run your program:
   ```bash
   ./hello
   ```
5. You should see the output `Hello, World!` printed to the terminal.

Congratulations! You've successfully written and run your first Go program on Linux.
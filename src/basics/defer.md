# Defer in Go

`Defer` is a unique and powerful feature in Go that allows you to postpone the execution of a function until the surrounding function completes. It's often used for cleanup tasks, ensuring resources are released appropriately.

## Basic Defer Usage

```go
package main

import "fmt"

func main() {
    defer fmt.Println("This will be deferred until the end of the function.")
    
    fmt.Println("Executing the main part of the function.")
}
```

In this example, the deferred statement will be executed after the main part of the function completes.

## Deferred Functions with Arguments

```go
package main

import "fmt"

func main() {
    name := "Armand"

    defer fmt.Printf("Deferred: Goodbye, %s!\n", name)
    
    fmt.Printf("Hello, %s!\n", name)
}
```

Even if a function has arguments, the values are evaluated immediately, but the execution is deferred.

## Defer in a Loop

```go
package main

import "fmt"

func main() {
    for i := 0; i < 5; i++ {
        defer fmt.Println("Deferred in loop:", i)
    }

    fmt.Println("Main part of the function.")
}
```

In a loop, the deferred statements are executed in a Last In, First Out (LIFO) order after the loop completes.

## Common Use: Resource Cleanup

```go
package main

import "fmt"

func main() {
    file := openFile("example.txt")
    defer closeFile(file)

    // File operations go here
}

func openFile(filename string) *File {
    fmt.Println("Opening file:", filename)
    // Implement file opening logic
    return &File{}
}

func closeFile(file *File) {
    fmt.Println("Closing file.")
    // Implement file closing logic
}
```

`Defer` is frequently used for resource management, ensuring that cleanup tasks, like closing files or releasing other resources, are performed, like *database connections*.

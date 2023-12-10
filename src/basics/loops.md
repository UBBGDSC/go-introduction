# Loops in Go

Loops in Go provide a way to repeatedly execute a block of code based on a specified condition. Go offers a simple and powerful set of loop constructs to handle various scenarios efficiently.

## For Loop

The `for` loop is the only loop statement in Go, but it can be used in multiple ways:

### Basic For Loop

```go
package main

import "fmt"

func main() {
    for i := 0; i < 5; i++ {
        fmt.Println(i)
    }
}
```

## For as While Loop

```go
package main

import "fmt"

func main() {
    counter := 0
    for counter < 5 {
        fmt.Println(counter)
        counter++
    }
}
```

## Infinite Loop

```go
package main

import "fmt"

func main() {
    for {
        fmt.Println("This is an infinite loop.")
        // Add a break condition to avoid infinite execution
        break
    }
}
```

## Range Loop

The `range` keyword is used to iterate over elements in various data structures, such as arrays, slices, maps, or strings:

```go
package main

import "fmt"

func main() {
    numbers := []int{1, 2, 3, 4, 5}
    for index, value := range numbers {
        fmt.Printf("Index: %d, Value: %d\n", index, value)
    }
}
```

## Defer Loop Execution

Defer can be used in a loop to postpone the execution of a function until the surrounding function completes:

```go
package main

import "fmt"

func main() {
    for i := 0; i < 3; i++ {
        defer fmt.Println(i)
    }
}
```

Defer will be covered in more detail in the [Defer](./defer.md) section.
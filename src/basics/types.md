# Types

In Go, types define the nature of variables, enabling the compiler to understand how to handle data. Understanding types is fundamental to writing robust and efficient Go code.

## Basic Data Types

Go has several basic data types, including:

- **Numeric Types:** `int`, `float64`, `uint`, etc.
- **String Type:** `string`
- **Boolean Type:** `bool`

For example:

```go
package main

import "fmt"

func main() {
    var age int = 25
    var name string = "Armand"
    var isStudent bool = true

    fmt.Printf("%s is %d years old. Student: %t\n", name, age, isStudent)
}
```

## Composite Data Types

Go supports composite data types that allow you to create structures and collections:

- **Arrays:** Fixed-size sequences of elements.
- **Slices:** Dynamic and flexible views into arrays.
- **Maps:** Key-value pairs for efficient lookups.

Example using slices:

```go
package main

import "fmt"

func main() {
    // Creating a slice
    fruits := []string{"apple", "banana", "orange"}

    // Adding a new element
    fruits = append(fruits, "grape")

    fmt.Println("Fruits:", fruits)
}
```

## User Defined Types

You can create your own types using the `type`` keyword. This enhances code readability and reusability. For instance:

```go
package main

import "fmt"

// Define a new type
type Celsius float64

func main() {
    temperature := Celsius(25.5)
    fmt.Printf("Current temperature: %.2f°C\n", temperature)
}
```

# Variables

Variables in Go are used to store and manage data. They are essential for any programming language, and Go provides a simple yet powerful way to declare and use variables.

## Variable Declaration

You can declare a variable in Go using the `var` keyword. For example:

```go
package main

import "fmt"

func main() {
    var age int
    age = 25

    var name string = "Armand"

    fmt.Printf("%s is %d years old.\n", name, age)
}
```

## Short Declaration

Go also allows short variable declarations, which infer the type:

```go
package main

import "fmt"

func main() {
    age := 25
    name := "Armand"

    fmt.Printf("%s is %d years old.\n", name, age)
}
```

## Variable Types

Variables can have various types, including:

- **Numeric Types:** `int`, `float64`, `uint`, etc.
- **String:** `string`
- **Boolean** `bool`

See [Types](./types.md) for more information.

## Constants

In addition to variables, Go supports constants—values that cannot be changed after declaration:

```go
package main

import "fmt"

const pi = 3.14

func main() {
    fmt.Printf("The value of pi is %.2f\n", pi)
}
```

## Global Variables

In Go, global variables are declared outside of any function and are accessible throughout the entire package. They have package-level scope and can be used by any function within the same package.

Example:

```go
package main

import "fmt"

// Global variable accessible throughout the package
var globalCount int = 0

func main() {
    // Accessing and modifying the global variable
    globalCount++
    fmt.Println("Global Count:", globalCount)

    // Calling a function that uses the global variable
    displayGlobalCount()
}

// Function that uses the global variable
func displayGlobalCount() {
    fmt.Println("Displaying Global Count:", globalCount)
}
```

<details>
<summary>Warning note: Global Variables in Go</summary>
It's important to note that while global variables can be convenient, they should be used judiciously to avoid unnecessary dependencies and potential issues related to state changes. In Go, emphasis is often placed on encapsulation and passing data explicitly between functions rather than relying heavily on global state.
</details>
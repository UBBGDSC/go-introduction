# If/Else Statements in Go

In Go, the `if` and `else` statements are fundamental constructs for making decisions in your code. While the syntax may appear familiar, Go introduces some unique features.

## Basic If Statement

The basic `if` statement in Go follows a straightforward syntax:

```go
package main

import "fmt"

func main() {
    age := 25

    if age >= 18 {
        fmt.Println("You are an adult.")
    }
}
```

## If/Else Statement

The `if` statement can be combined with an `else` statement for alternative execution paths:

```go
package main

import "fmt"

func main() {
    age := 15

    if age >= 18 {
        fmt.Println("You are an adult.")
    } else {
        fmt.Println("You are a minor.")
    }
}
```

## If with Initialization

Go allows you to initialize a variable as part of the `if` statement:

```go
package main

import "fmt"

func main() {
    if num := 10; num%2 == 0 {
        fmt.Println("The number is even.")
    } else {
        fmt.Println("The number is odd.")
    }
}
```

Note that the `num` variable is only scoped to the `if` and `else` blocks.

## Logical Operators

Go supports logical operators (`&&`, `||`, `!`) for combining conditions:

```go
package main

import "fmt"

func main() {
    temperature := 25

    if temperature > 30 || temperature < 0 {
        fmt.Println("Extreme temperature detected.")
    } else if temperature >= 20 && temperature <= 30 {
        fmt.Println("Optimal temperature.")
    } else {
        fmt.Println("Normal temperature range.")
    }
}
```
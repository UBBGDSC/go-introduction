# Functions

Functions in Go are blocks of code that perform a specific task. They play a crucial role in structuring and organizing your code. Let's explore the key concepts of functions in Go.

## Function Declaration

You can declare a function using the `func` keyword. Here's a simple example:

```go
package main

import "fmt"

// Function that prints a greeting
func greet() {
    fmt.Println("Hello, Go Functions!")
}

func main() {
    // Call the greet function
    greet()
}
```

## Function Parameters

Functions can take parameters, allowing them to receive input data. For example:

```go
package main

import "fmt"

// Function that takes parameters
func addNumbers(a, b int) {
    sum := a + b
    fmt.Printf("Sum of %d and %d is: %d\n", a, b, sum)
}

func main() {
    // Call the addNumbers function with arguments
    addNumbers(5, 7)
}
```

## Return Values

Functions can also return values. Here's an example:

```go
package main

import "fmt"

// Function that returns a value
func multiply(a, b int) int {
    return a * b
}

func main() {
    // Call the multiply function and print the result
    result := multiply(3, 4)
    fmt.Printf("Multiplication Result: %d\n", result)
}
```

## Multiple Return Values

Go allows functions to return multiple values:

```go
package main

import "fmt"

// Function with multiple return values
func divideAndRemainder(dividend, divisor int) (int, int) {
    quotient := dividend / divisor
    remainder := dividend % divisor
    return quotient, remainder
}

func main() {
    // Call the function and capture both return values
    q, r := divideAndRemainder(10, 3)
    fmt.Printf("Quotient: %d, Remainder: %d\n", q, r)
}
```

### Error Handling using Multiple Return Values

Multiple return values are often used to handle errors. For example:

```go
package main

import (
    "fmt"
    "errors"
)

// Function with multiple return values for error handling
func divideAndRemainder(dividend, divisor int) (int, int, error) {
    if divisor == 0 {
        // Return an error if divisor is zero
        return 0, 0, errors.New("cannot divide by zero")
    }

    quotient := dividend / divisor
    remainder := dividend % divisor
    return quotient, remainder, nil
}

func main() {
    // Call the function and handle the error
    if q, r, err := divideAndRemainder(10, 3); err == nil {
        fmt.Printf("Quotient: %d, Remainder: %d\n", q, r)
    } else {
        fmt.Println("Error:", err)
    }

    // Handling a divide by zero scenario
    if q, r, err := divideAndRemainder(10, 0); err == nil {
        fmt.Printf("Quotient: %d, Remainder: %d\n", q, r)
    } else {
        fmt.Println("Error:", err)
    }
}
```

In this example, the divideAndRemainder function returns an additional error value, allowing you to check for errors in the calling code. This is a common pattern in Go for effective error handling.

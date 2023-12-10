# Methods and Interfaces in Go
Go's approach to methods and interfaces is distinctive, providing a different approach to object-oriented programming than languages like Java or C++.

## Methods

In Go, methods are functions associated with a particular type. They enable you to attach behavior to values of a specific type.

```go
package main

import "fmt"

type Rectangle struct {
	Width  float64
	Height float64
}

// Method for calculating the area of a rectangle
func (r Rectangle) Area() float64 {
	return r.Width * r.Height
}

func main() {
	rect := Rectangle{Width: 5, Height: 10}
	fmt.Printf("Area of the rectangle: %f\n", rect.Area())
}
```

In this example, `Area` is a method associated with the `Rectangle` type, allowing you to calculate the area directly from a `Rectangle` instance.

## Interfaces

Interfaces in Go provide a way to define a set of methods that a type must implement. This promotes loose coupling and polymorphism in your code.

```go
package main

import "fmt"

// Shape interface with an Area method
type Shape interface {
	Area() float64
}

// Rectangle type implementing the Shape interface
type Rectangle struct {
	Width  float64
	Height float64
}

// Circle type implementing the Shape interface
type Circle struct {
	Radius float64
}

// Area method for Rectangle to satisfy the Shape interface
func (r Rectangle) Area() float64 {
	return r.Width * r.Height
}

// Area method for Circle to satisfy the Shape interface
func (c Circle) Area() float64 {
	return 3.14 * c.Radius * c.Radius
}

func printArea(s Shape) {
	fmt.Printf("Area: %f\n", s.Area())
}

func main() {
	rect := Rectangle{Width: 5, Height: 10}
	circle := Circle{Radius: 3}

	printArea(rect)   // Output: Area: 50.000000
	printArea(circle) // Output: Area: 28.260000
}
```

Here, both `Rectangle` and `Circle` types implement the `Shape` interface by providing their respective `Area` methods. The `printArea` function can then accept any type that satisfies the `Shape` interface.

## Summary

Think of structs as the classes of Go, where the methods are defined on the struct itself. Public methods/fields are those that start with a capital letter, and private methods/fields are those that start with a lowercase letter. Fields are accessed using the dot notation, similar to other languages.
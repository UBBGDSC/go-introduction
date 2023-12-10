# Concurrency in Go

Go is renowned for its built-in support for concurrency, providing goroutines and channels as first-class citizens to simplify concurrent programming.

## Goroutines

Goroutines are lightweight threads of execution that enable concurrent programming in Go. They are similar to threads in other languages, but they are much cheaper to create and manage.

```go
package main

import (
	"fmt"
	"time"
)

func printNumbers() {
	for i := 1; i <= 5; i++ {
		time.Sleep(500 * time.Millisecond)
		fmt.Println(i)
	}
}

func printLetters() {
	for char := 'a'; char <= 'e'; char++ {
		time.Sleep(300 * time.Millisecond)
		fmt.Printf("%c\n", char)
	}
}

func main() {
	// Start two goroutines concurrently
	go printNumbers()
	go printLetters()

	// Wait for a while to allow goroutines to execute
	time.Sleep(2 * time.Second)
}
```

In this example, `printNumbers` and `printLetters` are executed concurrently as goroutines. The `go` keyword initiates the concurrent execution.

## Channels

Channels are a powerful concurrency primitive in Go, facilitating communication between goroutines. They are used to send and receive values between goroutines.

```go
package main

import (
	"fmt"
	"time"
)

func sendMessage(msg string, c chan string) {
	time.Sleep(1 * time.Second)
	c <- msg // Send the message to the channel
}

func main() {
	messageChannel := make(chan string) // Create a channel

	go sendMessage("Hello", messageChannel)
	go sendMessage("World", messageChannel)

	// Receive messages from the channel
	msg1 := <-messageChannel
	msg2 := <-messageChannel

	fmt.Println(msg1, msg2)
}
```

In this example, two goroutines (`sendMessage`) send messages to the same channel (`messageChannel`). The main goroutine then receives and prints the messages.


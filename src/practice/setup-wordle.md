# Setup Wordle

In this practice session, you will set up a Wordle application with HTTP server endpoints for retrieving Wordle preferences and making guesses. 

We will be using a library called `gowordleapi` that provides a Wordle package with the necessary functionality. We created this library to help you focus on the core concepts of Go without getting bogged down in the details of the Wordle implementation.

Follow the step-by-step instructions below:

## Step 1: Import Necessary Packages

Open the previous ping-pong project and add the following imports:

```go
package main

import (
	"net/http"
	"github.com/UBBGDSC/gowordleapi/wordle"
)
```

To install the Wordle package, use the following command in your terminal:

```bash
go get github.com/UBBGDSC/gowordleapi/wordle
```

## Step 2: Create a Wordle Instance

Create a new Wordle instance in the main function:

```go
// Create a Wordle instance
wordleInstance := wordle.NewWordle()
```

## Step 3: Set Up Wordle Server Endpoints

```go
// Set up Wordle server endpoints
wordle.SetupServer(server, wordleInstance)
```

## Step 4: Make a GET request to the `/wordle/guess` Endpoint

```go
// Example GET request
res, err := http.Get("http://localhost:8080/wordle/guess")
if err != nil {
	// Handle error
}

var wordlePreferences wordle.WordlePreferences
err = json.NewDecoder(res.Body).Decode(&wordlePreferences)
if err != nil {
	// Handle decoding error
}

fmt.Printf("Wordle Preferences: %+v\n", wordlePreferences)
```

**Note:** This code will need to be placed in a `goroutine` or a separate Go project to run concurrently with the server. Because the server is blocking the main thread, the GET request will not be able to complete. See end of practice session for final code.

_Optional step_: In the browser, navigate to http://localhost:8080/wordle/guess to see the Wordle preferences. The browser makes a GET request by default.

You should see a response similar to the following:

```json
{
    "Length": 10,
    "ContainsCapitalLetters": false,
    "ContainsSpecialChars": false,
    "ContainsNumbers": false
}
```

## Step 5: Make a Guess with POST Request

```go
// Example POST request
guessRequestBody := wordle.GuessRequest{
	Guess: "yourguess",
}

jsonData, err := json.Marshal(guessRequestBody)
if err != nil {
	// Handle marshalling error
}

res, err := http.Post("http://localhost:8080/wordle/guess", "application/json", strings.NewReader(string(jsonData)))
if err != nil {
	// Handle POST request error
}

if res.StatusCode != http.StatusOK {
    // this means that the guess was not built correctly
    // (length, capital letters, special characters, numbers)
}

var guessResponse wordle.GuessResponse
err = json.NewDecoder(res.Body).Decode(&guessResponse)
if err != nil {
	// Handle decoding error
}

fmt.Printf("Guess Response: %+v\n", guessResponse)
```

**Note:** This code will need to be placed in a goroutine or a separate Go project to run concurrently with the server. Because the server is blocking the main thread, the POST request will not be able to complete. See end of practice session for final code.

If the guess length is not equal to the word length, you will get a Bad Request error.

Otherwise, you should see a response similar to the following (depending on your guess):

```json
{
    "correctPositionCount": 0,
    "partialMatchCount": 6,
    "feedback": "1011001011"
}
```

The feedback string contains a `1` for letters that exist in the word, but are not in the correct position, and a `0` for letters that do not exist in the word. `2` means the letter is in the correct position. Unfortunately in this example, the feedback string is saying we have 6 letters that exist in the word, but are not in the correct position. We will need to make more guesses to figure out the correct word.

Congratulations! You've successfully set up a Wordle application with HTTP server endpoints for retrieving Wordle preferences and making guesses.

### Final Code

```go
package main

import (
	"encoding/json"
	"fmt"
	"io"
	"net/http"
	"strings"

	"github.com/UBBGDSC/gowordleapi/wordle"
)

func main() {
	wordleInstance := wordle.NewWordle()

	server := &http.Server{
		Addr:    "127.0.0.1:8080", // Change the port as needed
		Handler: http.DefaultServeMux,
	}

	wordle.SetupServer(server, wordleInstance)

	go func() {
		// Example GET request
		res, err := http.Get("http://localhost:8080/wordle/guess")
		if err != nil {
			panic(err)
		}

		var wordlePreferences wordle.WordlePreferences
		err = json.NewDecoder(res.Body).Decode(&wordlePreferences)
		if err != nil {
			panic(err)
		}

		fmt.Printf("Wordle Preferences: %+v\n", wordlePreferences)
	}()

	go func() {
		// Example POST request
		guessRequestBody := wordle.GuessRequest{
			Guess: "yourguesss",
		}

		jsonData, err := json.Marshal(guessRequestBody)
		if err != nil {
			panic(err)
		}

		res, err := http.Post("http://localhost:8080/wordle/guess", "application/json", strings.NewReader(string(jsonData)))
		if err != nil {
			panic(err)
		}

		if res.StatusCode != http.StatusOK {
			// this means that the guess was not built correctly
			// (length, capital letters, special characters, numbers)
			body, err := io.ReadAll(res.Body)
			if err != nil {
				panic(err)
			}
			fmt.Printf("Error Message: %s\n", string(body))
			return
		}

		var guessResponse wordle.GuessResponse
		err = json.NewDecoder(res.Body).Decode(&guessResponse)
		if err != nil {
			panic(err)
		}

		fmt.Printf("Guess Response: %+v\n", guessResponse)
	}()

	// Start the server
	err := server.ListenAndServe()
	if err != nil {
		panic(err)
	}
}
```

Notice the use of `go` to run the GET and POST requests concurrently with the server. This is necessary because the server is blocking the main thread.

Also, the error handling are just `panic` statements. This is not recommended for production code, but is fine for practice sessions.

## What we learned so far

- How to setup an HTTP server in Go
- How to make GET and POST requests in Go
- How to install and use a Go library
- How to use goroutines to run code concurrently
# Ping Pong Practice

In this practice session, you will create a simple HTTP server with a /ping endpoint that responds with "pong." Follow the step-by-step instructions below:

## Step 1: Create a New Project

Create a new project called `ping-pong`:

```bash
go mod init ping-pong
```

## Step 2: Create a Simple HTTP Server

Create a new file called `main.go` and add the following code:

```go
package main

import (
	"net/http"
)

func main() {
	server := &http.Server{
		Addr:    "127.0.0.1:8080", // Change the port as needed
		Handler: http.DefaultServeMux,
	}

	// Start the server
	err := server.ListenAndServe()
	if err != nil {
		panic(err)
	}
}
```

The code above creates a simple HTTP server that listens on port 8080. Run the server and verify that it works:

```bash
go run .
```

Now open a browser and navigate to http://localhost:8080. You should see a "_404 page not found_" error.

## Step 2: Implement the /ping Endpoint

Extend your code to include a handler for the `/ping` endpoint.

```go
// ping handler
http.HandleFunc("/ping", func(w http.ResponseWriter, r *http.Request) {
    w.Write([]byte("pong"))
})
```

In this step, we introduce the `http.HandleFunc` function to associate the` /ping` URL path with a handler function. The handler function, in this case, is a simple anonymous function that writes the string "_pong_" to the response.

### Final Code

```go
package main

import (
	"net/http"
)

func main() {
	server := &http.Server{
		Addr:    "127.0.0.1:8080", // Change the port as needed
		Handler: http.DefaultServeMux,
	}

	// ping handler
	http.HandleFunc("/ping", func(w http.ResponseWriter, r *http.Request) {
		w.Write([]byte("pong"))
	})

	// Start the server
	err := server.ListenAndServe()
	if err != nil {
		panic(err)
	}
}
```

## Step 3: Build and Run the Server

Run the server again:

```bash
go run .
```

Now open a browser and navigate to http://localhost:8080/ping. You should see the string "_pong_" in the browser.

*Optional: to build the server binary, run:*

```bash
go build .
```

Now you should have an executable in the directory. You can double click on it to run the server.
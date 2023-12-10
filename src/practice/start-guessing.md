# Exercise: Start Guessing

In this exercise, you will modify the final code from the previous step to enable your Wordle application to start guessing words automatically. The Wordle library provides an `EasyWordChannel` that contains URLs to words that can be guessed. Your task is to implement a goroutine that continuously reads from this channel, retrieves Wordle preferences using a `GET` request, and makes guesses with a `POST` request, similar to the previous step.

Here's the code snippet to add to your existing program:

```go
go func() {
    for easyWordUrl := range wordleInstance.EasyWordChannel {
        go revealEasyWord(easyWordUrl)
    }
}()
```

This code snippet creates a goroutine that continuously reads from the `EasyWordChannel` and calls the `revealEasyWord` function for each URL. The `revealEasyWord` function should
make a `GET` request to the URL, retrieve the Wordle preferences, and make guesses until the word is revealed, similar to the previous step.

You will implement your own `revealEasyWord` function. Here's the function signature:

```go
func revealEasyWord(easyWordUrl string) {
    // TODO: Implement this function
}
```

### Explanation
The `EasyWordChannel` is a channel provided by the Wordle library that receives URLs to words that can be guessed.

The for `easyWordUrl := range wordleInstance.EasyWordChannel` loop continuously reads from the `EasyWordChannel`. When a new URL is received, it triggers the `revealEasyWord(easyWordUrl)` function.

The `easyWordRoutine` function is responsible for making `GET` requests to the provided URL to retrieve Wordle preferences and making `POST` requests to guess the word.

The entire goroutine is started with `go func() {...}()` to run concurrently with the rest of your server.

# Goal: Guess All Easy Words

Your goal is to modify the final code from the previous step to automatically guess all easy words. You are free to do so in any way you like, except by reverse engineering the Wordle API. The creator of this API has asked that you do not reverse engineer it. He wants you to use the API as intended. Otherwise, he will be very sad. And you don't want to make him sad, do you? 😢

# Bonus Goal: Guess All Hard Words

The hard words are randomly generated using other randomly generated WordlePreferences. Read from this channel and try to guess all the hard words as well, if you dare.

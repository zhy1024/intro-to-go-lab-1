# Intro to Go Lab 1: Imperative Programming

> If you're stuck look at examples on [Go by Example](https://gobyexample.com/)

## Setting up Go

**Before starting this lab**, make sure that your machine has Go correctly installed and your favourite editor/IDE properly configured. Go is supported by Linux, macOS and Windows. However, Lab 4 and the coursework use shell scripts and Makefiles so please avoid using Windows.

**If you're using the 2.11 lab machines** we wrote a quick setup guide for configuring Go and VS Code.

**If you're using your own machine** we prepared a series of videos to help you get started.

*You'll find all guides, videos and transcripts on the Unit Page on Blackboard.*

## Question 1 - Hello World

Below is a complete 'Hello World' program written in Go:

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello World")
}
```

### Question 1a

Type the above program into a new file `hello.go` (don't just copy and paste). To run your code you can either use `go run hello.go` or `go build hello.go` followed by `./hello`. Verify that Hello World is printed in both cases.

### Question 1b

Modify `hello.go` so that it uses a for loop to print Hello World 20 times.

## Question 2 - Quiz

Open `quiz.go`. It's a skeleton for a quiz program. Write a `main()` using the provided helper functions so that your program asks the 6 questions from `quiz-questions.csv` and prints out the final score at the end.

<details>
    <summary>Hint 1</summary>

Use `s := score(0)` to initialise your score variable.

</details>

<details>
    <summary>Hint 2</summary>

Use a [for-range loop](https://gobyexample.com/range) to ask all the questions.

</details>

## Question 3 - Arrays vs Slices

Open `sequences.go`.

### Question 3a

Implement `mapSlice` and `mapArray` using [for-range loops](https://gobyexample.com/range).

They are the same as Haskell's map. For example mapping `addOne` onto `[5, 10, 15]` should return `[6, 11, 16]`.

### Question 3b

In `main()`:

- Create a slice `intsSlice` with values `[1, 2, 3]`.
- Map `addOne` onto this slice.
- Print `intsSlice`.

- Create an array `intsArray` of length 3 with values `[1, 2, 3]`.
- Map `addOne` onto this array.
- Print `intsArray`.

Explain the result. Modify the skeleton to solve any issues that you may have observed.

<details>
    <summary>Hint</summary>

How are slices different from arrays? What exactly are they?

</details>

### Question 3c

Change the definitions of `intsArray` and `intsSlice` so that they both contain values `[1, 2, 3, 4, 5]`. Without modifying `mapSlice` or `mapArray` run your new program. Explain the result.

### Question 3d

Slices support a “slice” operator with the syntax `slice[lowIndex:highIndex]`. It allows you to cut out a portion of your slice. For example:

```go
// Given: intsSlice  = [2, 3, 4, 5, 6]
newSlice := intsSlice[1:3]  
// newSlice = [3, 4]
```

Define `newSlice` as shown above, map `square` onto `newSlice` and print both `newSlice` and the original `intSlice`. Explain the result.

### Question 3e

The function `double` should append a slice onto itself. For example, given `[5, 6, 7]` it should return `[5, 6, 7, 5, 6, 7]`. In `main`, try doubling and then printing your `intsSlice`. Explain the result. Modify the skeleton to solve any issues that you may have observed.

### Question 3f

Given the differences that you found between arrays and slices:

- Explain how arrays and slices are passed to functions.
- Explain how `append()` works.
- Give use cases for arrays and slices.

## Question 4 - Game of Life

Time to test what you've learnt! 

Open `gol.go`. This is a skeleton for a program that can run a game of life simulation. It contains everything you need to implement a serial game of life, it is missing a complete `round(current [][]byte, size Size) [][]byte` function. The purpose of this function is to complete one round of game of life. It has two arguments: `current` this is the current state of the grid; `size` this is a struct with two properties `height` and `width` of `current` and `next`. It should return a 2D-slice containing the new grid.

TODO: Skeleton, is a serial GoL, reads in PGM and calls round function number of times needed to make the image change to wink face. Use SDL but set that up so it just happens each round? At the end output the file to a pgm.

### What is Game of Life?

The British mathematician John Horton Conway devised a cellular automaton named ‘The Game of Life’. The game resides on a 2-valued 2D matrix, i.e. a binary image, where the cells can either be ‘alive’ (pixel value 255 - white) or ‘dead’ (pixel value 0 - black). The game evolution is determined by its initial state and requires no further input. Every cell interacts with its eight neighbour pixels: cells that are horizontally, vertically, or diagonally adjacent. At each matrix update in time the following transitions may occur to create the next evolution of the domain:

- any live cell with fewer than two live neighbours dies
- any live cell with two or three live neighbours is unaffected
- any live cell with more than three live neighbours dies
- any dead cell with exactly three live neighbours becomes alive

Consider the image to be on a closed domain (pixels on the top row are connected to pixels at the bottom row, pixels on the right are connected to pixels on the left and vice versa). A user can only interact with the Game of Life by creating an initial configuration and observing how it evolves. Note that evolving such complex, deterministic systems is an important application of scientific computing, often making use of parallel architectures and concurrent programs running on large computing farms.


### Task

Complete the `round` function so that it can complete a single round of game of life. 

## Question 5 - Concurrent Hello World

A goroutine is a lightweight thread of execution. Modify your `hello.go` so that it uses a for loop to start 5 goroutines and print `Hello from goroutine i` where `i` is the number of the goroutine.

Example output:

```bash
$ go run hello.go

Hello from goroutine 2
Hello from goroutine 3
Hello from goroutine 4
Hello from goroutine 0
Hello from goroutine 1
```

<details>
    <summary>Hint 1 - How do I start a new goroutine?</summary>

Starting a goroutine is easy, just say:

```go
go someFunc()
```

</details>

<details>
    <summary>Hint 2 - Why does my program exit without printing anything?</summary>

You may notice that your program exits without printing anything. For now you can fix this by placing this after your for loop:

```go
time.Sleep(1 * time.Second)
```

Soon you'll see how to fix this problem with channels.

</details>


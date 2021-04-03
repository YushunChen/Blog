# Special Statements

## Goto statement

 In Go, goto statement is used to alter the normal execution of a program and transfer control to a labeled statement in the same program. The label is an identifier, it can be any plain text and can be set anywhere in the Go program above or below to goto statement.

```go
package main

import "fmt"

func main() {

	var age int
election:
	fmt.Println("Enter your age ")
	fmt.Scanln(&age)
	if age <= 21 {
		fmt.Println("You cannot drink!")
		goto election
	} else {
		fmt.Print("You can drink!") // program terminates here
	}

}
```

```go
Enter your age 
13
You cannot drink!
Enter your age
40
You can drink!
```



## Break Statement

In Go, break statement gives you way to break or terminate the execution of innermost “for”, “switch”, or “select” statement that containing it, and transfers the execution to the next statement following it. It is similar to many other languages.

## Labeled Break Statement

The standard unlabeled break statement is used to terminates the nearest enclosing statement. The labeled break statement uses a label after the break statement.

```go
package main

import "fmt"

func main() {

	var i = 0
	var j = 0

outer:
	for i <= 10 {
		i++
		for j <= 5 {
			if j == 3 {
				break outer
			}
			fmt.Printf("Inside loop %d\n", j)
			j++
		}
	}
	fmt.Println("Out of loop")

}
```

```go
Inside loop 0
Inside loop 1
Inside loop 2
Out of loop
```



## Continue Statement

The continue statement gives you way to skip over the current iteration of any loop. It is similar to many other languages.

## Labeled Continue Statement

The standard unlabeled continue statement is used to skip the current iteration of nearest enclosing loop. The labeled continue statement uses a label after the continue statement.

```go
package main

import "fmt"

func main() {

	var i = 0
	var j = 0

outerfor:
	for i < 3 {
		j = 0
		i++
		for j < 3 {
			j++
			fmt.Printf("i is %d and j is %d\n", i, j)
			if i == 2 {
				fmt.Println("continue here")
				continue outerfor
			}
		}

	}

}
```

```go
i is 1 and j is 1
i is 1 and j is 2
i is 1 and j is 3
i is 2 and j is 1
continue here
i is 3 and j is 1
i is 3 and j is 2
i is 3 and j is 3
```


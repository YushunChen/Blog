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


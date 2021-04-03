# Decision Making

| STATEMENT | DESCRIPTION |
| :--- | :--- |
| if Statements | Block of statement executed only when specified test expression is true. |
| if else Statements | When we want to execute some block of code if a condition is true and another block of code if a condition is false, In such a case we use if….else statement. |
| nested If Statements | When there is an if statement inside another if statement then it is known as nested if else. |
| switch Statement | A switch statement evaluates an expression against multiple cases in order to identify the block of code to be executed. |

{% hint style="info" %}
Above statements are standard as in many other languages, such as C and Java.
{% endhint %}

### 

### If with short statement

In Go, the conditional expression can be preceded by a simple statement, which is executes before the conditional expression is evaluated, and if it is a declaration statement then the variable declared in the statement will only be available inside the if block and it’s else or else-if sections.

```go
package main

import "fmt"

func main() {

	if x := 3; x%2 == 0 {
		fmt.Printf("%d is even\n", x)
	} else {
		fmt.Printf("%d is odd\n", x)
	}

}
```

```go
3 is odd
```

### 

### Switch Statement \(single cases\)

```go
package main

import "fmt"

func main() {
  var dayOfWeek = 5
	switch dayOfWeek {
	case 1:
		fmt.Println("Today is Monday.")
	case 2:
		fmt.Println("Today is Tuesday.")
	case 3:
		fmt.Println("Today is Wednesday.")
	case 4:
		fmt.Println("Today is Thursday.")
	case 5:
		fmt.Println("Today is Friday.")
	case 6:
		fmt.Println("Today is Saturday.")
	case 7:
		fmt.Println("Today is Sunday.")
	default:
		fmt.Println("Invalid weekday!")
	}
}
```

```go
Today is Friday.
```

### 

### Switch Statement \(multiple cases\)

```go
package main

import "fmt"

func main() {

	var dayOfWeek = 3
	switch dayOfWeek {
	case 1, 2, 3, 4, 5:
		fmt.Println("It's a weekday.")
	case 6, 7:
		fmt.Println("It's the weekend!")
	default:
		fmt.Println("Invalid day!")
	}

}
```

```go
It's a weekday.
```

### 

### Switch Statement - fallthrough

All the following cases are executed after a match is found in the switch statement cases.

```go
package main

import "fmt"

func main() {

	var x = 2
	switch x {
	case 1:
		fmt.Println("1")
		fallthrough
	case 2:
		fmt.Println("2")
		fallthrough
	case 3:
		fmt.Println("3")
	}

}

```

```go
2
3
```



### Switch Statement - Short Statement

Similar to short statement for if statement.

```go
package main

import "fmt"

func main() {

	switch dayOfWeek := 5; dayOfWeek {
	case 1, 2, 3, 4, 5:
		fmt.Println("It's a weekday.")
	case 6, 7:
		fmt.Println("It's the weekend!")
	default:
		fmt.Println("Invalid day!")
	}

}
```

```go
It's a weekday.
```



### Switch Statement - No Expression

```go
package main

import "fmt"

func main() {
	var marks = 40
	switch {
	case marks > 60:
		fmt.Println("You got A!")
	case marks < 60 && marks >= 50:
		fmt.Println("You got B.")
	case marks < 50 && marks >= 35:
		fmt.Println("You got C :(")
	default:
		fmt.Println("Failed!")
	}
}
```

```go
You got C :(
```




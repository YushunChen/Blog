# Loops

## For Loop

```go
package main

import "fmt"

func main() {
	sum := 0
	for i := 1; i < 10; i++ {
		sum += i
	}
	fmt.Println(sum)
}
```

```bash
45
```

## While Loop \(or just For Loop\)

{% hint style="info" %}
If we only have the middle statement of the for loop \(condition\), then the for loop behaves like a while loop as in other languages.
{% endhint %}

```go
package main

import "fmt"

func main() {
	power := 1
	for power < 4 {
		power *= 3
	}
	fmt.Println(power)
}

```

```bash
9
```

{% hint style="info" %}
If we go one step further, removing the condition will result in an infinite loop.
{% endhint %}

```go
package main

import "fmt"

func main() {
	sum := 0
	for { // infinite loop!
		sum++ 
	}
	fmt.Println(sum) // unreachable code
}
```



## Range Keyword in For Loops

### Syntax:

```go
for key, value := range collection {
    // statements
}
```

### Example1 - Array:

```go
package main

import "fmt"

func main() {

	langs := []string{"Go", "C", "C++", "Java"}
	for i, s := range langs {
		fmt.Println(i, s)
	}
}

```

```bash
0 Go
1 C
2 C++
3 Java
```

### Example2 - String:

```go
package main

import "fmt"

func main() {

	for i, s := range "Oliver" {
		fmt.Printf("%U represents %c and it is at position %d\n", s, s, i)
	}
}

```

```bash
U+004F represents O and it is at position 0
U+006C represents l and it is at position 1
U+0069 represents i and it is at position 2
U+0076 represents v and it is at position 3
U+0065 represents e and it is at position 4
U+0072 represents r and it is at position 5
```

### Example3 - Map:

In Go, `range` on map iterates over key/value pairs. It can also iterate over just the keys of a map.[  
](https://www.w3adda.com/golang-tutorial/go-decision-making)

```go
package main

import "fmt"

func main() {

	fruits := map[string]string{"A": "Apple", "B": "Banana", "C": "Cherry"}
	// iterate over key value pairs
	for key, value := range fruits {
		fmt.Printf("%s -> %s\n", key, value)
	}
	// iterate over the keys
	for key := range fruits {
		fmt.Println("Key: ", key)
	}
}

```

```bash
A -> Apple
B -> Banana
C -> Cherry
Key:  A
Key:  B
Key:  C
```

### Example3 - Channel\*\(Discussed Later\):

```go
package main

import "fmt"

func main() {

	ch := make(chan string)
	go func() {
		ch <- "O"
		ch <- "L"
		ch <- "I"
		ch <- "V"
		ch <- "E"
		ch <- "R"
		close(ch)
	}()
	for n := range ch {
		fmt.Print(n)
	}
}
```

```bash
OLIVER
```




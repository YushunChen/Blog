# Functions

### Declaration

A function can take 0 or more arguments. The type comes after the variable name, as mentioned before (same here for functions). The reason for that can be found here:

{% embed url="https://blog.golang.org/declaration-syntax" %}

To be short, using the same example in the blog,

`func main(argc int, argv []string) int` is a nice order because you can just read it off from this function declaration: function main takes an int and a slice of strings and returns an int.

```go
package main

import "fmt"

func add(x int, y int) int {
	return x + y
}

func main() {
	fmt.Println(add(42, 13))
}
```

```go
func add(x, y int) int { // shorter version if x, y share a type
	return x + y
}
```

```bash
55
```

### Return values

A function can return any number of results. Return values may be named. If so, they are treated as variables defined at the top of the function.

A `return `statement without arguments returns the named return values. This is called "naked" return.

```go
package main

import "fmt"

func split(sum int) (x, y int) {
	x = sum * 4 / 9   // 20 * 4 / 9
	y = sum - x       // 20 - 8 
	return            // x, y
}

func main() {
	fmt.Println(split(20))
}
```

```bash
8 12
```

{% hint style="info" %}
Naked return statements should only be used in short functions. They hard readability in longer functions.
{% endhint %}

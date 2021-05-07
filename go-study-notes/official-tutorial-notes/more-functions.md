# More Functions

## Function Values

Functions are values too. They can be passed around just like other values. Function values may be used as function arguments and return values.

### Example

```go
package main

import (
	"fmt"
	"math"
)

func compute(fn func(float64, float64) float64) float64 {
	return fn(3, 4)
}

func main() {
	hypot := func(x, y float64) float64 {
		return math.Sqrt(x*x + y*y)
	}
	fmt.Println(hypot(5, 12))
	fmt.Println(compute(hypot))
	fmt.Println(compute(math.Pow))	
}
```

```bash
13
5
81
```

## Function Closures

Go functions may be closures. A closure is a function value that references variables from outside its body. The function may access and assign to the referenced variables; in this sense the function is "bound" to the variables.



### Example 1 \(No Parameter\)

```go
package main

import "fmt"

func increment() func() int {
    var x int
    return func() int {
        x++
        return x
    }
}

func main() {
    a := increment()
    b := increment()
    
    fmt.Println("a: ", a())
    fmt.Println("a: ", a())
    fmt.Println("a: ", a())
    
    fmt.Println("b: ", b())
}
```

```bash
a:  1
a:  2
a:  3
b:  1
```

{% hint style="info" %}
Notice here `a` and ~~`b`~~ have their own closure and each is bound to its own `x` variable
{% endhint %}

### Example 2 \(With Parameter\)

```go
package main

import "fmt"

func adder() func(int) int {	// two return types: a func and an int
	sum := 0
	return func(x int) int {		// return an anonymous function
		sum += x
		return sum
	}
}

func main() {
	pos, neg := adder(), adder()
	for i := 0; i < 10; i++ {
		fmt.Println(
			pos(i),
			neg(-1*i),
		)
	}
}
```

```bash
0 0
1 -1
3 -3
6 -6
10 -10
15 -15
21 -21
28 -28
36 -36
45 -45
```

{% hint style="info" %}
 The `adder` function returns a closure. Each closure is bound to its own `sum` variable.
{% endhint %}

### More About Closure

{% embed url="https://dev.to/spindriftboi/function-literals-and-closure-in-go-2hgn\#:~:text=A%20Function%20Literal%20is%20a,literal%20and%20the%20surrounding%20function.&text=when%20this%20function%20is%20invoked,I%20am%20a%20function%20literal!" caption="Great article!" %}






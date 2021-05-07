# Methods

There are no classes in Go. But, we can define methods on types.

A method is a function with special **receiver** argument. The receiver appears in its own argument list between the `func` keyword and the method name.

### Example \(Method\)

```go
package main

import (
    "fmt"
    "math"
)

type Vertex struct {
    X, Y float64
}

func (v Vertex) Dist() float64 {
    return math.Sqrt(v.X * v.X + v.Y * v.Y)
}

func main() {
    v := Vertex{5, 12}
    fmt.Println(v.Dist())
}
```

```go
13
```

{% hint style="info" %}
Note that methods are still functions, just with a receiver argument.
{% endhint %}

### Example \(Regular Function\)

```go
package main

import (
	"fmt"
	"math"
)

type Vertex struct {
	X, Y float64
}

func Dist(v Vertex) float64 {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

func main() {
	v := Vertex{5, 12}
	// written in regular function form
	// pass in v Vertex as paramter
	// same functionality
	fmt.Println(Dist(v))
}
```

```go
13
```


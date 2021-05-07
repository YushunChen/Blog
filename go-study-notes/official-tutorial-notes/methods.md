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

```bash
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

```bash
13
```

## Methods on Non-Struct Types

We can declare a method on non-struct types, too.

In this example we see a numeric type `MyFloat` with an `Abs` method.

You can only declare a method with a receiver whose type is defined in the **same package** as the method. You cannot declare a method with a receiver whose type is defined in another package \(which includes the built-in types such as `int`\).

```go
package main

import (
	"fmt"
	"math"
)

type MyFloat float64

func (f MyFloat) Abs() float64 {
	if f < 0 {
		return float64(-f)
	}
	return float64(f)
}

func main() {
	f := MyFloat(-math.Sqrt2)
	fmt.Println(f.Abs())
}
```

```bash
1.4142135623730951
```

{% hint style="info" %}
Here we see a numeric type `MyFloat` with an `Abs` method.
{% endhint %}

## Pointer Receivers

We can declare methods with pointer receivers. The receiver type has `*T` for some type `T` \(Note that `T` cannot be a pointer itself, say `*int`\)

### Example 1 \(Pointer Receiver\)

```go
package main

import (
	"fmt"
	"math"
)

type Vertex struct {
	X, Y float64
}

func (v Vertex) Abs() float64 {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

func (v *Vertex) Scale(f float64) {
	v.X = v.X * f
	v.Y = v.Y * f
}

func main() {
	v := Vertex{3, 4}
	v.Scale(10)
	fmt.Println(v.Abs())
}
```

```go
50
```

Methods with pointer receivers can modify the value to which the receiver points \(as `Scale` does here\). Since methods often need to modify their receiver, pointer receivers are more common than value receivers.

### Example 2 \(Value Receiver\)

```go
package main

import (
	"fmt"
	"math"
)

type Vertex struct {
	X, Y float64
}

func (v Vertex) Abs() float64 {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

func (v Vertex) Scale(f float64) {
	v.X = v.X * f
	v.Y = v.Y * f
}

func main() {
	v := Vertex{3, 4}
	v.Scale(10)
	fmt.Println(v.Abs())
}
```

```go
5
```

{% hint style="info" %}
We only removed the `*` from the function declaration of `scale`. Notice we do not need to change `v.Scale(10)` on line 23 to `(&v).Scale(10)`. Keep reading :\)
{% endhint %}

Now, with a value receiver, the original `Vertex` value is not changed.  This is because the `Scale` method operates on a **copy** of the original `Vertex` value. \(This is the same behavior as for any other function argument.\) The `Scale` method must have a pointer receiver to change the `Vertex` value declared in the `main` function.

### Example 3 \(Function Version\)

```go
package main

import (
	"fmt"
	"math"
)

type Vertex struct {
	X, Y float64
}

func Abs(v Vertex) float64 {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

func Scale(v *Vertex, f float64) {
	v.X = v.X * f
	v.Y = v.Y * f
}

func main() {
	v := Vertex{3, 4}
	Scale(&v, 10)
	fmt.Println(Abs(v))
}
```

```go
50
```

Here are the  `Abs` and `Scale` methods rewritten as functions. If we change this to passing by value \(instead of reference\) by just removing the `*` from line 16, the code would not compile:

```bash
./prog.go:23:8: cannot use &v (type *Vertex) as type Vertex in argument to Scale
```

We also need to change `&v` to `v`. And the output is:

```bash
5
```

## Methods and Pointer Indirection

The previous examples lead us to some differences the pointer and value receivers in actual code writing.


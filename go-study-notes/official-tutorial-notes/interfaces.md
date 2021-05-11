# Interfaces

An interface type is a set of method signatures. A value of interface type can hold any value that implements those methods.

### Example

```go
package main

import (
    "fmt"
    "math"
)

func main() {
	var a Abser
	f := MyFloat(-math.Sqrt2)
	v := Vertex{3, 4}

	a = f  // a MyFloat implements Abser
	fmt.Println(a.Abs())
	a = &v // a *Vertex implements Abser
	fmt.Println(a.Abs())
}

type MyFloat float64

func (f MyFloat) Abs() float64 {
	if f < 0 {
		return float64(-f)
	}
	return float64(f)
}

type Vertex struct {
	X, Y float64
}
```

```go
1.4142135623730951
5
```

{% hint style="info" %}
Note that in line 15, if we use `a = v` instead, there will be an error because `v` is of `Vertex` type and does not implement `Abser`.
{% endhint %}

## Implicit Implementation

Interfaces are implemented implicitly. A type implements an interface by implementing its methods. There is no explicit declaration of intent, no "implements" keyword. Implicit interfaces decouple the definition of an interface from its implementation, which could then appear in any package without prearrangement.

### Example

```go
package main

import "fmt"

type I interface {
    M()
}

type T struct {
    S string
}

// This method means type T implements interface I
func (t T) M() {
    fmt.Println(t.S)
}

func main() {
    var i I = T{"Oliver"}
    i.M()
}
```

```go
Oliver
```

## Interface Values

Interface values can be considered as a tuple of a value and a concrete type under the hood. An interface value holds a value of a specific underlying concrete type. ****Calling a method on an interface value executes the method of the same name on its underlying type.

### Example

```go
package main

import (
	"fmt"
	"math"
)

type I interface {
	M()
}

type T struct {
	S string
}

func (t *T) M() {
	fmt.Println(t.S)
}

type F float64

func (f F) M() {
	fmt.Println(f)
}

func main() {
	var i I

	i = &T{"Oliver"}
	printPair(i)
	i.M()

	i = F(math.Pi)
	printPair(i)
	i.M()
}

func printPair(i I) {
	// show value and type here
	fmt.Printf("(%v, %T)\n", i, i)
}

```

```go
(&{Oliver}, *main.T)
Oliver
(3.141592653589793, main.F)
3.141592653589793
```

### Nil Underlying Values

If the concrete value inside the interface itself is nil, the method will be called with a nil receiver.

A null pointer exception may be thrown in other languages, but in Go it is common to write methods that gracefully handle being called with a nil receiver, like the method `M` in the following example:

```go
package main

import "fmt"

type I interface {
	M()
}

type T struct {
	S string
}

func (t *T) M() {
	if t == nil {
		fmt.Println("<nil>")
		return
	}
	fmt.Println(t.S)
}

func main() {
	var i I

	var t *T
	i = t
	printPair(i)
	i.M()

	i = &T{"Oliver"}
	printPair(i)
	i.M()
}

func printPair(i I) {
	fmt.Printf("(%v, %T)\n", i, i)
}

```

```go
(<nil>, *main.T)
<nil>
(&{Oliver}, *main.T)
Oliver
```

### Nil Interface Values

A nil interface value holds neither value nor concrete type.

Calling a method on a nil interface is a **run-time error** because there is no type inside the interface tuple to indicate which concrete method to call:

```go
package main

import "fmt"

type I interface {
	M()
}

func main() {
	var i I
	printPair(i)
	i.M()
}

func printPair(i I) {
	fmt.Printf("(%v, %T)\n", i, i)
}

```

```go
(<nil>, <nil>)
panic: runtime error: invalid memory address or nil pointer dereference
[signal SIGSEGV: segmentation violation code=0x1 addr=0x0 pc=0x498fcf]
```

## Empty Interface




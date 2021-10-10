---
description: This is a long section...
---
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

```bash
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

```bash
Oliver
```

## Interface Values

Interface values can be considered as a tuple of a value and a concrete type under the hood. An interface value holds a value of a specific underlying concrete type.** **Calling a method on an interface value executes the method of the same name on its underlying type.

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

```bash
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

```bash
(<nil>, <nil>)
panic: runtime error: invalid memory address or nil pointer dereference
[signal SIGSEGV: segmentation violation code=0x1 addr=0x0 pc=0x498fcf]
```

## Empty Interface

The interface type that specifies zero methods is  the **empty interface**: `interface{} `An empty interface may hold values of any type, i.e., every type implements at least zero methods. Empty interfaces are used by code that handles values of unknown type. 

### Example

```go
package main

import "fmt"

func main() {
	var i interface{}
	printPair(i)

	i = 3.1415926
	printPair(i)
	
	i = 7
	printPair(i)

	i = "Oliver"
	printPair(i)
}

func printPair(i interface{}) {
	fmt.Printf("(%v, %T)\n", i, i)
}

```

```bash
(<nil>, <nil>)
(3.1415926, float64)
(7, int)
(Oliver, string)
```

{% hint style="info" %}
Here, `fmt.Print` takes any number of arguments of type `interface{}`.
{% endhint %}

## Type Assertions

A type assertion provides access to an interface value's underlying concrete value. `t:= i.(T)` means  the interface value `i` holds the concrete type `T` and assigns the underlying `T` value to the variable `t`. If `i` does not hold a `T`, the statement will trigger a panic.

To test whether an interface value holds a specific type, a type assertion can return two values: the underlying value and a boolean value that reports whether the assertion succeeded.

```go
t, ok = := i.(T)
```

If `i` holds a `T`, then `t` will be the underlying value and `ok` will be true.

Else, `ok` will be false and `t` will be the zero value of type `T`, and no panic occurs.

### Example

```go
package main

import "fmt"

func main() {
	var i interface{} = "hello"

	s := i.(string)
	fmt.Println(s)

	s, ok := i.(string)
	fmt.Println(s, ok)

	f, ok := i.(float64)
	fmt.Println(f, ok)

	f = i.(float64) // panic
	fmt.Println(f)
}
```

```bash
hello
hello true
0 false
panic: interface conversion: interface {} is string, not float64
```

{% hint style="info" %}
Note that the the usage of the two return values `s` and `ok` is similar to its usage when reading from a map.
{% endhint %}

## Type Switches

A type switch permits several type assertions in series. A type switch is similar to a regular switch statement, but the cases in a type switch specify types (not values), and those values are compared against the type of the value held by the given interface value.

 The declaration in a type switch has the same syntax as a type assertion `i.(T)`, but the specific type `T` is replaced with the keyword `type`.

### Example

```go
package main

import "fmt"

func print(i interface{}) {
    switch v := i.(type) {
        case int:
            fmt.Printf("%v is an integer\n", v)
        case string:
            fmt.Printf("%q is %v bytes long\n", v, len(v))
        default:
            fmt.Printf("I do not know about type %T\n", v)
    }
}

func main() {
	print(777)
	print("Oliver")
	print(true)
}
```

```bash
777 is an integer
"Oliver" is 6 bytes long
I do not know about type bool
```

{% hint style="info" %}
 This switch statement tests whether the interface value `i` holds a value of type `int` or `string`. In each case, the variable `v` will be of that type respectively and hold the value held by `i`. In the default case, the variable `v` is of the same interface type and value as `i`.
{% endhint %}

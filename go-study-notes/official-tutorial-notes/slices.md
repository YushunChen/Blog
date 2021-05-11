---
description: This is a long section...
---

# Slices

As mentioned before, an array's size is fixed. However, a slice is a **dynamically-sized** and flexible view into the elements of an array.

{% hint style="info" %}
In practice, slices are much more common than arrays.
{% endhint %}

The type `[]T` is a slice with elements of type T.

### Declaration

A slice is formed by specifying two indices, a low and high bound, separated by a colon. This selects a half-open range which includes the first element, but excludes the last one.

```go
a[low : high]

a[1 : 4]    // a slice includes 1 through 3 of `a`
```

### Example

```go
package main

import "fmt"

func main() {
	primes := [6]int{2, 3, 5, 7, 11, 13}

	var s []int = primes[1:4]
	fmt.Println(s)
}
```

```bash
[3 5 7]
```

## Consider Slices as References to Arrays

A slice is just a section of an underlying array. It does not store any data. Changing the elements of one slice changes the corresponding elements of its corresponding array. So, other slices that share the same underlying array would see the changes.

### Example

```go
package main

import "fmt"

func main() {
	names := [4]string{
		"Oliver",
		"Chen",
		"Yushun",
		"Chen",
	}
	fmt.Println(names)

	a := names[0:2]
	b := names[1:3]
	fmt.Println(a, b)

	b[0] = "XXX"
	fmt.Println(a, b)
	fmt.Println(names)
}
```

```bash
[Oliver Chen Yushun Chen]
[Oliver Chen] [Chen Yushun]
[Oliver XXX] [XXX Yushun]
[Oliver XXX Yushun Chen]
```

{% hint style="info" %}
`a` reflects the modification `b[0] = "XXX"` because a and b share the same underlying array, whose second element is changed by this modification.
{% endhint %}

## Slice Literals

A slice literal is like an array literal without the length. This is an **array literal**:

```go
[3]bool[true, false, true}
```

This is a **slice literal:**

```go
[]bool{true, false, true}
```

{% hint style="info" %}
 This create the same array as above, and builds a slice that references it.
{% endhint %}

### Example

```go
package main

import "fmt"

func main() {
	// slice literal of integers
	q := []int{2, 3, 5, 7, 11, 13}
	fmt.Println(q)

	// slice literal of booleans
	r := []bool{true, false, true, true, false, true}
	fmt.Println(r)

	// slice literal of structs
	s := []struct {
		i int
		b bool
	}{
		{2, true},
		{3, false},
		{5, true},
		{7, true},
		{11, false},
		{13, true},
	}
	fmt.Println(s)
}
```

```bash
[2 3 5 7 11 13]
[true false true true false true]
[{2 true} {3 false} {5 true} {7 true} {11 false} {13 true}]
```

## Slice Defaults

We can use defaults instead of specifying the low or high bounds. 

Consider an array `var a[10]int`. The following slide expressions are equivalent:

* `a[0:10]`
* `a[:10]`
* `a[0:]`
* `a[:]`

### Example

```go
package main

import "fmt"

func main() {
	s := []int{2, 3, 5, 7, 11, 13}

	s = s[1:4]
	fmt.Println(s)

	s = s[:2]
	fmt.Println(s)

	s = s[1:]
	fmt.Println(s)
}

```

```bash
[3 5 7]
[3 5]
[5]
```

{% hint style="info" %}
Notice how the references to `s` changes when re-assign a slide to it every time.
{% endhint %}

## Slice Length and Capacity

A slide has both a **length** and a **capacity**. 

|  | Length | Capacity |
| :--- | :--- | :--- |
| **Definition** | The number of elements the slice contains | The number of elements in the underlying array, counting from the first element in the slice |
| **Usage** | `len(s)` | `cap(s)` |

{% hint style="info" %}
A slice's length can be extended by re-slicing it, given that it has sufficient capacity.
{% endhint %}

### Example

```go
package main

import "fmt"

func main() {
	s := []int{2, 3, 5, 7, 11, 13}
	printSlice(s)

	// Slice the slice to give it zero length.
	s = s[:0]
	printSlice(s)

	// Extend its length.
	s = s[:4]
	printSlice(s)

	// Drop its first two values.
	s = s[2:]
	printSlice(s)
}

func printSlice(s []int) {
	fmt.Printf("len=%d cap=%d %v\n", len(s), cap(s), s)
}
```

```bash
len=6 cap=6 [2 3 5 7 11 13]
len=0 cap=6 []
len=4 cap=6 [2 3 5 7]
len=2 cap=4 [5 7]
```

## Zero Value

The zero value of a slice is `nil`. A nil slice has a length and capacity of 0 and has no underlying array.

## `Make` a Slice

Remember we mentioned that arrays are fix-sized. Now, we can create dynamically-sized arrays using the built-in `make` function.

The make function allocates a zeroed array and returns a slice that refers to that array. The first argument is the array type; the second is the length; the third is the capacity.

### Example

```go
package main

import "fmt"

func main() {
	a := make([]int, 5)
	printSlice("a:", a)

	b := make([]int, 0, 5)
	printSlice("b:", b)

	c := b[:2]
	printSlice("c:", c)

	d := c[2:5]
	printSlice("d:", d)
}

func printSlice(s string, x []int) {
	fmt.Printf("%s len=%d cap=%d %v\n", s, len(x), cap(x), x)
}
```

```bash
a: len=5 cap=5 [0 0 0 0 0]
b: len=0 cap=5 []
c: len=2 cap=5 [0 0]
d: len=3 cap=3 [0 0 0]
```

## Slices of Slices

Since slices can contain any type, they can also contain other slices.

### Example \(Tic-Tac-Toe board: 2D array\)

```go
package main

import (
	"fmt"
	"strings"
)

func main() {
	// Create a tic-tac-toe board.
	board := [][]string{
		[]string{"_", "_", "_"},
		[]string{"_", "_", "_"},
		[]string{"_", "_", "_"},
	}

	// The players take turns.
	board[0][0] = "X"
	board[2][2] = "O"
	board[1][2] = "X"
	board[1][0] = "O"
	board[0][2] = "X"

	for i := 0; i < len(board); i++ {
		fmt.Printf("%s\n", strings.Join(board[i], " "))
	}
}
```

```bash
X _ X
O _ X
_ _ O
```

## Append Function

The first parameter `s` of `append` is a slice of type `T`, and the rest are `T` values to append to the slice.

The resulting value of `append` is a slice containing all the elements of the original slice plus the provided values. If the backing array of `s` is too small to fit all the given values a bigger array will be allocated. The returned slice will point to the newly allocated array.

### Example

```go
package main

import "fmt"

func main() {
    var s []int
    printSlice(s)
    
    // append on nil slices
    s = append(s, 0)
    printSlice(s)
    
    // the slice grows as needed
    s = append(s, 1)
    printSlice(s)
    
    // add more than 1 element at a time
    s = append(s, 2, 3, 4, 5)
    printSlice(s)
}

func printSlice(s []int) {
	fmt.Printf("len=%d cap=%d %v\n", len(s), cap(s), s)
}
```

```bash
len=0 cap=0 []
len=1 cap=1 [0]
len=2 cap=2 [0 1]
len=6 cap=6 [0 1 2 3 4 5]
```

## More on Slices

{% embed url="https://blog.golang.org/slices-intro" %}




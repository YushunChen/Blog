---
description: 'Warning: Long Section'
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

```go
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

```go
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

```go
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

```go
[3 5 7]
[3 5]
[5]
```

{% hint style="info" %}
Notice how the references to `s` changes when re-assign a slide to it every time.
{% endhint %}


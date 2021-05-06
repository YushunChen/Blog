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


# Arrays

The type `[n]T` is an array of `n` values of type `T`.

### Declaration

```go
var a [10]int    // a variable `a` as an array of 10 integers
```

{% hint style="info" %}
An array's length is part of its type, so arrays can't be resized. Don't worry about this limitation for now. There is a convenient way later.
{% endhint %}

### Example

```go
package main

import "fmt"

func main() {
    var a [2]string
    a[0] = "Oliver"
    a[1] = "Chen"
    fmt.Println(a[0], a[1])
    fmt.Println(a)
    
    numbers := [7]int{1, 2, 3, 4, 5, 6, 7}
    fmt.Println(numbers)
}
```

```go
Oliver Chen
[Oliver Chen]
[1 2 3 4 5 6 7]
```


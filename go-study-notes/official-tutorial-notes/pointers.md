# Pointers

A pointer holds the memory address of a value.

### Declaration

```go
var p *int         // *T means a pointer to a T value

i := 2
p = &i             // & operator generates a pointer to its operand

fmt.Println(*p)    // * operatos is used for dereferencing
*p = 21
```

{% hint style="info" %}
There is no pointer arithmetic in Go, unlike C.
{% endhint %}

### Example

```go
package main

import "fmt"

func main() {
    i, j := 18, 7799
    
    p := &i            // pointer to i
    fmt.Println(*p)    // read i from the pointer
    
    *p = 19            // change i from the pointer
    fmt.Println(i)
    
    p = &j             // re-assign the pointer to j
    *p = *p / 7
    fmt.Println(j)
}
```

```go
18
19
1114
```




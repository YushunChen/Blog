# Structs

A `struct`  is a collection of fields. Struct fields are accessed using a dot.

### Example

```go
package main

import "fmt"

type Vertex struct {
    X int
    Y int
}

func main() {
    fmt.Println(Vertex{1, 2})
    
    v := Vertex{1, 2}
    v.X = 4
    fmt.Println(v.X)
}
```

```bash
{1 2}
4
```

## Pointers to Structs

Struct fields can also be accessed using a struct pointer.

```go
package main

import "fmt"

type Vertex struct {
    X int
    Y int
}

func main() {
    v := Vertex{1, 2}
    p := &v           // struct pointer p
    p.X = 1e9
    // (*p).X = 9     // output would be {9 2}
    fmt.Println(v)
}
```

```bash
{1000000000 2}
```

{% hint style="info" %}
We could write `(*p).X` to access the field `X` of the `Vertex` struct. However, this is a cumbersome notation. So, Go allows us to use **`p.X`** without this explicit derefence.
{% endhint %}

## Struct Literals

A struct literal denotes a newly allocated struct value by listing the values of its fields. The predix `&` returns a pointer to the struct value.

```go
package main

import "fmt"

type Vertex struct {
    X, Y int
}

var (
    v1 = Vertex{1, 2}
    v2 = Vertex{X: 1}    // using Name: syntax; Y: 0 is implicit
    v3 = Vertex{}        // X:0 and Y:0
    p = &Vertex{1, 2}    // has type *Vertex
)

func main() {
    fmt.Println(v1, v2, v3, p)
}

```

```bash
{1 2} {1 0} {0 0} &{1 2}
```


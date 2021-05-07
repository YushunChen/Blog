# Maps

A map maps keys to values. The zero value of a map is `nil`. A `nil` map has no keys, nor can keys be added.

The `make` function returns a map of the given type, initialized and ready for use.

### Example

```go
package main

import "fmt"

type Vertex struct {
    Lat, Long, float64
}

var m map[string]Vertex

func main() {
    m = make(map[string]Vertex)
    m["Bell Labs"] = Vertex{
        40.68433, -74.39967,
    }
    fmt.Println(m["Bell Labs"])
}
```

```bash
{40.68433 -74.39967}
```

## Map Literals

Map literals are like struct literals, but the keys are required.

### Example

```go
package main

import "fmt"

type Vertex struct {
	Lat, Long float64
}

var m = map[string]Vertex{
	"Bell Labs": Vertex{
		40.68433, -74.39967,
	},
	"Google": Vertex{
		37.42202, -122.08408,
	},
}

func main() {
	fmt.Println(m)
}
```

```bash
map[Bell Labs:{40.68433 -74.39967} Google:{37.42202 -122.08408}]
```


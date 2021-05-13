# Goroutines

A goroutine is a lightweight thread managed by the Go runtime: `go f(x, y, z)` starts a new running goroutine `f(x, y, z)`. The evaluation of `f`, `x`, `y`, and `z` happens in the current goroutine and the execution of `f` happens in the new goroutine.

 Goroutines run in the same address space, so access to shared memory must be synchronized. The [`sync`](https://golang.org/pkg/sync/) package provides useful primitives, but there are other primitives to be used more commonly. \(introduced later\)

### Example

```go
package main

import (
	"fmt"
	"time"
)

func print(s string) {
	for i := 0; i < 5; i++ {
		time.Sleep(100 * time.Millisecond)
		fmt.Println(s)
	}
}

func main() {
	go print("Oliver")
	print("Hello!")
}
```

```bash
Hello!
Oliver
Oliver
Hello!
Hello!
Oliver
Oliver
Hello!
Hello!
```


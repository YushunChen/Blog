# Variables

## Syntax

```go
var <name> <type>
var <name> <type> = <expression>
```

```go
package main
import "fmt"
 
func main(){
    var hello_str string
    hello_str="Hello, World!"
    fmt.Println(hello_str)
}
```



## Variables with Initializers

The type can be omitted if there is an initializer. The variables takes the type of the initializer.

```go
package main

import "fmt"

var i, j int = 1, 2

func main() {
	var c, python, java = true, false, "no!"
	fmt.Println(i, j, c, python, java)
}
```

```bash
1 2 true false no!
```



## Short Variable Declarations

Inside a function, the `:=` short assignment statement can be used in place of a `var` declaration with implicit type.

Outside a function, every statement begins with a keyword \(`var`, `func`, and so on\) and so the `:=` construct is not available.

```go
package main

import "fmt"

func main() {
	var i, j int = 1, 2
	k := 3
	c, python, java := true, false, "no!"

	fmt.Println(i, j, k, c, python, java)
}
```

```bash
1 2 3 true false no!
```



## Zero Values

| TYPES | ZERO VALUES |
| :--- | :--- |
| Numeric types | 0 |
| Boolean type | false |
| Strings | "" \(empty string\) |

```go
package main

import "fmt"

func main() {
	var i int
	var f float64
	var b bool
	var s string
	fmt.Printf("%v %v %v %q\n", i, f, b, s)
}
```

```bash
0 0 false ""
```


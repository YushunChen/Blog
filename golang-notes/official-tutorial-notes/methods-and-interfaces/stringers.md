# Stringers

 One of the most ubiquitous interfaces is [`Stringer`](https://golang.org/pkg/fmt/#Stringer) defined by the [`fmt`](https://golang.org/pkg/fmt/) package:

```go
type Stringer interface {
    String() string
}
```

  A `Stringer` is a type that can describe itself as a string. The `fmt` package (and many others) look for this interface to print values.

### Example

```go
package main

import "fmt"

type Person struct {
	Name string
	Age  int
}

func (p Person) String() string {
	return fmt.Sprintf("%v (%v years)", p.Name, p.Age)
}

func main() {
	a := Person{"Oliver Chen", 20}
	z := Person{"Yulin Chen", 4}
	fmt.Println(a, z)
}

```

```bash
Oliver Chen (20 years) Yulin Chen (4 years)
```

### Exercise

Make the `IPAddr` type implement `fmt.Stringer` to print the address as a dotted quad.

For instance, `IPAddr{1, 2, 3, 4}` should print as `"1.2.3.4"`.

```go
package main

import "fmt"

type IPAddr [4]byte

// TODO: Add a "String() string" method to IPAddr.
func (ip IPAddr) String() string {
	return fmt.Sprintf("%v.%v.%v.%v", ip[0], ip[1], ip[2], ip[3])
}

func main() {
	hosts := map[string]IPAddr{
		"loopback":  {127, 0, 0, 1},
		"googleDNS": {8, 8, 8, 8},
	}
	for name, ip := range hosts {
		fmt.Printf("%v: %v\n", name, ip)
	}
}

```

```bash
googleDNS: 8.8.8.8
loopback: 127.0.0.1
```

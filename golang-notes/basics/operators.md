# Operators

## Types of Operators

* Arithmetic Operators
* Assignment Operators
* Comparison (Relational) Operators
* Logical Operators
* Bitwise Operators

### Arithmetic Operators

```go
package main
import "fmt"
func main() {
    var a int=20
    var b int=11
    fmt.Println(a+b)
    fmt.Println(a-b)
    fmt.Println(a*b)
    fmt.Println(a/b)
    fmt.Println(a%b)
}
```

```bash
31
9
220
1
9
```

### Assignment Operators

```go
package main
import "fmt"
func main() {
    var a int=30
    var b int=5
 
    a+=b
    fmt.Printf("a+=b :%d\n", a)
    a-=b
    fmt.Printf("a-=b :%d\n", a)
    a*=b
    fmt.Printf("a*=b :%d\n", a)
    a/=b
    fmt.Printf("a/=b :%d\n", a)
    a%=b
    fmt.Printf("a%%=b :%d\n", a)
}
```

```bash
a+=b :35
a-=b :30
a*=b :150
a/=b :30
a%=b :0
```

Other assignment operators:

| Operator | Description                     |
| -------- | ------------------------------- |
| <<=      | Left shift and assign           |
| >>=      | Right shift and assign          |
| &=       | Bitwise AND assign              |
| ^=       | Bitwise exclusive OR and assign |
| \|=      | Bitwise inclusive OR and assign |

### Comparison Operators

* \> greater than
* < less than
* \>= greater than or equal to
* <= less than or equal to 
* \== is equal to
* != not equal to

### Logical Operators

* && Logical AND
* || Logical OR
* ! Logical NOT

### Bitwise Operators

* & bitwise AND
* \| bitwise OR
* ^ bitwise NOT
* &^ bit clear (AND NOT)

### Other Operators

| Operator | Name                   | Description                                                   |
| -------- | ---------------------- | ------------------------------------------------------------- |
| &        | Address of             | \&a generates a pointer to a                                  |
| \*       | Pointer to             | \*a denotes the variable pointed to by a                      |
| <-       | Receive Operator       | <-ch is the value received from channel ch                    |
| +=       | String concat operator | Strings can be concatenated using + or += assignment operator |

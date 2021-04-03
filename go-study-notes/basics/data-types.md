# Data Types

## Introduction

Go is statically typed, meaning variables always have a specific type and that type cannot change.

Data Type for a variable defines:

* The amount of memory space allocated for variables.
* A data type specifies the possible values for variables.
* The operations that can be performed on variables.

Go built-in data types:

* Numbers
* Boolean 
* String

### Integer

#### Signed integers

<table>
  <thead>
    <tr>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Size</th>
      <th style="text-align:left">Description (Two&apos;s complement)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">int8</td>
      <td style="text-align:left">8 bits</td>
      <td style="text-align:left">8 bit signed integer</td>
    </tr>
    <tr>
      <td style="text-align:left">int16</td>
      <td style="text-align:left">16 bits</td>
      <td style="text-align:left">16 bit signed integer</td>
    </tr>
    <tr>
      <td style="text-align:left">int32</td>
      <td style="text-align:left">32 bits</td>
      <td style="text-align:left">32 bit signed integer</td>
    </tr>
    <tr>
      <td style="text-align:left">int64</td>
      <td style="text-align:left">64 bits</td>
      <td style="text-align:left">
        <p>64 bit signed integer,</p>
        <p>can also be represented in octal and hexadecimal</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>int</b>
      </td>
      <td style="text-align:left">Platform dependent</td>
      <td style="text-align:left">signed integers of at least 32-bit in size, not equivalent to int32.</td>
    </tr>
  </tbody>
</table>

#### Unsigned integers

| Type | Size | Description \(Two's complement\) |
| :--- | :--- | :--- |
| uint8 | 8 bits | 8 bit unsigned integer |
| uint16 | 16 bits | 16 bit unsigned integer |
| uint32 | 32 bits | 32 bit unsigned integer |
| uint64 | 64 bits | 64 bit unsigned integer |
| uint | Platform dependent | unsigned integers of at least 32-bit in size, not equivalent to int32. |

{% hint style="info" %}
Use **int** unless for specific reasons for others. Integral types have default value of 0. Octal numbers can be declared using prefix and hexadecimal using the **0x** prefix.
{% endhint %}

#### Other integer types

| Type | Description \(Two's complement\) |
| :--- | :--- |
| byte | It is alias for and equivalent to uint8 |
| rune | It is alias for and equivalent to int32, used to represent characters. |
| uintptr | It is used to hold memory address pointers |

{% hint style="info" %}
Golang does not support a char data type, instead it has **byte** and **rune** to represent character values. This helps to distinguish characters from integer values. **byte** data type is represented with a ASCII value and the **rune** data type is represented with Unicode value encoded in UTF-8 format.
{% endhint %}

```go
package main
import "fmt"
 
func main() {
 var varByte byte = 'a' // ASCII value of 97
 var varRune rune = '♥' // Unicode value of U+2665
 
 fmt.Printf("%c = %d and %c = %U\n", varByte, varByte, varRune, varRune)
}
```

```go
a = 97 and ♥ = U+2665
```

#### Float

Go supports float32 and float64 represented with 32-bit and 64-bit in memory respectively.

```go
var num1 float32 = 20.0320
var num2 = 20.0818 // Type inferred as float64
```

#### Complex Numbers

Go supports complex64 and complex128. Each of the type uses float32 and float64 respectively, to represent their real and imaginary parts.

```go
var num1 = 3 + 7i  // Type inferred as complex128
```

### 

### Boolean

```go
var flag = true
```

### 

### String

```go
// No newlines, and can contain escape sequences like \n, \t
var fstr="Hello World"
 
// Can span multiple lines. Escape characters are not allowed.
var sstr= `Hello world, this
a multi-line text string.`
```



## Type Conversions

#### Syntax: The expression `T(v)` converts the value `v` to the type `T`.

```go
var i int = 42
var f float64 = float64(i)
var u uint = uint(f)
```

```go
// short syntax
i := 42
f := float64(i) // 42.000000
u := uint(f)
```



## Type Inference

When declaring a variable without specifying an explicit type \(either by using the `:=` syntax or `var =` expression syntax\), the variable's type is inferred from the value on the right hand side.

```go
package main

import "fmt"

func main() {
	i := 42
	f := 12.0212
	c := 0.5 + 2i
	fmt.Printf("i is of type %T\n", i)
	fmt.Printf("f is of type %T\n", f)
	fmt.Printf("c is of type %T\n", c)
}
```

```go
i is of type int
f is of type float64
c is of type complex128
```


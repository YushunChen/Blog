# Channels

A channel is a typed conduit/tube through which we send and receive values with the channel operator `<-`.

```go
ch <- v        // send v to channel ch
v := <-ch      // receive from channel ch and store the value in v
```

{% hint style="info" %}
The data flows in the direction of the arrow `<-`
{% endhint %}

We can create channels similar to creating maps and slices using the `make` function:

```go
ch := make(chan int)
```

By default, sends and receives block until the other side is ready. This allows goroutines to synchronize without explicit locks or condition variables.

### Example

```go
package main

import "fmt"

func sum(s []int, ch chan int) {
    sum := 0
    for _,v := range s {
        sum += v
    }
    ch <- sum 
}

func main() {
    s := []int{9, 8, 7, 5, 4, 0, -9, -8}
    ch := make(chan int)
    
    go sum(s[:len(s)/2], ch)    // 4+0-9-8=-13
    go sum(s[len(s)/2:], ch)    // 9+8+7+5=29
    x, y := <-ch, <-ch
    
    fmt.Println(x, y, x+y)
}
```

```go
-13 29 -16
```

{% hint style="info" %}
The example code sums the numbers in a slice, distributing the work between two goroutines. Once both goroutines have completed their computation, it calculates the final result.
{% endhint %}

## Buffered Channels

Channels can be buffered. Provide the buffer length as the second argument to `make` to initialize a buffered channel:

```go
ch := make(chan int, 100)
```

Sends to a buffered channel block only when the buffer is full. Receives block when the buffer is empty.

### Example

```go
package main

import "fmt"

func main() {
	ch := make(chan int, 2)
	ch <- 1
	ch <- 2
	// ch <- 3
	fmt.Println(<-ch)
	fmt.Println(<-ch)
}
```

```go
1
2
```

{% hint style="info" %}
If we overfill the buffer using the commented code on line 9, we would get: `fatal error: all goroutine are asleep - deadlock!`
{% endhint %}

z = z- ((z*z - x) / (2*z))
```go
func Sqrt(x float64) float64 {
	z:= 1.0
	z_before := 0.0
	fmt.Println(z-z_before < 0.001)
	for i:=0; z!=z_before;i++ {
		z_before = z
		z = z- ((z*z - x) / (2*z))
		fmt.Println(i,z,x)
	}
	return z
}
```


### pointer receiver
The first is so that the method can modify the value that its receiver points to.
The second is to avoid copying the value on each method call. This can be more efficient if the receiver is a large struct, for example.

```go
func (v *Vertex) Scale(f float64) {
	v.X = v.X * f
	v.Y = v.Y * f
}

func (v *Vertex) Abs() float64 {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

```

#### Interfaces
There is no explicit declaration of intent, no "implements" keyword.

Implicit interfaces decouple the definition of an interface from its implementation, which could then appear in any package without prearrangement.
```go
type I interface {
	M()
}

type T struct {
	S string
}

// This method means type T implements the interface I,
// but we don't need to explicitly declare that it does so.
func (t T) M() {
	fmt.Println(t.S)
}

func main() {
	var i I = T{"hello"}
	i.M()
}

```

An empty interface may hold values of any type. (Every type implements at least zero methods.) are used by code that handles values of unknown type. For example, `fmt.Print` takes any number of arguments of type `interface{}`.

## Type assertions
A _type assertion_ provides access to an interface value's underlying concrete value.
```go
t := i.(T)
t, ok := i.(T)
switch v := i.(type) {
case T:
    // here v has type T
case S:
    // here v has type S
default:
    // no match; here v has the same type as i
}

```
This statement asserts that the interface value `i` holds the concrete type `T` and assigns the underlying `T` value to the variable `t`.

If `i` does not hold a `T`, the statement will trigger a panic.



```go
package main

import "fmt"
import "code.google.com/p/go-tour/tree"

// Walk walks the tree t sending all values
// from the tree to the channel ch.
func Walk(t *tree.Tree, ch chan int) {
    var walker func(t *tree.Tree)
    walker = func (t *tree.Tree) {
        if (t == nil) {
            return
        }
        walker(t.Left)
        ch <- t.Value
        walker(t.Right)
    }
    walker(t)
    close(ch)
}

// Same determines whether the trees
// t1 and t2 contain the same values.
func Same(t1, t2 *tree.Tree) bool {
    ch1, ch2 := make(chan int), make(chan int)

    go Walk(t1, ch1)
    go Walk(t2, ch2)

    for {
        v1,ok1 := <- ch1
        v2,ok2 := <- ch2

        if v1 != v2 || ok1 != ok2 {
            return false
        }

        if !ok1 {
            break
        }
    }

    return true
}

func main() {
    fmt.Println("1 and 1 same: ", Same(tree.New(1), tree.New(1)))
    fmt.Println("1 and 2 same: ", Same(tree.New(1), tree.New(2)))

}
```

We can also use `defer` to ensure the mutex will be unlocked as in the `Value`method.
```go
package main

import (
	"fmt"
	"sync"
	"time"
)

// SafeCounter is safe to use concurrently.
type SafeCounter struct {
	mu sync.Mutex
	v  map[string]int
}

// Inc increments the counter for the given key.
func (c *SafeCounter) Inc(key string) {
	c.mu.Lock()
	// Lock so only one goroutine at a time can access the map c.v.
	c.v[key]++
	c.mu.Unlock()
}

// Value returns the current value of the counter for the given key.
func (c *SafeCounter) Value(key string) int {
	c.mu.Lock()
	// Lock so only one goroutine at a time can access the map c.v.
	defer c.mu.Unlock()
	return c.v[key]
}

func main() {
	c := SafeCounter{v: make(map[string]int)}
	for i := 0; i < 1000; i++ {
		go c.Inc("somekey")
	}

	time.Sleep(time.Second)
	fmt.Println(c.Value("somekey"))
}

```

### Substitute variables into strings

It's trivial with `fmt`.

~~~~
package main

import "fmt"

func main() {
  x, y := "foo", "bar"
  s := fmt.Sprintf("X is %v and Y is %v", x, y) // Outputs "X is foo and Y is bar"
}
~~~~

How about leading zeroes?

~~~~
package main

import "fmt"

func main() {
  ss := fmt.Sprintf("%03d", 23) // Outputs 023
}
~~~~


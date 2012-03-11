### Generate random numbers

Most of the time `math/rand`[link][rand] is what you want.

~~~~
package main

import (
  "fmt"
  "math/rand"
  "time"
)

package main() {
  src := rand.NewSource(time.Now().Unix())
  r := rand.New(src)
  fmt.Println(r.Int() % 10)
}
~~~~

[rand]: http://weekly.golang.org/pkg/math/rand/
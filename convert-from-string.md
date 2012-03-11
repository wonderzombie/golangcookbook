### Converting to and from strings

Two ways are `strconv`([doc][strconv]) and `fmt`([doc][fmt]).

`strconv` has a number of methods for parsing ints. The most straightforward is `Atoi()` (and its cousin `Itoa()`).

~~~~
package main

import (
  "fmt"
  "strconv"
  "strings"
)

func main() {
  ss := "3 37 Dennis"
  s := strings.Fields(ss)
  id, err := strconv.Atoi(s[0])
  if err != nil {
    panic(err)
  }
  fmt.Println(id)
}
~~~~

This is fine for just one string, but if we wanted to convert multiple fields it's a bit burdensome.

`fmt` has a number of methods for just this scenario. `Sscan()` in particular will parse space-separated fields into a set of supplied variables. In this way, you can avoid having to parse the values in individual steps.

~~~~
import (
  "fmt"
)

func main() {
  var (
    id, age int
    name string
  )
  ss := "3 37 Dennis"
  if _, err := fmt.Sscan(ss, &id, &age, &name); err != nil {
    panic(err)
  }
  fmt.Println(id, age, name)
}
~~~~

`Sscanf()` grants you more control over how the values are intepreted via a format string.

A third way involves `text/scanner`. 



[fmt]: http://weekly.golang.org/pkg/fmt/
[strconv]: http://weekly.golang.org/pkg/strconv/
[scanner]: http://weekly.golang.org/pkg/text/scanner/
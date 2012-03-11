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

A third way involves `text/scanner`[link][scanner]. From the docs, the basic usage pattern looks like this:

~~~~
var s scanner.Scanner
s.Init(src)
tok := s.Scan()
for tok != scanner.EOF {
  // do something with tok
  tok = s.Scan()
}
~~~~

`tok` in the above case is a `rune` which will be one of a set of constants in `text/scanner` which indicates the type of the token. This one may be useful to you if you have little to no idea what order the tokens are in and thus cannot rely on `fmt.Sscanf` or `regexp.FindSubmatchString`.

Here's a dumb, toy example:

~~~~
package main

import (
  "fmt"
  "bytes"
  "text/scanner"
)

func main() {
  ss := `foo 123 "baz"`
  buf := bytes.NewBufferString(ss)
  var s scanner.Scanner
  s.Init(buf)
  tok := s.Scan()
  for tok != scanner.EOF {
    fmt.Println("=>", s.TokenText())
    switch tok {
    case scanner.Int:
        fmt.Println("int")
    case scanner.String:
        fmt.Println("string")
    case scanner.Ident:
        fmt.Println("ident")
    default:
        fmt.Println("i dunno")
    }
    // do something with tok
    tok = s.Scan()
  }
}
~~~~

In combination with `strconv`, you can now take an arbitrary sequence of tokens, infer their type equivalent, and choose the appropriate `strconv` method.

[fmt]: http://weekly.golang.org/pkg/fmt/
[strconv]: http://weekly.golang.org/pkg/strconv/
[scanner]: http://weekly.golang.org/pkg/text/scanner/
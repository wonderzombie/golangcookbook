### Show non-printing characters

Use `%q` for your format string.

~~~~
package main

import "fmt"

func main() {
  var s = "\x01foo\x01 bar"
  fmt.Println(s)        // Prints "foo bar" (minus quotes).
  fmt.Printf("%q\n", s) // Prints "\x01foo\x01 bar" (including quotes).
}
~~~~
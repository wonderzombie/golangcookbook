### Test for the presence of a key/value in a map

When performing a lookup in a map, you'll never get `nil` back. Instead, you'll always get the zero-initialized instance of whatever the map's value type is. For some use cases such as a `string` value it might not matter. For an arbitrary struct, though, it may be tedious or impractical to check every public field for its zero value.

You can find out for sure whether the entry was there by assigning to a second variable as part of the lookup. The variable will be populated with a `bool` indicating whether or not there was an entry for that key.

~~~~
type Translation struct {
  Spanish string
  Mandarin string
}

colors := map[string]Translation {
  "green": {"verde", "lù"},
  "red": {"rojo", "hóng"},
  "blue": {"azul", "lán"}
}

c, ok := colors["black"]
~~~~

In this example, `ok` will be false. If you're only testing for the presence of the value and thus don't care about the value itself, you can use `_` instead:

~~~~
_, ok := colors["black"]
~~~~

The [docs](http://weekly.golang.org/doc/effective_go.html#maps) also mention using a map as a set.

~~~~
package main

import "fmt"

type Set map[string]bool

func (ss Set) Put(k string) bool {
  _, ok := ss[k]
  if !ok {
    ss[k] = true
    return true
  }
  return false
}


func main() {
  names := make(Set, 0)
  rawNames := []string {
    "Alice",
    "Bob",
    "Alice",
    "Claire",
    "Bob",
  }

  for _, n := range rawNames {
    if ret := names.Put(n); !ret {
      fmt.Println("Ignoring duplicate name:", n)
    }
  }

  fmt.Println(names)
}
~~~~
[ego]: http://golang.org/doc/effective_go.html
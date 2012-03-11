### Test a map for the presence of an item

When performing a lookup, you'll never get `nil` or nothing back; you'll always get some zero-initialized instance of whatever the map's value type is. If it's a string, you'll get `""` instead of `nil`, for instance.

When you do the look up, though, you can use a second return value which will indicate whether or not a value for the given key was present.

~~~~
val, ok := mymap[key]
if !ok {
  // handle the case where key was not present
}
~~~~

If you don't care about the value, you can use `_` instead and just check the second return value.

The [docs](http://weekly.golang.org/doc/effective_go.html#maps) talk about all this. Among other things, they mention using a `map[sometype]bool` as a set. Here's an example:

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
    names.Put(n)
  }
  
  fmt.Println(names)  
}
~~~~
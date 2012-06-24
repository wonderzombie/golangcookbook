### Iterate over an array

This is simple:

~~~~
var ss = []string{
  "foo",
  "bar",
  "baz", // note required trailing comma
}

for i, s := range ss {
  fmt.Println("Index", i, "Value", s)
}
~~~~

If you don't want either the index or the value, use `_` in lieu of it.

There is a potential gotcha with modifying the contents of the array.

<http://play.golang.org/p/rqbXldcnaw>

~~~~
type Record struct {
  Id    int
  Name  string
}

var records := []*Record{
  &{6, "Bob"},
  &{7, "Alice"},
  &{8, "Charlie"},
}

// r is a temporary variable, so...
for _, r := range records {
  if r.Id == 8 {
    r.Name = "Charles" // ...this will do nothing.
  }
}
~~~~

You can get around this in one of two ways. One is simply to use the index to read or assign as you might if you were writing the `for` loop manually.

Another possibly cleaner approach is to take the address of the item at the current index:

~~~~
for i := range records {
  r := &records[i] // r is now a *Record, pointing to the item at index i.
  if r.Id == 8 {
    r.Name = "Charles"
  }
}
~~~~

This pattern occurs regularly in the Go standard libraries.
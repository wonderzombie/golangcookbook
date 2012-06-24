### Printing a struct

You can use `%v` for printing a struct. For simple structs, this may be sufficient, but not necessarily.

~~~~
package main

import "fmt"

type Record struct {
  Id    int
  FirstName string
  MiddleName  string
  LastName  string
}

var records = []Record{
  {7, "Charlie", "", "Chaplin"},
  {8, "Cher", "", ""},
}

func main() {
  for _, r := range records {
    fmt.Printf("%v\n", r)
  }
}
~~~~

This prints `{7 Charlie  Chaplin}` for the first record. Worse, the second is `{8 Cher  }`. Imagine if your struct had multiple numeric fields, there were newlines in a field, or a series of empty fields.

Try `%+v` or `%#v` instead:

~~~~
for _, r := range records {
  fmt.Println(r)
  fmt.Printf("%+v", r)
  fmt.Printf("%#v", r)
}
~~~~

Output:

~~~~
{7 Charlie  Chaplin}
{Id:7 FirstName:Charlie MiddleName: LastName:Chaplin}
main.Record{Id:7, FirstName:"Charlie", MiddleName:"", LastName:"Chaplin"}
{8 Cher  }
{Id:8 FirstName:Cher MiddleName: LastName:}
main.Record{Id:8, FirstName:"Cher", MiddleName:"", LastName:""}
~~~~
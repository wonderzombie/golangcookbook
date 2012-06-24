### Parse JSON

<http://play.golang.org/p/c-uDBX0y8t>

`encoding/json` is what you want, as discussed in [JSON and Go][goblog].

Relatively simple example:

~~~~
package main

import "fmt"
import "encoding/json"

var myJson = `{'foo': 0, 'bar': {'baz': 1}}`

type JsonResp struct {
  Foo int
  Bar struct {
    Baz int
  }
}

func main() {
  fmt.Println("Hello, playground")
  var j JsonResp
  json.Unmarshal([]byte(myJson), &j)
  fmt.Printf("%#v\n", j)
  fmt.Println(j.Bar.Baz)
}
~~~~

[goblog]: http://blog.golang.org/2011/01/json-and-go.html
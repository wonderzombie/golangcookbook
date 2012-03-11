### Formatting strings

<http://play.golang.org/p/z32mCk38QF>

The `fmt` package is one avenue. 

~~~
package main

import (
  "bytes"
  "fmt"
)

type Data struct {
  Name string
  Age int
}

func main() {
  d := Data{Name: "Dennis", Age: 37}
  
  // Simple, w/o any formatting verbs
  fmt.Println("Name is", d.Name, "and age is", d.Age)
  
  // %v is idiomatic. See also %q and %d.
  fmt.Printf("Name is %v, age is %v\n", d.Name, d.Age)

  // Write to a buffer like a file.
  var buf bytes.Buffer
  fmt.Fprintf(&buf, "%v is %v", d.Name, d.Age)
  fmt.Println("Buffer contains:", buf.String())
}
~~~

Another avenue is the `template` package.

<http://play.golang.org/p/RQcXWr0gpC>

~~~
package main

import (
  "fmt"
  "os"
  "text/template"
)

type Data struct {
  Name string
  Age int
}

func main() {
  d := Data{"Dennis", 37}
  tmpl, _ := template.New("data").Parse("{{.Name}} is {{.Age}}\n")
  // ...or bytes.Buffer, or whatever else.
  tmpl.Execute(os.Stdout, d)
  
  
  // Multiple rows of data.
  dd := []Data {
     {"Georgia", 34},
     {"Jorge", 13},
     {"Summer", 21},
     {"George", 59},
     {"Balthazar", 40},
  }
  // Default output isn't that pretty.
  fmt.Println(dd)
  
  // Here is some nicer output.
  tmplStr := `{{range $i, $d := .}}{{printf "Row #%v: %v is age %v\n" $i $d.Name $d.Age}}{{end}}`
  tmpl = template.Must(template.New("report").Parse(tmplStr))
  tmpl.Execute(os.Stdout, dd)
}
~~~

### Parsing structured data in a text file

You have many potential choices. I'll discuss two. 

We'll use a file that looks like this as the data source:

~~~~
0 37 Dennis
1 73 Diana
2 40 Jorge
3 18 Georgia
4 13 Reggie
~~~~

Here's a snippet which uses `strings`

~~~~
package main

import (
  "bytes"
  "flag"
  "io/ioutil"
  "strings"
)

var (
  filename = flag.String("file", "", "File to use as input.")
)

func main() {
  data := ioutil.ReadFile("foo.txt")
  buf := bytes.NewBuffer(data)

  var (
    line []bytes
    table map[int]string
  )

  var err error
  for line, err := buf.ReadBytes('\n') {
    s := strings.Split(" ")
    if len(m) != 0 {
      id, label := m[0], m[1]
      map[id] = label
    }
  }
}
~~~~
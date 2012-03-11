### Receive command line flags

You'll want the `flag` package. Here's some basic usage:

~~~~
package main

import (
  "flag"
  "os"
)

func main() {
  var (
    filename = flag.String("filename", "default.cfg", "Default configuration file to use.")
    verbose = flag.Bool("v", false, "Whether to use verbose output.")
  )
  flag.Parse()

  if (*verbose) {
    // do something
  }
  
  f, err := os.Open(*filename)
  // Do something with the file.
}
~~~~

For more, check the documentation for the [flag][flag] package.

[flag]: http://weekly.golang.org/pkg/flag/
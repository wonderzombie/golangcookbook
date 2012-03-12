### Test whether a regular expression matches a string

The `regexp` package offers the usual suite of regular expression functionality.

If you just want to check a string with a one-off regexp:

~~~~
s := "foo bar baz"
m, err := regexp.MatchString("\w+", s)
if err != nil {
  panic(err)
}
// do something with m
~~~~


### Capture text with a regular expression

Capturing the contents of the regexp requires initializing a `Regexp` struct:

~~~~
s := "foo bar baz quux"
re := regexp.MustCompile("\w+\s\w+")
matches := re.FindStringSubmatch(s) 
if len(matches) == 0 {
  // deal with error case
}
for _, m := range (matches[1:]) {
  // do something with each match
}
~~~~

If you want to use named captures:

~~~~
re := regexp.MustCompile("(?P<id>\\d+),(?P<name>\\w+)")

tests := []string {
  "123,foo",
  "456,bar",
}

for _, t := range tests {
  mm := re.FindStringSubmatch(t)
  if len(mm) == 0 {
    fmt.Println("Failed to match regex:", t)
    continue
  }
  // The first index of a Find*Submatch method will always be the whole string matched. Similarly,
  // the first index of names is always the empty string. Trim both of them.
  mm = mm[1:] 
  names := re.SubexpNames()[1:] 
  
  fmt.Println("For string:", t)
  for i, m := range mm {
    n := names[i]
    fmt.Printf("%v: %v\n", n, m)
  }
  
}
~~~~
<http://play.golang.org/p/giPM4-30ym>

There's a lot more you can do, however. 

As the [docs][regexp] puts it:

    There are 16 methods of Regexp that match a regular expression and identify the matched text. Their names are matched by this regular expression:

         Find(All)?(String)?(Submatch)?(Index)?


`All` is equivalent to `/foo/g`, in that it finds all instances of an expression instead of just the first. `String` specifies that we're speaking `string` instead of `[]byte`. 

`Submatch` is most immediately useful for capturing text.

 [regexp]: http://weekly.golang.org/pkg/regexp/
### Search a slice

If your slice is `[]string`, `[]int`, or `[]float64`, `sort` has what you want. You will need to sort them first, but there are methods for that, too.

~~~~
s := []string {
  "foo",
  "bar",
  "baz",
}

sort.StringSlice(s).Sort() // convert & sort
x := sort.SearchStrings(s, "foo")
fmt.Printf("Found %v at %v", s[x], x)
~~~~

If the data type you want to sort is not among those, you'll need to implement [sort.Interface][sortif] or sort it yourself. 

Once it is sorted, you can use `sort.Search()`. You supply a higher-order function which takes an `int` representing the index of a candidate, and returns a `bool` indicating whether the candidate is the one you're looking for. It's a binary search so the slice has to be sorted.

~~~~
ss := []string{
  "Alice",
  "Bob",
  "Claire",
  // ...
  "Yaron",
  "Zelda",
}

name := "Yaron"
n := sort.Search(len(ss), func(i int) { return ss[i] == name })
~~~~

There's more to it if the item isn't found; `n` in the above case will point to where the string `"Yaron"` ought to have been if it were in the list. As always, the Go docs are very comprehensive and worth reading in more depth.

[sortif]: http://weekly.golang.org/pkg/sort/#Interface
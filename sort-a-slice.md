### Sort a slice

There's a `sort` package for this, but it will take some work for arbitrary data types. The example in the docs is very good; there's really no need to recapitulate it here. However, I can explain.

Go doesn't have generics. Instead, you'll need to implement [sort.Interface][sortif]. That consists of a few methods: `Len()`, `Swap()`, and `Less()`. For slices, the first two are trivial.

`Less()` is the comparison operator; it gives you two indices and you return a `bool`.

To implement sorting by multiple criteria for one list type involves a bit of sleight of hand.

~~~~
type Record {
  Name string
  Age int
}

// ... implementations of Swap() and Len() elided

type RecordsByName struct{Record}
~~~~

That last part is the magical part. You then define a `Less()` method on `RecordsByName` which compares `rr.Record[i]` with `rr.Record[j]`.

There are some pre-configured types available: `int`, `float64`, and `string`.

As a bonus, there is support for a higher-order `Search` function, a la Ruby.


[sortif]: http://weekly.golang.org/pkg/sort/#Interface
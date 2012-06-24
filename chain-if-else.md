### Chain if/else

You can of course do this:

~~~~
if (x == y) {

} else if (z == x) {

} else if (z == y) {

}
~~~~

However, you can also use a case statement without a parameter:

~~~~
switch {
  case x == y:
  // ...
  case z == x:
  // ...
  case z == y:
  // ...
}
~~~~
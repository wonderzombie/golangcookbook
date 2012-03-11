### Fetch a URL

The `net/http` package is the way. 

The most direct way:

~~~~
resp, err := http.Get("http://example.com/")
if err != nil {
  // handle error
}
defer resp.Body.Close()
body, err := ioutil.ReadAll(resp.Body)
~~~~


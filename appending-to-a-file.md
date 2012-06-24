### Appending to a file -- WIP

This will create a new file if it doesn't exist, open it with R/W permissions, and append to it:

~~~~
f, err := os.OpenFile("file.txt", os.O_CREATE|os.O_RDWR|os.O_APPEND, 0666)
if err != nil {
  log.Fatal(err)
}
defer f.Close()

f.WriteString("Hello world")
~~~~

If you did not have `os.O_APPEND`, then you would overwrite anything in the file. Likewise if you didn't have O_CREATE then if the file did not exist, `err` would be non-nil.
### Execute a command -- WIP

You can easily execute an external command and collect its output to stdout using `os/exec`.

~~~~
cmdLine := strings.Fields("ls -l /var/log")
out, err := exec.Command(...cmdLine).Output()
if err != nil {
  log.Fatal(err)
}
fmt.Printf("Contents of /var/log: %s", out)
~~~~

You may also wish to look at [Cmd.StdoutPipe][http://golang.org/pkg/os/exec/#Cmd.StdoutPipe] and its `Stderr` and `Stdin` siblings should you need something more sophisticated.
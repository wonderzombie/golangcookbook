~~~
package main

import "fmt"

func main() {
	fmt.Println("Hello, playground")
	s := "The 12 Monkeys"
	var (
		num int
		title string
	)
	_, err := fmt.Sscanf(s, "The %v %v", &num, &title)
	if err != nil {
		fmt.Println(err)
	} else {
		fmt.Println(num)
		fmt.Println(title)
	}
	
	f := ":trahari!~trahari@host PRIVMSG #bucket :Foo"
	ff := ":%v %v %v :%v"
	var prefix, cmd, channel, txt string
	if _, err = fmt.Sscanf(f, ff, &prefix, &cmd, &channel, &txt); err != nil {
		fmt.Println(err)
	}
	
	fmt.Println(prefix, cmd, channel, txt)
	
	var nick, user, host string
	_, err = fmt.Sscanf(prefix, "%v!~%v@%v", &nick, &user, &host)
	if err != nil {
		fmt.Println(err)
	}
	
	data := `foo
	bar
	baz`
	
	var line string
	fmt.Scanln(data, &line)
	fmt.Println(line)
	
}
~~~
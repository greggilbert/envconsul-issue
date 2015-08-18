# envconsul issue


## To run:

1. `vagrant up`
2. `vagrant ssh`
3. `consul agent -server -bootstrap-expect 1 -data-dir /tmp/consul &`
4. `curl -X PUT -d 'test' http://localhost:8500/v1/kv/web/key1`
5. `envconsul -consul=127.0.0.1:8500 -prefix web`

## Error

```bash
panic: runtime error: slice bounds out of range

goroutine 6 [running]:
main.(*Runner).Run(0xc20807c000, 0xc208090d78, 0x0, 0x0)
	/home/vagrant/envconsul/runner.go:272 +0x1464
main.(*Runner).Start(0xc20807c000)
	/home/vagrant/envconsul/runner.go:159 +0x41f
created by main.(*CLI).Run
	/home/vagrant/envconsul/cli.go:107 +0x70b

goroutine 1 [select]:
main.(*CLI).Run(0xc20800a300, 0xc20800a000, 0x4, 0x4, 0x7f3c935489a8)
	/home/vagrant/envconsul/cli.go:114 +0xdf2
main.main()
	/home/vagrant/envconsul/main.go:12 +0x107

goroutine 5 [syscall]:
os/signal.loop()
	/usr/lib/go/src/os/signal/signal_unix.go:21 +0x1f
created by os/signal.init·1
	/usr/lib/go/src/os/signal/signal_unix.go:27 +0x35

goroutine 7 [select]:
github.com/hashicorp/consul-template/watch.(*View).poll(0xc20800ae40, 0xc20805c300, 0xc20805c360)
	/home/vagrant/go/src/github.com/hashicorp/consul-template/watch/view.go:67 +0x90b
created by github.com/hashicorp/consul-template/watch.(*Watcher).Add
	/home/vagrant/go/src/github.com/hashicorp/consul-template/watch/watcher.go:103 +0x557

goroutine 13 [runnable]:
github.com/hashicorp/consul-template/watch.(*View).fetch(0xc20800ae40, 0xc20805c720, 0xc20805c960)
	/home/vagrant/go/src/github.com/hashicorp/consul-template/watch/view.go:112
created by github.com/hashicorp/consul-template/watch.(*View).poll
	/home/vagrant/go/src/github.com/hashicorp/consul-template/watch/view.go:65 +0xc6

goroutine 11 [IO wait]:
net.(*pollDesc).Wait(0xc208010d10, 0x72, 0x0, 0x0)
	/usr/lib/go/src/net/fd_poll_runtime.go:84 +0x47
net.(*pollDesc).WaitRead(0xc208010d10, 0x0, 0x0)
	/usr/lib/go/src/net/fd_poll_runtime.go:89 +0x43
net.(*netFD).Read(0xc208010cb0, 0xc20800f000, 0x1000, 0x1000, 0x0, 0x7f3c9354cbf0, 0xc20802ab70)
	/usr/lib/go/src/net/fd_unix.go:242 +0x40f
net.(*conn).Read(0xc20802c1e0, 0xc20800f000, 0x1000, 0x1000, 0x0, 0x0, 0x0)
	/usr/lib/go/src/net/net.go:121 +0xdc
net/http.noteEOFReader.Read(0x7f3c9354e478, 0xc20802c1e0, 0xc208068318, 0xc20800f000, 0x1000, 0x1000, 0x6f9f80, 0x0, 0x0)
	/usr/lib/go/src/net/http/transport.go:1270 +0x6e
net/http.(*noteEOFReader).Read(0xc20801f380, 0xc20800f000, 0x1000, 0x1000, 0xc208012000, 0x0, 0x0)
	<autogenerated>:125 +0xd4
bufio.(*Reader).fill(0xc20805c9c0)
	/usr/lib/go/src/bufio/bufio.go:97 +0x1ce
bufio.(*Reader).Peek(0xc20805c9c0, 0x1, 0x0, 0x0, 0x0, 0x0, 0x0)
	/usr/lib/go/src/bufio/bufio.go:132 +0xf0
net/http.(*persistConn).readLoop(0xc2080682c0)
	/usr/lib/go/src/net/http/transport.go:842 +0xa4
created by net/http.(*Transport).dialConn
	/usr/lib/go/src/net/http/transport.go:660 +0xc9f

goroutine 12 [select]:
net/http.(*persistConn).writeLoop(0xc2080682c0)
	/usr/lib/go/src/net/http/transport.go:945 +0x41d
created by net/http.(*Transport).dialConn
	/usr/lib/go/src/net/http/transport.go:661 +0xcbc
```

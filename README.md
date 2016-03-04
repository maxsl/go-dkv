# go-dkv
Golang simple KV Database use system's file system

Features:
- Support create a database in a samba directory
- Support Multi-process, Multi-thread

`go get github.com/zeropool/go-dkv`

```go
package main

import (
	"fmt"

	"github.com/zeropool/go-dkv"
)

type T struct {
	A int
	B string
}

func main() {
	// create a database under folder test
	db, err := dkv.Open("test", false)
	if err != nil {
		panic(db)
	}
	// can store any variable that can marshal with json
	db.Set("Hello", "World")
	db.Set("PI", 3.1415926)
	db.Set("test", &T{1, "OK"})
	fmt.Println("Hello:", db.Get("Hello"))
	fmt.Println("dummy will nil:", db.Get("dummy"))

	db.Interate(func(k string, v interface{}) {
		fmt.Println(k, v)
	})

	db.Del("Hello")
	// empty the database, will remove database directory
	db.Cls()
	db.Close()
}
```

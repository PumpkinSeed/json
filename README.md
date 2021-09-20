# json

Copy of Golang's json library with IsZero feature from [CL13977](https://go-review.googlesource.com/c/go/+/13977/)

## Disclaimer

It is a package primary used for my own projects, I will keep it up-to-date with the mainline versioning of Go.

## Usage

Exactly the same as Go's [JSON](https://pkg.go.dev/encoding/json). Plus...

```go
package main

import (
	"encoding/json"
	"fmt"
)

type nullString struct {
	Valid  bool
	String string
}

func (n nullString) IsZero() bool {
	return !n.Valid
}

type RandomDataSet struct {
	Data1 nullString `json:"data1,omitempty"`
	Data2 nullString `json:"data2,omitempty"`
}

func main() {
	result, err := json.Marshal(RandomDataSet{Data1: nullString{Valid: true, String: "test"}})
	if err != nil {
		panic(err)
	}
	fmt.Println(string(result))
}

// Output: {"data1":{"Valid":true,"String":"test"}}
```
[//title]: (case-insensitive-string-compare-in-go)
[//englishtitle]: (case-insensitive-string-compare-in-go)
[//category]: (go,snippet)
[//tags]: (go,snippet)
[//createtime]: (20210429)
[//updatetime]: (20210429)

```go
package main

import (
    "fmt"
    "strings"
)

func main() {
    res := strings.EqualFold("abc", "AbC")
    fmt.Println(res)

    res = strings.EqualFold("abc", "AbCd")
    fmt.Println(res)
}
// output：
// true
// false
```

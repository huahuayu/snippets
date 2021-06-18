[//title]: (go-write-string-to-file)
[//englishtitle]: (go-write-string-to-file)
[//category]: (go,snippet)
[//tags]: (go,snippet)
[//createtime]: (20210526)
[//updatetime]: (20210526)

```go
package file

import (
	"os"
	"path/filepath"
)

func WriteToFile(file string, str string) error{
	dir := filepath.Dir(file)
	if _, err := os.Stat(dir);os.IsNotExist(err) {
		os.MkdirAll(dir, 0755)
	}
	f, err := os.OpenFile(file, os.O_CREATE|os.O_APPEND|os.O_WRONLY, 0600)
	if err != nil {
		return err
	}
	defer f.Close()
	if _, err = f.WriteString(str + "\n"); err != nil {
		return err
	}
	return f.Sync()
}
```

## context

- write string to file by append
- if file not exists, create it (create dir first then create file by openFile option `os.O_CREATE`)
- close file by defer
- commit file change by `f.Sync()`

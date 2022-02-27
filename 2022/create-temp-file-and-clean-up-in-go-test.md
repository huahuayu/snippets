[//title]: (create-temp-file-and-clean-up-in-go-test)
[//englishtitle]: (create-temp-file-and-clean-up-in-go-test)
[//category]: (go,snippet)
[//tags]: (go,snippet)
[//createtime]: (20220224)
[//updatetime]: (20220224)

```go
import (
	"fmt"
	"io/ioutil"
	"os"
	"testing"
)

func tempdir(patten string) string{
	dir, _ := ioutil.TempDir("/tmp", patten)
	fmt.Println(dir + ": created")
	return dir
}

func TestTempDir(t *testing.T) {
	dir := tempdir("dir-prefix*suffix")
	cleanUp := func() { os.RemoveAll(dir)}
	// test logic...
	cleanUp()
	fmt.Println(dir + ": deleted")
}
```

output:

```text
=== RUN   TestTempDir
/tmp/dir-prefix400328188suffix: created
/tmp/dir-prefix400328188suffix: deleted
```

## note

`ioutil.TempDir`

- create temp file with patten, the first param can be space, if not specified, it will use `os.TempDir()` to put the temp dir
- the second param use '\*' to split prefix and suffix

`os.RemoveAll`

- removes path and any children it contains.

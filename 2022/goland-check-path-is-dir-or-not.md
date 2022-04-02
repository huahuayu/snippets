[//title]: (goland-check-path-is-dir-or-not)
[//englishtitle]: (goland-check-path-is-dir-or-not)
[//category]: (golang,snippet)
[//tags]: (golang,snippet)
[//createtime]: (20220402)
[//updatetime]: (20220402)

```go
func(dir string) bool {
    info, err := os.Stat(dir)
    if err != nil || !info.IsDir() {
        return false
    }
    return true
}
```

[//title]: (bash-search-content-within-file)
[//englishtitle]: (bash-search-content-within-file)
[//category]: (bash,linux,snippet)
[//tags]: (bash,find,xargs,linux,snippet)
[//createtime]: (20220330)
[//updatetime]: (20220331)

在当前目录递归搜索名字为 `go.mod` 的文件，看是否包含 `ttl` 关键字。

```bash
find . -name go.mod | xargs grep -n 'ttl'
```

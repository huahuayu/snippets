[//title]: (golang-join-filename-and-dir)
[//englishtitle]: (golang-join-filename-and-dir)
[//category]: (go,snippet)
[//tags]: (go,snippet,path)
[//createtime]: (20220402)
[//updatetime]: (20220402)

To concat dir and fileName as a path, use code below

```go
path := filepath.Join(dir, fileName)
```

or

```go
path := dir + os.PathSeparator + fileName
```

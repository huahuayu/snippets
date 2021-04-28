[//title]: (go生成随机bytes)
[//englishtitle]: (generate-random-bytes-in-go)
[//category]: (go,snippet)
[//tags]: (go,snippet)
[//createtime]: (20210428)
[//updatetime]: (20210428)

```go
func GenRandomBytes(size int) (randomBytes []byte) {
	rand.Seed(time.Now().UnixNano())
	randomBytes = make([]byte, size)
	rand.Read(randomBytes)
	return randomBytes
}
```

## Context

Pay attention to this line, otherwise everytime `randomBytes` is the same.

```go
rand.Seed(time.Now().UnixNano())
```

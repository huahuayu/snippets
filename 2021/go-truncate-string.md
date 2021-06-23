[//title]: (go-truncate-string)
[//englishtitle]: (go-truncate-string)
[//category]: (go,snippet)
[//tags]: (go,string,truncate,snippet)
[//createtime]: (20210623)
[//updatetime]: (20210623)

```go
func truncate(str string, length int) (truncated string) {
	if length <= 0 {
		return
	}
	if len(str) < length{
		return str
	}
	for i, char := range str {
		if i >= length {
			break
		}
		truncated += string(char)
	}
	return
}
```

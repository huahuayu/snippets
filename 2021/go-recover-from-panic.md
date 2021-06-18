[//title]: (go-recover-from-panic)
[//englishtitle]: (go-recover-from-panic)
[//category]: (go,snippet)
[//tags]: (go,recover,panic,snippet)
[//createtime]: (20210618)
[//updatetime]: (20210618)

```go
			go func(txHash common.Hash) {
				defer func() {
					if r := recover(); r != nil {
						logrus.Error("recovered from panic: ", r)
						logrus.Debug(string(debug.Stack()))
					}
				}())
```

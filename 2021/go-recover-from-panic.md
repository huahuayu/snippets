[//title]: (go-recover-from-panic)
[//englishtitle]: (go-recover-from-panic)
[//category]: (go,snippet)
[//tags]: (go,recover,panic,snippet)
[//createtime]: (20210618)
[//updatetime]: (20210618)

```go
defer func() {
	if r := recover(); r != nil {
		logrus.Error("recovered from panic: ", r)
  		// 0-PanicLevel 1-FatalLevel 2-ErrorLevel 3-WarnLevel 4-InfoLevel 5-DebugLevel 6-TraceLevel
		if logrus.GetLevel().String() == "5"{
			fmt.Println("debug trace:\n" + string(debug.Stack()))
		}
	}
}()
```

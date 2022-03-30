[//title]: (go-sync-once-by-example)
[//englishtitle]: (go-sync-once-by-example)
[//category]: (go,concurrent-programming,snippet)
[//tags]: (go,snippet,concurrent-programming)
[//createtime]: (20220329)
[//updatetime]: (20220330)

`sync.Once` ensure the anonymous function execute only once, and before execution finished, it will block all the other goroutines.

`sync.Once` is singleton pattern, it can be used to initialize config / singleton instance.

```go
func TestSyncOnce(t *testing.T) {
	var once sync.Once
	for i:=0;i<=5;i++{
		go func(i int) {
			once.Do(func() {
				fmt.Println("inside once: ", i)
				time.Sleep(5 * time.Second)
			})
			fmt.Println(i)
		}(i)
	}
	time.Sleep(6 * time.Second)
}
```

result

```text
inside once:  5
<sleep 5 seconds>
5
0
1
2
3
4
```

## real world example

```go
var (
	signer      types.Signer
	onlyOnce    sync.Once
)

func getSender(tx *types.Transaction) (common.Address, error) {
	onlyOnce.Do(func() {
		signer = types.LatestSignerForChainID(tx.ChainId())
	})
	return signer.Sender(tx)
}
```

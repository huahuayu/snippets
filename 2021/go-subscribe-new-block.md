[//title]: (go-subscribe-new-block)
[//englishtitle]: (go-subscribe-new-block)
[//category]: (go,ethereum,snippet)
[//tags]: (go,ethereum,snippet)
[//createtime]: (20210622)
[//updatetime]: (20210622)

```go
func TestSubscribeNewBlock(t *testing.T) {
	client, err := ethclient.DialContext(context.Background(), "ws://10.136.0.32:9546")
	if err != nil {
		t.Fatal(err)
	}
	ch := make(chan *types.Header)
	sub, err := client.SubscribeNewHead(context.Background(), ch)
	if err != nil {
		t.Fatal(err)
	}
	for {
		select {
		case header := <-ch:
			t.Log(header.Number)
		case err = <-sub.Err():
			if err != nil {
				t.Error(err.Error())
			}
			return
		}
	}
}
```

## reference

https://goethereumbook.org/block-subscribe/

https://github.com/ethereum/go-ethereum/blob/master/rpc/client_example_test.go

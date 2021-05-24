[//title]: (go-subscribe-newPendingTransactions)
[//englishtitle]: (go-subscribe-newPendingTransactions)
[//category]: (go,ethereum,snippet)
[//tags]: (go,ethereum,snippet)
[//createtime]: (20210525)
[//updatetime]: (20210525)

```go
func TestSubscribeNewPendingTransactions(t *testing.T) {
	rpcClient, _ := rpc.Dial("ws://127.0.0.1:9546")
	ethClient, err := ethclient.DialContext(context.Background(), "ws://127.0.0.1:9546")
	ch := make(chan common.Hash, 2000)
	sub, err := rpcClient.EthSubscribe(context.Background(), ch, "newPendingTransactions")
	if err != nil {
		panic(err)
	}
	for {
		select {
		case txHash := <-ch:
			go func(txHash common.Hash) {
				defer func() {
					if r := recover(); r != nil {
						t.Error("recovered from panic", r)
					}
				}()
				t0 := time.Now()
				tx, isPending, err := ethClient.TransactionByHash(context.Background(), txHash)
				t.Log("TransactionByHash: ", time.Since(t0))
				if err != nil {
					t.Errorf("tx %s TransactionByHash error: %s\n", txHash.String(), err.Error())
					return
				}
				if !isPending {
					t1 := time.Now()
					receipt, err := ethClient.TransactionReceipt(context.Background(), txHash)
					t.Log("TransactionReceipt: ", time.Since(t1))
					if err != nil {
						t.Errorf("tx %s TransactionReceipt error: %s\n", txHash.String(), err.Error())
						return
					}
					if receipt.Status == types.ReceiptStatusFailed {
						t.Log("tx failed")
					} else if receipt.Status == types.ReceiptStatusSuccessful {
						t.Log("tx success")
					} else {
						t.Log("unknown tx status")
					}
					t.Log("blockNumber: ", receipt.BlockNumber)
				}
				from, err := types.Sender(types.NewEIP155Signer(tx.ChainId()), tx)
				if err != nil {
					t.Error("get from address: ", err)
					return
				}
				_ = from
				//t.Log("txHash: ",txHash.String())
				//t.Log("from: ",from.String())
				//t.Log("to: ",tx.To().String())
				//t.Log("data: ",hexutil.Encode(tx.Data()))
				//t.Log("isPending: ",isPending)
			}(txHash)
		case err := <-sub.Err():
			t.Error(err)
		}
	}
}
```

## context

Subscribe `newPendingTransactions` only gets txHash, if you want to get txData, another query is needed.

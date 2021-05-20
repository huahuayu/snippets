[//title]: (get-signed-tx-by-type.transactions)
[//englishtitle]: (get-signed-tx-by-type.transactions)
[//category]: (go,ethereum,snippet)
[//tags]: (go,ethereum,snippet)
[//createtime]: (20210520)
[//updatetime]: (20210520)

```go
func (t *Txn) SignedTxn() string {
	tx, _, err := eth.EthClient.TransactionByHash(context.Background(), common.HexToHash(t.Params.Result.TxHash))
	if err != nil {
		return ""
	}
	bs, err := tx.MarshalBinary()
	if err != nil {
		return ""
	}
	return hexutil.Encode(bs)
}
```

## context

After get signedRawTx, it can be use to send by rpc like `{"jsonrpc":"2.0","method":"eth_sendRawTransaction","params":["0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"],"id":1}`

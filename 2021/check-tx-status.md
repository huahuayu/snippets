[//title]: (check-ethereum-tx-status)
[//englishtitle]: (check-ethereum-tx-status)
[//category]: (go,ethereum,snippet)
[//tags]: (go,ethereum,snippet)
[//createtime]: (20210520)
[//updatetime]: (20210520)

```go
func (t *Txn) Status() (status string, blockNumber *big.Int, err error) {
	_, pending, err := eth.EthClient.TransactionByHash(context.Background(), common.HexToHash(t.Params.Result.TxHash))
	if err != nil {
		return Unknown, nil, err
	}
	if pending {
		return Pending, nil, nil
	}
	receipt, err := eth.EthClient.TransactionReceipt(context.Background(), common.HexToHash(t.Params.Result.TxHash))
	if err != nil {
		return Unknown, nil, err
	}
	if receipt.Status == types.ReceiptStatusFailed {
		return Failed, receipt.BlockNumber, nil
	}
	return Success, receipt.BlockNumber, nil
}
```

## context

Check ethereum tx status in go may need two queries, the first one `TransactionByHash()` check it's pending or not, the second `TransactionReceipt()` further check it's failed or success.

The status can be:

- `send`: tx send out
- `pending`: tx pending in mempool
- `success`: tx success
- `failed`: tx failed
- `cancel`: tx canceled by user (with same nonce)
- `drop`: tx dropped by miner because gas too low

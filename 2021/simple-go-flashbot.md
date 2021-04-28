[//title]: (simple-go-flashbot-request)
[//englishtitle]: (simple-go-flashbot-request)
[//category]: (go,flashbot,snippet)
[//tags]: (go,flashbot,snippet)
[//createtime]: (20210428)
[//updatetime]: (20210428)

```go
    request := ethRequest{
        ID:      1,
        JSONRPC: "2.0",
        Method:  "eth_sendBundle",
        Params:  []interface{}{encodedTxs, "latest", 0, 0},
    }

    body, err := json.Marshal(request)
    if err != nil {
        return err
    }
    req, err := http.NewRequest("POST", mevRelayServer, bytes.NewBuffer(body))
    if err != nil {
        log.Fatalf("%s", err)
    }

    req.Header.Set("Content-Type", "application/json")
    sig, err := crypto.Sign(crypto.Keccak256(body), pk)
    signature := addr.Hex() + ":" + hexutil.Encode(sig)
    req.Header.Set("X-Flashbots-Signature", signature)
```

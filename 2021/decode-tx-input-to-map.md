[//title]: (decode-tx-input-to-map)
[//englishtitle]: (decode-tx-input-to-map)
[//category]: (go,ethereum,snippet)
[//tags]: (go,ethereum,snippet)
[//createtime]: (20210520)
[//updatetime]: (20210520)

```go
func (t *Txn) decode() (fn string, decode map[string]interface{}, err error) {
	const ABI = "$ABI"
	// load contract ABI
	a, _ := abi.JSON(strings.NewReader(ABI))
	txInput := t.Params.Result.TxContents.Input
	// validate transaction, should be function call
	if len(txInput) < 10 {
		return "", nil, errors.New("not a valid transaction")
	}
	// decode txInput method signature
	decodedSig, err := hex.DecodeString(t.Params.Result.TxContents.Input[2:10])
	if err != nil {
		return "", nil, errors.New("decode txInput method signature error: " + err.Error())
	}
	method, err := a.MethodById(decodedSig)
	if err != nil {
		return "", nil, errors.New("recover method from abi error: " + err.Error())
	}
	// decode txInput Payload
	decodedData, err := hex.DecodeString(txInput[10:])
	if err != nil {
		return "", nil, errors.New("decode txInput Payload error: " + err.Error())
	}
	// unpack method inputs
	decode = make(map[string]interface{}, 0)
	err = method.Inputs.UnpackIntoMap(decode, decodedData)
	if err != nil {
		return "", nil, errors.New("unpack method inputs: " + err.Error())
	}
	return method.Name, decode, nil
}
```

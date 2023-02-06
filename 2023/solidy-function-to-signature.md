[//title]: (solidity-function-to-method-id)
[//englishtitle]: (solidity-function-to-method-id)
[//category]: (snippet,go,solidity)
[//tags]: (go,snippet,solidity,signature)
[//createtime]: (20230202)
[//updatetime]: (20230206)

Give any solidity function like `transfer(address to, uint256 value) returns(bool)` convert it to `0xa9059cbb` .

In golang:

```go
func fnToSig(fn string) (string, error) {
	f, err := toNormalized(fn)
	if err != nil {
		return "", err
	}
	hash := sha3.NewLegacyKeccak256()
	hash.Write([]byte(f))
	sig := "0x" + fmt.Sprintf("%x\n", hash.Sum(nil))[:8]
	return sig, nil
}

/*
transfer(address to, uint256 value) returns(bool)
transfer(address to, uint256 value)
transfer(address to, uint256 amt)
transfer(address to, uint value)
transfer(address , uint256)

should convert to:
transfer(address,uint256)

step1: truncate the char after the first ')'
step2: get the string inside the (), for example: str := "address to, uint256 value"
step3: split the string by ',' and trim the space in prefix & suffix, for example: params = ["address to", "uint256 value"]
step4: split the params by ' ' and delete all spaces, for example: param0 = ["address", "to"], param1 = ["uint256", "value"]
step5: replace uint to uint256, for example: ["address", "uint"] -> ["address", "uint256"]
step6: join the params by ',' and add '(', ')', for example: ["address", "uint256"] -> "(address,uint256)"
step7: return transfer(address,uint256)
*/
func toNormalized(fn string) (string, error) {
	fnName := fn[:strings.Index(fn, "(")]
	// step1: truncate the char after the first ')'
	fn = fn[:strings.Index(fn, ")")+1]
	// step2: get the string inside the ()
	originParams := fn[strings.Index(fn, "(")+1 : strings.Index(fn, ")")]
	// step3: split the string by ',' and trim the space in prefix & suffix
	paramSlice := strings.Split(originParams, ",")
	paramTypes := make([]string, 0)
	for i, param := range paramSlice {
		paramSlice[i] = strings.TrimSpace(param)
		// step4: split the originParams by ' ', get the variable type
		typ := strings.Split(paramSlice[i], " ")[0]
		// step5: replace uint to uint256
		if typ == "uint" {
			typ = "uint256"
		}
		paramTypes = append(paramTypes, typ)
	}
	// step6: rejoin the params by ','
	normalized := fmt.Sprintf("%s(%s)", fnName, strings.Join(paramTypes, ","))
	return normalized, nil
}
```

It's interesting that solidity can return it's selector by itself(refer https://etherscan.io/address/0xef1c6e67703c7bd7107eed8303fbe6ec2554bf6b#code Callbacks.sol).

```solidity
    function onERC1155BatchReceived(address, address, uint256[] calldata, uint256[] calldata, bytes calldata)
        external
        pure
        returns (bytes4)
    {
        return this.onERC1155BatchReceived.selector;
    }
```

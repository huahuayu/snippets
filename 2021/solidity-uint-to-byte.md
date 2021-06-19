[//title]: (solidity-uint-to-byte)
[//englishtitle]: (solidity-uint-to-byte)
[//category]: (solidity,ethereum,snippet)
[//tags]: (solidity,ethereum,snippet)
[//createtime]: (20210618)
[//updatetime]: (20210618)

```solidity
uint256 i = 10;
byte(uint8(i));
```

## context

uint256 can't convert to byte directly, but can convert to uint8 then convert to byte.

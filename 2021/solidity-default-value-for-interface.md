[//title]: (solidity-default-value-for-interface)
[//englishtitle]: (solidity-default-value-for-interface)
[//category]: (solidity,ethereum,snippet)
[//tags]: (solidity,snippet,default-value)
[//createtime]: (20210621)
[//updatetime]: (20210621)

```solidity
pragma solidity 0.6.6;

interface IERC20{
    function name() external view returns (string memory);
}

contract DefaultValue{
    IERC20 public a_erc20; // default value 0x0000000000000000000000000000000000000000
    mapping(address => IERC20) public erc20s; // default value for a non-exist key 0x0000000000000000000000000000000000000000
}
```

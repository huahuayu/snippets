[//title]: (solidity-default-value-for-interface-instance)
[//englishtitle]: (solidity-default-value-for-interface-instance)
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
    mapping(address => IERC20) public erc20s; // default value for a non-exist key address(nonexistKey) = address(0)

    function addErc20(address addr) public{
        erc20s[addr] = IERC20(addr);
    }

    function isExist(address addr) public view returns (bool){
        if (address(erc20s[addr]) == address(0)){
            return false;
        }
        return true;
    }
}
```

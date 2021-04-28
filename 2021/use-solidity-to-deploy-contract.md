[//title]: (使用solidity部署合约)
[//englishtitle]: (use-solidity-to-deploy-contract)
[//category]: (solidity,snippet)
[//tags]: (solidity,snippet)
[//createtime]: (20210428)
[//updatetime]: (20210428)

```soldity
contract Foo {
    constructor(address _owner) public {
        owner = _owner;
    }
    // other functions
}

contract Deploy {
    function deploy(bytes32 salt) external returns (address){
        return address(new TxnSender{salt : salt}($owner_address));
    }
}
```

## Context

salt must be byte32，if use remix to pass the salt, it is looks like `0x81ab92dd3a944ae29ec86e46c4e891b3ef3078f446cd88c56edd342542c3a8cc`

[//title]: (deploy-a-contract-with-leading-zeros)
[//englishtitle]: (deploy-a-contract-with-leading-zeros)
[//category]: (solidity,snippet)
[//tags]: (solidity,snippet)
[//createtime]: (20210428)
[//updatetime]: (20210428)

```solidity
// SPDX-License-Identifier: undefined
pragma solidity 0.6.6;

contract Foo{
    address public owner;
    constructor(address _owner) public{
        owner = _owner;
    }
}

contract AddressFinder{
    function getAddress(address _factory, bytes32 _salt, bytes calldata _bytecode) external pure returns (address){
        return address(uint(keccak256(abi.encodePacked(
                hex'ff',
                _factory,
                _salt,
                keccak256(_bytecode)
            ))));
    }
}

contract Factory {
    event deployed(address addr, uint256 salt);

    function deploy(bytes memory _bytecode, uint _salt) public {
        address addr;
        assembly {
            addr := create2(0, add(_bytecode, 0x20), mload(_bytecode), _salt)
            if iszero(extcodesize(addr)) {
                revert(0, 0)
            }
        }
        emit deployed(addr, _salt);
    }

    function getCreationBytecode(address _owner) public pure returns (bytes memory) {
        bytes memory bytecode = type(Foo).creationCode;
        return abi.encodePacked(bytecode, abi.encode(_owner));
    }
}
```

## context

How to depoly a contract with address have leading zeros like: `0x00000000` ?

1. `Foo` is the contract I want to deploy, but I want get it's address before deploy.
2. deploy `Factory` contract first, get it's address
3. call `getCreationBytecode` get bytecode of `Foo` contract
4. deploy `AddressFinder` contract
5. call `AddressFinder.getAddress` by pass factory address and `Foo` bytecode, and give a random `salt`, you will get an address in return.
6. use the same `salt` call `Factory.deploy`, you will get a `Foo` contract deployed in the same address you got at step5. Magic!
7. repeat step5, with other random `salt`, until find an address you like.

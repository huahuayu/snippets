[//title]: (solidity-abi-encode-decode)
[//englishtitle]: (solidity-abi-encode-decode)
[//category]: (solidity,snippet)
[//tags]: (solidity,encode,decode)
[//createtime]: (20210721)
[//updatetime]: (20210721)

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.6;
contract Console {
    event LogUint(string, uint);
    function log(string memory s , uint x) internal {
    emit LogUint(s, x);
    }

    event LogInt(string, int);
    function log(string memory s , int x) internal {
    emit LogInt(s, x);
    }

    event LogAddress(string, address);
    function log(string memory s , address x) internal {
    emit LogAddress(s, x);
    }

    event LogBytes(string, bytes);
    function log(string memory s , bytes memory x) internal {
    emit LogBytes(s, x);
    }

    event LogBytes32(string, bytes32);
    function log(string memory s , bytes32 x) internal {
    emit LogBytes32(s, x);
    }

    event LogBool(string, bool);
    function log(string memory s , bool x) internal {
    emit LogBool(s, x);
    }
}

contract AbiEncodeDecode is Console{
    function decode(address[] calldata _foo, uint[] calldata _bar, uint _amount) external{
        bytes memory data = encode(_foo, _bar, _amount);
        (address[] memory foo, uint[] memory bar, uint amount) = abi.decode(data, (address[], uint[], uint));
        uint l = foo.length;
        for(uint i = 0; i<l; i++){
            log("foo",address(foo[i]));
            log("bar", bar[i]);
        }
        log("amount",amount);
    }

    function encode(address[] calldata _foo, uint[] calldata _bar, uint _amount) internal returns (bytes memory){
        bytes memory data = abi.encode(_foo, _bar, _amount);
        log("encodeData", data);
        return data;
    }
}
```

test data:

```text
["0xD5A67554A4bA09A9d3f6F10e2D664dD72943e3E5","0xF4625AeD0db002105ec70793a85a2F8e3CcD164C","0x31FdF4333d2edCAdCebd25edd7DaBCB73B27e851"],[100,200,300],"10000"
```

output:

```json
[
  {
    "from": "0xDA0bab807633f07f013f94DD0E6A4F96F8742B53",
    "topic": "0xe8407a0209fa99ec3a7228aff140c3d3e68bd279391739c7e0b65cd406cc93b5",
    "event": "LogBytes",
    "args": {
      "0": "encodeData",
      "1": "0x000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000000e000000000000000000000000000000000000000000000000000000000000027100000000000000000000000000000000000000000000000000000000000000003000000000000000000000000d5a67554a4ba09a9d3f6f10e2d664dd72943e3e5000000000000000000000000f4625aed0db002105ec70793a85a2f8e3ccd164c00000000000000000000000031fdf4333d2edcadcebd25edd7dabcb73b27e8510000000000000000000000000000000000000000000000000000000000000003000000000000000000000000000000000000000000000000000000000000006400000000000000000000000000000000000000000000000000000000000000c8000000000000000000000000000000000000000000000000000000000000012c"
    }
  },
  {
    "from": "0xDA0bab807633f07f013f94DD0E6A4F96F8742B53",
    "topic": "0x62ddffe5b5108385f7a590f100e1ee414ad9551a31f089e64e82998440785e1e",
    "event": "LogAddress",
    "args": {
      "0": "foo",
      "1": "0xD5A67554A4bA09A9d3f6F10e2D664dD72943e3E5"
    }
  },
  {
    "from": "0xDA0bab807633f07f013f94DD0E6A4F96F8742B53",
    "topic": "0x941296a39ea107bde685522318a4b6c2b544904a5dd82a512748ca2cf839bef7",
    "event": "LogUint",
    "args": {
      "0": "bar",
      "1": "100"
    }
  },
  {
    "from": "0xDA0bab807633f07f013f94DD0E6A4F96F8742B53",
    "topic": "0x62ddffe5b5108385f7a590f100e1ee414ad9551a31f089e64e82998440785e1e",
    "event": "LogAddress",
    "args": {
      "0": "foo",
      "1": "0xF4625AeD0db002105ec70793a85a2F8e3CcD164C"
    }
  },
  {
    "from": "0xDA0bab807633f07f013f94DD0E6A4F96F8742B53",
    "topic": "0x941296a39ea107bde685522318a4b6c2b544904a5dd82a512748ca2cf839bef7",
    "event": "LogUint",
    "args": {
      "0": "bar",
      "1": "200"
    }
  },
  {
    "from": "0xDA0bab807633f07f013f94DD0E6A4F96F8742B53",
    "topic": "0x62ddffe5b5108385f7a590f100e1ee414ad9551a31f089e64e82998440785e1e",
    "event": "LogAddress",
    "args": {
      "0": "foo",
      "1": "0x31FdF4333d2edCAdCebd25edd7DaBCB73B27e851"
    }
  },
  {
    "from": "0xDA0bab807633f07f013f94DD0E6A4F96F8742B53",
    "topic": "0x941296a39ea107bde685522318a4b6c2b544904a5dd82a512748ca2cf839bef7",
    "event": "LogUint",
    "args": {
      "0": "bar",
      "1": "300"
    }
  },
  {
    "from": "0xDA0bab807633f07f013f94DD0E6A4F96F8742B53",
    "topic": "0x941296a39ea107bde685522318a4b6c2b544904a5dd82a512748ca2cf839bef7",
    "event": "LogUint",
    "args": {
      "0": "amount",
      "1": "10000"
    }
  }
]
```

## context

if use `abi.encodePacked` for encode , there's no `abi.decodePacked` function to use, because it non-standard.

## reference

[abi spec](https://docs.soliditylang.org/en/v0.8.6/abi-spec.html)

[What are ABI encoding functions in Solidity 0.4.24?](https://medium.com/@libertylocked/what-are-abi-encoding-functions-in-solidity-0-4-24-c1a90b5ddce8)

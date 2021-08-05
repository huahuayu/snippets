[//title]: (solidity-uniswap-like-pair-query-multicall)
[//englishtitle]: (solidity-uniswap-like-pair-query-multicall)
[//category]: (solidity,snippet,ethereum)
[//tags]: (solidity,snippet,uniswap,multicall)
[//createtime]: (20210623)
[//updatetime]: (20210805)

```solidity
//SPDX-License-Identifier: MIT
pragma solidity 0.6.6;

interface IPair {
    function token0() external view returns (address);
    function token1() external view returns (address);
    function getReserves() external view returns (uint112 reserve0, uint112 reserve1, uint32 blockTimestampLast);
}

abstract contract Factory  {
    address[] public allPairs;
    function allPairsLength() external view virtual returns (uint);
}

contract PairQuery {
    function getPairs(IPair[] calldata _pairs) external view returns (address[3][] memory, uint[2][] memory, uint) {
        uint len = _pairs.length;
        address[3][] memory result = new address[3][](len);
        uint[2][] memory reserves = new uint[2][](len);
        for (uint i = 0; i < len; i++) {
            IPair pair = IPair(_pairs[i]);
            result[i][0] = pair.token0();
            result[i][1] = pair.token1();
            result[i][2] = address(pair);
            (reserves[i][0], reserves[i][1], ) = pair.getReserves();
        }
        return (result,reserves,block.number);
    }

    function getPairsByIndexRange(Factory _factory, uint _start, uint _stop) external view returns (address[3][] memory, uint[2][] memory, uint) {
        uint _allPairsLength =_factory.allPairsLength();
        if (_stop > _allPairsLength) {
            _stop = _allPairsLength;
        }
        require(_stop >= _start, "start cannot be higher than stop");
        uint len = _stop - _start + 1;
        address[3][] memory result = new address[3][](len);
        uint[2][] memory reserves = new uint[2][](len);
        for (uint i = 0; i < len; i++) {
            IPair pair = IPair(_factory.allPairs(_start + i));
            result[i][0] = pair.token0();
            result[i][1] = pair.token1();
            result[i][2] = address(pair);
            (reserves[i][0], reserves[i][1], ) = pair.getReserves();
        }
        return (result,reserves,block.number);
    }

    function getAllPairLength(Factory _factory) external view returns (uint) {
        return _factory.allPairsLength();
    }

    function getAllPairLengthByFactorys(Factory[] calldata _factorys) external view returns (uint[] memory, uint) {
        uint len = _factorys.length;
        uint[] memory result = new uint[](len);
        for (uint i = 0; i < len; i++){
            result[i] = _factorys[i].allPairsLength();
        }
        return (result, block.number);
    }
}
```

## context

depolyed at:
https://etherscan.io/address/0x80Ddf6DeC02a0958E3e2629892f7b3015829Bb73  
https://bscscan.com/address/0x7bD13ece4326F463A45ad6a82d82e33611389765  
https://polygonscan.com/address/0x737e30A607Be32c38C64a0F751825D7a70A861c6

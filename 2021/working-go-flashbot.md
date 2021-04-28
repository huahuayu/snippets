[//title]: (working-go-flashbot)
[//englishtitle]: (working-go-flashbot)
[//category]: (go,snippet)
[//tags]: (go,snippet)
[//createtime]: (20210428)
[//updatetime]: (20210428)

```go
package ethrpc

import (
    "bytes"
    "crypto/ecdsa"
    "crypto/tls"
    "github.com/ethereum/go-ethereum/common/hexutil"
    ethcrypto "github.com/ethereum/go-ethereum/crypto"
    "io/ioutil"
    "net/http"
)

type FlashbotsTransport struct {
    privateKey    *ecdsa.PrivateKey
    publicAddress string
    r             http.RoundTripper
}

func signHash(hashString string) []byte {
    return ethcrypto.Keccak256([]byte("\x19Ethereum Signed Message:\n66" + hashString))
}

func (h *FlashbotsTransport) RoundTrip(request *http.Request) (*http.Response, error) {
    body, err := ioutil.ReadAll(request.Body)
    if err != nil {
        return nil, err
    }
    request.Body = ioutil.NopCloser(bytes.NewBuffer(body))

    signatureBytes, err := ethcrypto.Sign(signHash(hexutil.Encode(ethcrypto.Keccak256(body))), h.privateKey)
    if err != nil {
        return nil, err
    }

    request.Header.Add("X-Flashbots-Signature", h.publicAddress+":"+hexutil.Encode(signatureBytes))
    return h.r.RoundTrip(request)
}
```

## context

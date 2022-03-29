[//title]: (get-local-and-external-ip-address-in-golang)
[//englishtitle]: (get-local-and-external-ip-address-in-golang)
[//category]: (go,network,snippet)
[//tags]: (go,network,snippet,ip)
[//createtime]: (20220329)
[//updatetime]: (20220329)

```go
package ip

import (
	"fmt"
	"io/ioutil"
	"net"
	"net/http"
	"testing"
)

func TestGetLocalIP(t *testing.T) {
	addrs,_ := getLocalIP()
	for _, a := range addrs{
		fmt.Println(a)
	}
// 172.19.208.108
// 172.19.198.50
}

func TestGetOutboundIP(t *testing.T) {
	ip, _ := getOutboundIP()
	fmt.Println(ip)
// 172.19.198.50
}

func TestGetExternalIP(t *testing.T) {
	ip, _ := getPublicIP()
	fmt.Println(ip)
// 69.172.92.94
}

// getLocalIP get all your local ipv4 address (except 127.0.0.1)
func getLocalIP() ([]string, error) {
	addrs, err := net.InterfaceAddrs()
	if err != nil {
		return nil, err
	}
	IPs := make([]string, 0)
	for _, a := range addrs {
		if ipNet, ok := a.(*net.IPNet); ok && !ipNet.IP.IsLoopback() {
			if ipNet.IP.To4() != nil {
				IPs = append(IPs, ipNet.IP.To4().String())
			}
		}
	}
	return IPs, nil
}

// getOutboundIP get the out bound ip, especially useful when you have multi local ipv4 ip and you want figure out which one is been used
func getOutboundIP() (string, error) {
	conn, err := net.Dial("udp", "8.8.8.8:80")
	//conn, err := net.Dial("udp", "114.114.114.114:80")
	if err != nil {
		return "", err
	}
	defer conn.Close()
	localAddr := conn.LocalAddr().(*net.UDPAddr)
	return localAddr.IP.String(), nil
}

// getPublicIP get your publilc ip
func getPublicIP() (string, error) {
	resp, err := http.Get("https://ifconfig.me")
	if err != nil {
		return "", err
	}
	defer resp.Body.Close()
	body, err := ioutil.ReadAll(resp.Body)
	if err != nil {
		return "", err
	}
	return string(body), nil
}
```

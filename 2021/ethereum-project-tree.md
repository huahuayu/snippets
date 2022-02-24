[//title]: (ethereum-source-tree)
[//englishtitle]: (ethereum-source-tree)
[//category]: (go,ethereum,snippet)
[//tags]: (go,ethereum,snippet)
[//createtime]: (20220224)
[//updatetime]: (20220224)

```text
go-ethereum
├── accounts                        # 实现了一个高等级的以太坊账户管理
│   ├── abi
│   ├── external
│   ├── keystore
│   ├── scwallet
│   └── usbwallet
├── build                           # 编译相关脚本，编译好的可执行文件也放在这里（bin目录）
│   └── deb
├── cmd                             # 命令行工具
│   ├── abidump                     # Parses the given ABI data and tries to interpret it from the fourbyte database.
│   ├── abigen                      # 通过合约生成go代码，实现和go和合约的交互
│   ├── bootnode                    # 启动一个bootstrap节点帮助节点发现
│   ├── checkpoint-admin
│   ├── clef                        # 独立交易签名器，实现一方请求一方确认；规则引擎，实现自动化请求确认
│   ├── devp2p                      # 和节点网络层进行交互的utility
│   ├── ethkey
│   ├── evm                         # Developer utility version of the EVM
│   ├── faucet                      # 水龙头
│   ├── geth                        # 以太坊节点
│   ├── p2psim
│   ├── puppeth                     # 帮助创建一个新以太坊网络的命令行向导
│   ├── rlpdump                     # Developer utility tool to convert binary RLP to user-friendlier hierarchical representation
│   └── utils
├── common                          # 公共的工具类
│   ├── bitutil
│   ├── compiler
│   ├── fdlimit
│   ├── hexutil
│   ├── math
│   ├── mclock
│   └── prque
├── consensus                       # 提供了以太坊的一些共识算法，比如ethhash, clique(proof-of-authority)
│   ├── beacon
│   ├── clique
│   ├── ethash
│   └── misc
├── console                         # console类
│   ├── prompt
│   └── testdata
├── contracts
│   └── checkpointoracle
├── core                            # 以太坊的核心数据结构和算法(虚拟机，状态，区块链，布隆过滤器)
│   ├── asm
│   ├── beacon
│   ├── bloombits
│   ├── forkid
│   ├── rawdb
│   ├── state
│   ├── types
│   └── vm
├── crypto                          # 加密和hash算法
│   ├── blake2b
│   ├── bls12381
│   ├── bn256
│   ├── ecies
│   ├── secp256k1
│   └── signify
├── docs
│   ├── audits
│   └── postmortems
├── eth                             # 实现了以太坊的协议
│   ├── catalyst
│   ├── downloader
│   ├── ethconfig
│   ├── fetcher
│   ├── filters
│   ├── gasprice
│   ├── protocols
│   └── tracers
├── ethclient                       # 提供了以太坊的RPC客户端
│   └── gethclient
├── ethdb                           # eth的数据库(包括实际使用的leveldb和供测试使用的内存数据库)
│   ├── dbtest
│   ├── leveldb
│   └── memorydb
├── ethstats                        # 提供网络状态的报告
├── event                           # 处理实时的事件
├── graphql
├── internal
│   ├── build
│   ├── cmdtest
│   ├── debug
│   ├── ethapi
│   ├── flags
│   ├── guide
│   ├── jsre
│   ├── shutdowncheck
│   ├── syncx
│   ├── testlog
│   ├── utesting
│   └── web3ext
├── les                             # 实现了以太坊的轻量级协议子集
│   ├── catalyst
│   ├── checkpointoracle
│   ├── downloader
│   ├── fetcher
│   ├── flowcontrol
│   ├── utils
│   └── vflux
├── light                           # 实现为以太坊轻量级客户端提供按需检索的功能
├── log                             # 提供对人机都友好的日志信息
├── metrics                         # 统计
│   ├── exp
│   ├── influxdb
│   ├── librato
│   └── prometheus
├── miner                           # 提供以太坊的区块创建和挖矿
│   └── stress
├── mobile                          # 移动端使用的一些warpper
├── node                            # 以太坊的多种类型的节点
├── p2p                             # 以太坊p2p网络协议
│   ├── discover
│   ├── dnsdisc
│   ├── enode
│   ├── enr
│   ├── msgrate
│   ├── nat
│   ├── netutil
│   ├── nodestate
│   ├── rlpx
│   ├── simulations
│   └── tracker
├── params
├── rlp                             # 以太坊序列化处理
│   ├── internal
│   └── rlpgen
├── rpc                             # 远程方法调用
│   └── testdata
├── signer
│   ├── core
│   ├── fourbyte
│   ├── rules
│   └── storage
├── swarm                           # swarm网络处理
├── tests                           # 测试
│   ├── evm-benchmarks
│   ├── fuzzers
│   ├── solidity
│   └── testdata
└── trie                            # 以太坊重要的数据结构Package trie implements Merkle Patricia Tries
```

# 区块链评测工具

## 参考工具

* [caliper](https://github.com/hyperledger/caliper)
* [tape](https://github.com/Hyperledger-TWGC/tape)
     ![](https://i.imgur.com/cY86Pfk.png)

* 信通院的trustedbench（目前还没开源）
* [BlockchainPerformanceMonitoring](https://github.com/InPlusLab/BlockchainPerformanceMonitoring) from paper *A Detailed and Real-time Performance Monitoring Framework for Blockchain Systems*
    * parses only `TPS`, `starttime`, `endtime`, `txconfirmedcount`

## 性能指标 Performance Metrics

* 交易吞吐量 throughput/TPS
* 交易确认延迟 transaction latency
* 交易成功率 transaction success rate
* 只读操作吞吐量 read only TPS
* 只读操作延迟 read-only latency
* 系统可扩展性 scalability
* 系统容错性 fault-tolerant
        *note: test if the system is still workingwhen certain nodes fail*
    * CFT (our focus)
        * kafka
        * raft
    * BFT
        * PBFT
* 资源利用率（CPU，网络，磁盘，能耗等等）
 *note: based on system functionalities/tools*
* ~~新节点启动时间~~

## 支持平台 Supported Platform

* Hyperledger Fabric (Chaincode)
* Ethereum (Solidity)
* Fisco Bcos (Solidity)

## scenarios of using smart contracts

1. copyright protection 文化版权
    * NFT
    * 
3. law 司法存证
    * [Fisco Bcos code](https://github.com/FISCO-BCOS/evidenceSample)
4. government services 政务服务 
    * 智慧城市建设
    * 自然资源登记
    * 政务诚信
5. IoT 物联网
    [fabric code](https://github.com/yigitpolat/Hyperledger-Fabric-for-Trusted-IoT)
    * 智能家居跨平台联盟
    * 农业溯源
5. 金融行业 trade & finance
    * 网贷机构良性退出
    * 机构间对账
        * [fabric code](https://github.com/hyperledger/fabric-samples/tree/main/interest_rate_swaps)
    * 供应链金融
        * [Fabric code](https://github.com/wearetheledger/awesome-hyperledger-fabric)
    * 旅游金融
    * 拍卖
        * [fabric code](https://github.com/hyperledger/fabric-samples/tree/main/auction-simple)
6. 智慧社区
    * 物业管理
7. 公益事业
    * solidity codes
        * [1](https://github.com/vbarzokas/smart-contract-donations/blob/master/contracts/Charitable.sol)
        * [2](https://github.com/wsun19/Blockchains-Project/blob/master/contracts/Charity.sol)
        * [3](https://github.com/rubyruby/charity-contracts/blob/master/Charity.sol)
        Problem found: the functionalities of the code is rather simple just transfer assets
9. 人才招娉
10. 游戏娱乐
    Based on [DappRadar](https://dappradar.com/rankings/category/games)
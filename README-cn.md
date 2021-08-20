# 区块链评测工具

## 参考工具

* [caliper](https://github.com/hyperledger/caliper)
* [tape](https://github.com/Hyperledger-TWGC/tape)
     ![](https://i.imgur.com/cY86Pfk.png)

* 信通院的trustedbench（目前还没开源）
* [BlockchainPerformanceMonitoring](https://github.com/InPlusLab/BlockchainPerformanceMonitoring) from paper *A Detailed and Real-time Performance Monitoring Framework for Blockchain Systems*
    * parses only `TPS`, `starttime`, `endtime`, `txconfirmedcount`

# 智能合约性能测试报告

*基于超级账本性能测试白皮书（[原文地址](https://www.hyperledger.org/learn/publications/blockchain-performance-metrics)）*


## 性能指标 (Key Metrics)


* 只读操作延迟 Read Latency
Read Latency = Time when response received - submit time
只读操作延迟=收到响应的时间–提交时间
只读操作延迟是指当只读操作提交时和服务器接收到时中间的一段时间

* 只读操作吞吐量 Read Throughput/TPS
Read Throughput = Total read operations / total time in seconds
只读操作吞吐量=总读取操作数/总时间（秒）
只读操作吞吐量是指一个在规定的时间段内完成多少个读取操作的度量，用每秒读取数（Rate Per Second, RPS）表示。

* 交易确认延迟 Transaction Latency
Transaction Latency = (Confirmation time @ network threshold) – submit time
交易确认延迟=（确认时间@网络阈值）–提交时间
交易确认延迟是指从提交到结果在网络中广泛可用的时间，包括传播时间和由于共识机制而产生的任何稳定时间。


* 交易吞吐量 Transaction Throughput/TPS
Transaction Throughput = Total committed transactions / total time in seconds @ #committed nodes
交易吞吐量=提交的事务总数/总时间（秒）@ 已提交节点数
交易吞吐量是区块链SUT在规定的一段时间内提交有效交易的速率。请注意，这不是单个节点的速率，而是整个SUT的速率，即在网络的所有节点上提交的速率。此速率以网络大小的每秒交易数（Transaction Per Second， TPS）表示。


* 交易成功率 Transaction Success Rate
* 系统可扩展性 Scalability
* 系统容错性 Fault Tolerance
    *note: test if the system is still working when some nodes fail*
    * CFT crash fault tolerance
        * kafka
        * raft
    * BFT byzantine fault tolerance
        * PBFT
* 资源利用率（CPU，网络，磁盘，能耗等等）


## 智能合约分类及描述


* 贸易
    * 商业票据 [Commercial Paper](https://github.com/hyperledger/fabric-samples/tree/main/commercial-paper)
        * 参与方及功能 Participants
            * **Digibank**
                * 发行 Issue
            * **Magnetcorp**
                * 购买 Buy
                * 赎回 Redeem
                * 查询 Queries
* 物流
    * 供应链案例 [Supplychain Example](https://github.com/xcottos/convector-example-supplychain-master)
        * 智能合约将记录商品物流详情，商品从生产厂家生产出一直到消费者手里，商品信息都会上链
        * 参与方及功能
            + 供应商 **Supplier**
                + rawMaterialAvailable: is a number that expresses the quantity of raw material available to be supplied
            + 生产工厂 **Manufacturer**
                + rawMaterialAvailable: is a number that expresses the quantity of raw material available to be used for creating products
                + productsAvailable: is a number that expresses the quantity of products ready to be distributed
            + 运输中转 **Distributor**
                + productsToBeShipped: is a number that expresses the quantity of products ready to be shipped
                + productsShipped: is a number that expresses the quantity of products shipped
                + productsReceived: is a number that expresses the quantity of products shipped that have been received.
            + 零售商 **Retailer**
                + productsOrdered: is a number that expresses the quantity of products ordered
                + productsAvailable: is a number that expresses the quantity of products available for being sold
                + productsSold: is a number that expresses the quantity of products that have been sold
            + 顾客 **Customer**
                + productsBought: is a number that expresses the quantity of products bought
            + helper functions
                + **createSupplier**: creates a Supplier
                + **createManufacturer**: creates a Manufacturer
                + **createDistributor**: creates a Distributor
                + **createRetailer**: creates a Retailer
                + **createCustomer**: creates a Customer
                + **getAllSuppliers**: shows all the created Suppliers
                + **getAllManufacturers**: shows all the created Manufacturers
                + **getAllDistributors**: shows all the created Distributors
                + **getAllRetailers**: shows all the created Retailers
                + **getAllCustomers**: shows all the created Customers
                + **getAllModels**: shows all the created Models

* 文娱
    * [Simple Ping Pong Game](https://github.com/cnnrznn/fabric-samples/blob/release-1.4/chaincode/fabcar/javascript/lib/fabcar.js)
        * Based on fabcar example
        * The transacions per block was reduced to one to eliminate the latency of compiling a block
* 社会公共服务
    * 可信身份 [TrustID](https://github.com/hyperledger-labs/TrustID)
        * 去中心化的数字身份系统
        * 个人身份 Individual Identity
            * 独一无二的去中心化身份号码 DID
            * 公钥 PublicKey
            * 身份持有人 Controller
            * 权限 Access
        * 服务身份 Service Identity
            * 独一无二的去中心化身份号码 DID
            * 智能合约名称 Name
            * 是否是公开的服务 Public
            * 权限 Access
            * 服务持有人 Controller
* 金融
    * 国际金融区块链 [IBM/global-financing-blockchain](https://github.com/IBM/global-financing-blockchain)
        * 参与方及功能 Participants
            * 基于`订单(Order)`的智能合约
                * 订单状态包含 Created, Bought, Cancelled, Ordered, ShipRequest, Delivered, Delivering, Backordered, Dispute, Resolve, PayRequest, Authorize, Paid, Refund, Refunded
            * 买家
                * 创建订单
            * 卖家
                * 联系供应商
            * 物流
                * 运输物品
            * 金融公司
                * 中转交易费用给卖家

        ![](https://i.imgur.com/7x2AH7s.png)

        
* 政务
    * 市民脉搏 [citizen-pulse](https://github.com/hyperledger-labs/citizens-pulse)
        * 一个基于超级账本Fabric去中心化的市民参政议政平台
        * 主要内容为针对Plan的CRUD操作
        * CRUD OPs
            * Plan
            * PlanPriveteDetails
* 知识产权
    * [fabric-ipn-contract](https://github.com/mickeymond/fabric-ipn-contract/blob/master/src/contracts/CopyrightContract.ts)
        * 知识产权上链
        * 主要内容为针对Copyright的CRUD操作
        * CRUD OPs
            * Copyright
* 社交
    * forum content to chain (example not found on chaincode)
        * solidty
* 日常消费
    * 物流链案例 Supply Chain Example
        * [fabric-supply-chain](https://github.com/jiaxyan/fabric-supply-chain/blob/master/example01/chaincode.go)
            * ProductName
            * Supplier
            * ArrivedTime
            * Singature
        * 自动生产框架 [Automation Framework](https://github.com/hyperledger-labs/blockchain-automation-framework/blob/master/docs/source/example/supplychain.md)
            * 物品信息上链
            * [chaincode](https://github.com/hyperledger-labs/blockchain-automation-framework/blob/master/examples/supplychain-app/fabric/chaincode_rest_server/chaincode/supplychain/Common.go)
            * trackingID
            * type
            * health
            * location
            * containerID
            * custodian
            * timestamp
            * contents
            * participants
* 工业
    * 物流链
<!--     * Fabric机器 [Fabric-Machine](https://github.com/hyperledger-labs/fabric-machine)
        * 基于FPGA的硬件加速器 -->
* 农业
    * 精准农业 [Precision Farming](https://github.com/manilpuri9/hyperledger-fabric-precision-farming)
        * 针对农作物(Crop)的操作，包含以下属性
            * `GeoLocation`
            * `FarmInfo`
            * `Temperature`
            * `Pressure`
            * `Humidity`
            * `Radiation`
            * `Moisture`
            * `Nitrogen`
            * `Phosphorus`
            * `Weather`
            * `SoilCondition`
* 能源
    * 去中心化的能源交易 [Decentralized Energy](https://github.com/IBM/decentralized-energy-fabric-on-IBP20)
        * 参与方 Participants
            * 住户 **Residents**
            * 银行 **Banks**
            * 功能公司 **utilityCompanies**
            * 身份地图 **identityMap**
        * Functions
            * 能源交易 EnergyTrade
            * 现金交易 CashTrade
* 教育
    * 教育链 [eduCC](https://github.com/kevin-hf/education/blob/master/chaincode/eduCC.go)
        * 数据上链，进行CRUD操作
        * 简单的数据存储
* 医疗
    * [substra-chaincode](https://github.com/Substra/substra-chaincode)
        * 基于一个保证安全可信的机器学习任务分发框架
        * 参与方 Participants
            * 数据管理员 DataManager
                * 数据 DataSamples
                * 算法 Algo
                * 任务 Objective
                * 设置 Traintuple
            * 医院
                * 训练数据 Train DataSamples
                * 测试数据 Test DataSamples
        * 功能 Functions
            * CRUD
            * log
            * query

![](https://doc.substra.ai/_images/architecture_overview.png)



## Appendix 附录

* 测试系统

显示了区块链性能评估的典型配置。左侧的测试线束在右侧显示了用于针对被测系统（SUT）生成负载的程序和系统。图1中的每个术语都在本节中定义。
![](https://i.imgur.com/mmYMd3h.png)

* 测试工具

测试工具是用于运行性能评估的硬件和软件。这个测试工具通常代表许多客户机，这些客户机可以注入工作负载并在任意数量的节点上进行观察。

* 客户

一个客户是可以将工作引入系统或调用系统行为的实体。在区块链系统中，通常在多个级别上有多种类型的客户端。

一个负载生成客户端代表用户向区块链网络（SUT）提交交易的节点，通常遵循自动测试脚本。客户机和SUT之间的接口可以从简单的表示状态转移（REST）接口到全面的软件开发工具包（SDK）。根据接口的不同，客户机可以是无状态的，也可以是有状态的。

一个观察客户是一个节点，它接收来自SUT的通知，或者可以查询SUT有关已提交事务的状态，通常在自动测试脚本之后。可以有多个观察客户端。观察客户端不能提交任何新事务。

* 测试系统(SUT)

定义被测系统（SUT）是一个复杂的问题。在本文档中，SUT被定义为运行和维护区块链所需的硬件、软件、网络和具体配置。或不包括任何用于加速读取外部数据库的时间。

* 节点

在区块链网络的上下文中，节点是一个独立的计算实体，它与网络中的其他节点通信，共同协作完成交易。

节点是一个虚拟实体，从某种意义上说，它可以运行在物理硬件上，也可以作为VM或容器化环境运行。在后一种情况下，节点可以与同一网络中的其他节点共享物理硬件。
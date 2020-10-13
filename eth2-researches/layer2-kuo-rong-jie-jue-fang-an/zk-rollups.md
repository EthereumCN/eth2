# ZK-Rollups

### 背景

Plasma是一种第二层扩容性解决方案，以侧链形式搭建在以太坊区块链之上。Plasma实现使得我们能够在链下处理侧链中的数百个交易，而且只需要将侧链区块的单个哈希值添加到以太坊区块链中。但这种方案存在一些固有缺陷，导致无法进一步扩容。如果用户想要退出侧链，则需要保留大量的数据，以便之后能够继续进行验证。并且，漫长的挑战期内用户也必须保持在线，否则就会失去奖励。因此，大家一直在探索对用户更加友好、对资源要求更低的第二层扩容性方案，ZK-Rollups便是其中之一。

### 简介 <a id="_2"></a>

ZK-Rollups是当前的第二层解决方案之一，通过在单笔交易中对大量资金转移进行集中处理以提升扩容性。Plasma在每次发生资金转移时都会创建一笔交易，而ZK-Rollups则将数百次转移都捆绑在一笔交易中。智能合约负责解构并验证单笔交易中所包含的所有转移。

而"零知识证明"则被用来呈现并且公开记录以太坊区块链上Rollup区块的有效性。ZK（零知识）通过压缩交易中所包含的数据，从而减少验证区块时所占用的计算和存储资源。

### 概述 <a id="_3"></a>

ZK-Rollup方案中包括两种类型的用户：交易者和中继者。交易者创建其资金转移，并将转移广播到网络中。转移数据中包含索引化的“to”和“from”地址、交易值、网络费用和随机数。地址经索引之后被缩短为3个字节，减少了资源处理的需求。交易值大于零创建为存款，小于零则创建为提款。智能合约将数据记录在两颗默克尔树中，地址和交易量被分别记录在这两颗默克尔树中。

中继者则收集大量的资金转移以创建一个rollup。生成SNARK证明也是中继者的工作。SNARK证明是一个哈希值，代表区块链状态的变动，此处状态指“存在状态”。SNARK证明将发生转移之前的区块链快照与发生转移之后的区块链快照（即钱包余额）进行比较，并仅将哈希可验证的变更馈送到主网。

值得注意的是，只要在智能合约中按规定质押了保证金，任何人都可以成为中继者。锁定保证金的机制在一定程度上避免了中继者篡改或阻挠rollup。

### 用户体验 <a id="_4"></a>

使用ZK-Rollup机制的dapp用户交易费将更低。创建零知识证明需要大量的算力。提议的实现是采用“提交-验证”方式。区块确认的等待时间将延长，因为SNARK证明将存在一定数量区块的延迟。在实现之前，这对用户的影响暂未可知。

### 优缺点 <a id="_5"></a>

优点：

* 减少交易费用
* 速度优于Optimistic Rollup和Plasma
* 在并行计算模型中计算区块，促进去中心化
* 压缩每笔交易所含数据，提升吞吐量和第二层扩容性
* Optimistic Rollup需要进行欺诈验证，而ZK-Rollup则是通过延迟提款（至多两周）预防欺诈

缺点：

* 计算零知识证明有一定难度，因此需要优化数据以达到最大吞吐量
* ZK-Rollups的初始设定催生中心化机制（参阅“安全性考量”）
* 安全机制以一定程度且无需验证的信任为前提
* 量子计算会对ZK-Rollup区块链造成威胁

### Demo <a id="demo"></a>

* [ZK Sync Network](https://demo.zksync.dev/explorer/) 是一个ZK-Rollup区块链的示例

### 安全性考量 <a id="_6"></a>

ZK-Rollups的初始设定为信任状态，即使无法验证信任。一小部分开发者将负责信任状态的初始设定，假若贿赂开发者操纵代码或是提供漏洞信息，就会妨害去中心化程度，同时也伴随着攻击风险。

量子计算会对ZK-Rollup造成一定威胁，因为与当前的加密协议相比，SNARK证明的哈希被“猜中”的几率更大。

### 相关资源 <a id="_7"></a>

* [零知识证明 - 视频介绍](https://youtu.be/0Sy6nb72gCk)
* [什么是zkSNARKs？](https://blog.ethereum.org/2016/12/05/zksnarks-in-a-nutshell/)
* [通过集中验证交易可能将链上吞吐量提升至500笔/秒](https://ethresear.ch/t/on-chain-scaling-to-potentially-500-tx-sec-through-mass-tx-validation/3477)
* [ZK Rollup & Optimistic Rollup \(En\)](https://medium.com/coinmonks/zk-rollup-optimistic-rollup-70c01295231b)
* [链上扩容提供完整数据可用性。那么将验证移至链下呢？](https://ethresear.ch/t/on-chain-scaling-with-full-data-availability-moving-verification-of-transactions-off-chain/3847)



### 文章来源

[EthHub](https://zh.docs.ethhub.io/%E4%BB%A5%E5%A4%AA%E5%9D%8A%E8%B7%AF%E7%BA%BF%E5%9B%BE/layer-2-%E6%89%A9%E5%AE%B9%E6%96%B9%E6%A1%88/zk-rollups/)


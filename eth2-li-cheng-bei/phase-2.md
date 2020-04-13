# Phase 2

## [Eth2 Phase2 Wiki](https://hackmd.io/UzysWse1Th240HELswKqVA?view#Eth-1--gt-Eth-2-Switchover)

本文档将梳理、跟踪目前Eth2 阶段2的最新进展、相关讨论和决策。

**欢迎大家参与编辑！**

如果有兴趣参与本文档编辑，请前往[sharding的gitter聊天室](https://gitter.im/ethereum/sharding)申请编辑权限。

## **入门**

Vitalik Buterin的阶段2提案：[https://notes.ethereum.org/s/Bkoaj4xpN](https://notes.ethereum.org/s/Bkoaj4xpN)

阶段2相关介绍：

* Scaling Ethereum - [Phase 2 ](https://www.youtube.com/watch?v=RW7K3JQOZOg&t=73m35s)
* Scaling Ethereum - [Phase 2 执行、Scout及Serenity历史](https://www.youtube.com/watch?v=RW7K3JQOZOg&t=104m33s)
* [Eth2 费用市场（中继器/状态提供者/内存池）](https://ethresear.ch/t/state-providers-relayers-bring-back-the-mempool/5647)
* [阶段2开放设计](https://www.youtube.com/watch?v=RW7K3JQOZOg&t=34m50s)

## 什么是Scout？

Scout是 Eth2 阶段2执行原型引擎，目前支持以YAML格式读取和输出分片/信标状态，并将扩展为客户端工具。

[https://github.com/ewasm/scout](https://github.com/ewasm/scout) \(Rust\)  
[https://webassembly.studio/?f=isz2bypxpy](https://webassembly.studio/?f=isz2bypxpy) \(使用Javascript + Typescript编写执行环境\) - 此功能正在积极开发中，不如上述Rust版本成熟  
[https://ethresear.ch/t/phase-2-execution-prototyping-engine-ewasm-scout/5509](https://ethresear.ch/t/phase-2-execution-prototyping-engine-ewasm-scout/5509)

**目标：**

* 创建一个（黑箱化的）执行原型化引擎
* 创建一些实例合约（“执行脚本”）
* 为EEs提供正式化[运行时主机功能](https://github.com/ewasm/scout/blob/ef9a11e83248e120ff830747fcbcadc29b62b868/src/main.rs#L64-L126)
* 确定执行任意wasm代码的有效方法
* 促进其他团队创建可用脚本
* 通过在脚本中包含实际用例，我们可以对设计进行基准测试（例如无状态）并确定瓶颈

年终目标是构建完整的Eth2测试网（执行阶段1），集成scout和样本执行环境。

## 执行环境 EEs

当前正在进行原型化的执行环境列表：

* [原始提案](https://notes.ethereum.org/s/Bkoaj4xpN)中描述的分片内ETH传输样本
* 通用资产（通证/ERC20）
* Rollup验证
* 基础数据写入
* Intel SGX 验证程序

需要构建的长效执行环境：

* Eth 1 EE
* Eth 2 EE
* 延迟状态执行框架

建议构建的执行环境：

* ZEXE
* 跨分片的Plasma checkin
* Libra/比特币或其他区块链？

关于Eth2执行环境的早期建议：[https://ethresear.ch/t/eth-execution-environment-proposal/5507](https://ethresear.ch/t/eth-execution-environment-proposal/5507)

## Eth 1 -&gt; Eth 2 迁移

在如何实现Eth1到Eth2的具体机制上还处于开放讨论中，但普遍共识是在社区主导下将Eth1切换为Eth2上的一个分片。这种方式需要在信标链上进行硬分叉，才能使信标链上的资金进入Eth1执行环境。硬分叉还需要为特定分片上的执行环境提供初始状态根。

Eth1执行环境也可以扩展为分片感知，这将为当前的Eth1增加其他功能。

迁移内容可能包括在Ewasm中编写EVM并在执行环境中使用。

Casey & Vitalik在推特上进行的相关讨论：  
[https://twitter.com/VitalikButerin/status/1134988921165758466](https://twitter.com/VitalikButerin/status/1134988921165758466)

Ethresear.ch中的开放讨论：  
[https://ethresear.ch/t/work-to-natively-integrate-eth1-into-eth2/5573](https://ethresear.ch/t/work-to-natively-integrate-eth1-into-eth2/5573)

## 跨链交易

目前处于开放讨论中。总体目标是搭建Eth2测试网，继而对不同的模型和假设进行测试。

#### 异步跨分片交易 <a id="Asynchronous-Cross-Shard-Transactions"></a>

关于yanking/收据模型的讨论。需要信标链上的交联才能最终确认（约6分钟）

* [https://ethresear.ch/t/phase-2-pre-spec-cross-shard-mechanics/4970](https://ethresear.ch/t/phase-2-pre-spec-cross-shard-mechanics/4970)
* [https://ethresear.ch/t/cross-shard-contract-yanking/1450](https://ethresear.ch/t/cross-shard-contract-yanking/1450)

#### Optimistic异步跨分片交易 <a id="Optimistic-Asynchronous-Cross-Shard-Transactions"></a>

这些模型围绕分叉选择规则以及如何进行重组来创建框架。在这些模型中，跨分片交易的延迟应为一个slot或一个区块（约4秒）。

* [https://ethresear.ch/t/fast-cross-shard-transfers-via-optimistic-receipt-roots/5337/9](https://ethresear.ch/t/fast-cross-shard-transfers-via-optimistic-receipt-roots/5337/9)
* Scaling Ethereum Talk, Barry Whitehat - [使用Rollup的跨分片支付](https://www.youtube.com/watch?v=RW7K3JQOZOg&t=178m25s)

#### 同步跨分片交易 <a id="Synchronous-Cross-Shard-Transfers"></a>

关于同步交易的讨论通常涉及“延迟状态执行” \([delayed state execution](https://ethresear.ch/t/delayed-state-execution-in-practice/1041)\) 的概念。这个概念将主链作为交易的组织和协调层。可以引入许多激励机制，以使第二层轻客户端负责在当前状态下执行交易。[一篇帖子](https://ethresear.ch/t/layer-2-state-schemes/5691/8)将延迟状态执行的某些版本称为“状态方案”。

* [https://ethresear.ch/t/synchronous-cross-shard-transactions-with-consolidated-concurrency-control-and-consensus-or-how-i-rediscovered-chain-fibers/2318](https://ethresear.ch/t/synchronous-cross-shard-transactions-with-consolidated-concurrency-control-and-consensus-or-how-i-rediscovered-chain-fibers/2318)
* [https://ethresear.ch/t/simple-synchronous-cross-shard-transaction-protocol/3097](https://ethresear.ch/t/simple-synchronous-cross-shard-transaction-protocol/3097)
* 有关延迟状态执行的讨论 - [https://ethresear.ch/t/a-data-availability-blockchain-with-sub-linear-full-block-validation/5503](https://ethresear.ch/t/a-data-availability-blockchain-with-sub-linear-full-block-validation/5503)
* [https://ethresear.ch/t/various-kinds-of-scaling-execution-models-and-multi-chains/5488](https://ethresear.ch/t/various-kinds-of-scaling-execution-models-and-multi-chains/5488)
* [https://ethresear.ch/t/layer-2-state-schemes/5691/8](https://ethresear.ch/t/layer-2-state-schemes/5691/8)

## 状态提供者及基础设施

Scout目前正致力于对可行性/吞吐量以及更多有关执行环境的无状态模型进行基准测试。假设使用无状态模型，则需要适当的基础设施。例如，需要有一组参与者来维护当前状态并打包交易的见证数据。每个分片的多个执行环境周围也需要存在存档节点和全节点，以保留状态的历史记录。所有这些参与者角色都需要进一步探索。

Vitalik[讨论](https://ethresear.ch/t/one-fee-market-ee-to-rule-them-all/5608/5)了有关如何接收当前状态或向交易添加见证/状态数据。轻客户端是提供此状态数据的自然候选者。要注意的是，轻客户端只能在一个分片上运行。确实还有一些问题悬而未决：

* 对于不同的执行环境我们是否需要不同的轻客户端来操作状态？
* 我们如何构建一个简单、快速运行的守护程序以增强分布式网络对于中心化服务器的竞争力？
* 统一状态通道设置，以便用户发现并支付轻型客户端服务费？
* 节点如何结合来自多个用户/提供者的数据？对此已进行了一些[讨论](https://ethresear.ch/t/state-providers-relayers-bring-back-the-mempool/5647)。

## 费用市场

对此已经进行了诸多讨论。最初，中继者市场 \(relayer market\) 被提出。[此处](https://ethresear.ch/t/state-providers-relayers-bring-back-the-mempool/5647)是相关背景和更多信息。

最近提出了一种替代方法。该中继者市场允许任何中继者打包交易，只需要区块矿工在区块末尾向费用市场EE发出一次调用。此调用将资金从中继者转移到区块矿工，以验证交易的哈希值已包括在内。因此共识层需要添加一种回溯机制，从而允许附加的wasm主机功能，使交易能够读取同一区块中先前交易的哈希。这是一种向中继者支付交易哈希打包费的简单方式。

Eth1或Eth2 EE中的费用市场的细节（类似于EIP 1559）是一个公开主题，尚未进行深入探索。另外，已经建议将轻客户端作为一种通过状态通道提供状态数据的机制。对于唯一的EE（例如基于ZK的EE），费用市场的建设必须良好运作，这一点至关重要。[此处](https://ethresear.ch/t/layer-2-state-schemes/5691)是针对费用市场和第二层机制影响的一些讨论。

## 开放性问题

实现细节、可行性和吞吐量方面还存在许多悬而未决的问题：

* 如何不采取分叉方式实现EE升级
  * 允许合约将自身拉取\(yanking\)到新的EE中，这假设合约由特定一方所有，并且在EE内部更新合约
* 执行环境治理（与上述问题相关）
* 发布执行环境的费用
  * 在每个分片和在信标链发布脚本独立收费？
  * 应该收取多少费用？
* 费用市场、状态提供者（见证提供者）、轻客户端等等需要基础设施的支撑
* 无状态模型的吞吐量和可行性
* 支持同一分片上执行环境之间的同步调用
* 跨分片交易、调用以及其他机制
* Eth1执行环境细节
* 由社区/EF支持的Eth2执行环境细节
* 独立启动阶段1或在阶段1中使用原始执行环境推迟启动阶段2（允许进行测试，引入经测试的eth1/eth2环境）
* 作为验证者节点或其他共享交易方式的一部分引入内存池 \(mempool\)

## FAQ

_阶段2的大致时间线和路线图是什么？_

这需要社区讨论决定。例如关于建立两个主要执行环境的讨论。其中一个侧重于eth1，以及迁移当前的合约状态等。另一个则专注于优化eth2，从而使合约和资金能够轻松过渡。这可以提供更高的灵活性，因为它不会受到当前eth 1设计的制约。然而，这两个执行环境都需要大量的维护、时间和测试才能完成。我们预计第2阶段将在这些执行环境完成之前准备就绪。这取决于社区的需求。

_首先启动简单的传输、Rollups、第二层checkin和更简单的执行环境是否有帮助？_

在启动过渡或启动eth 2 / eth 1执行环境之前，拥有一个开放的系统可能会有所帮助。

_那么账户抽象和与其相关的对话呢？_

现在将其授权给实际的执行环境本身。可以在执行环境的基础上建立相应规则。

## 相关术语

**Delayed Execution 延时执行**

执行不会在共识或核心协议层内发生，而是在第二层发生，随着更多事务或重组的引入，允许重新执行。假设有专门用于执行的独立轻客户端，主链仅充当组织事务的机制。通常这种方法作为原子或同步跨分片交易的解决方案进行讨论。请参阅上述“跨分片交易”部分。

**Dynamic Host Function \(DHF\) 动态主机功能**

在运行时动态链接到执行环境的额外主机功能。

**Execution Environment \(EE\) 执行环境**

部署到信标链的纯粹折叠函数。每个分片共识层内的执行将在执行环境的准则/框架内进行。本质上，执行环境是规则的框架/规则集，用于确定Ewasm作为虚拟机如何进行状态转换。它限制了状态的存储和更改方式。

**Execution Environment Shard State 执行环境分片状态**

如[Vitalik的提案](https://notes.ethereum.org/s/Bkoaj4xpN)所述，每个分片都包含一个状态根列表，这些状态根映射到信标链上定义的执行环境。每个执行环境在分片上维护一个状态根。目前存在一些疑问：状态根/功能是否存在每个分片上，或者在每个分片上包含状态根是否需要付费。

**Eth 1 EE**

Eth 1执行环境将定义规则/系统，以说明当前eth1帐户等如何在eth 2中运行。当前的讨论表明，分片将专用于eth 1 EE，并将引入其他规则以允许跨分片交易和交互。目的是防止过渡时当前的以太坊账户和交易发生中断。

**Ethereum Environment Interface \(EEI\) 以太坊环境接口**

EEI是一组DHF，为执行中的EE及其子代提供以太坊特定功能，例如检索当前区块编号、调用合约、确定交易发送方等。

**Eth 2 EE**

Eth 2大大增加了可能性，并尽力保持与eth 1 EVM、规则和合约的兼容性。结果针对引入经扩展的eth 2 EE进行了讨论，该eth 2 EE可以轻松地与eth 1 EE进行桥接。

**Generic Asset EE**

A concept where one execution environment manages token and eth balances across all execution environments. If synchronous calls between execution environments in the same shard is supported, this approach may be quite valuable. If not, it would likely be used as an asynchronous system to claim funds in a universal fee market. Some discussion here: [https://ethresear.ch/t/one-fee-market-ee-to-rule-them-all/5608/11](https://ethresear.ch/t/one-fee-market-ee-to-rule-them-all/5608/11)

**Host Function**

A host function is a method that the node makes available to the execution environment during runtime. The [list](https://github.com/ewasm/ewasm-rust-api/blob/92d14a6072ff4f15963ac8ac1ef0afb4681445d0/src/eth2.rs#L20-L24) of host functions is still under specification.

**Light client Server**

A set of actors dedicated to syncing to the latest state for a shard. It may or may not contain historical data and should keep track of the result/transactions of each slot. Light client servers should be capable of submitting transactions to the network or validator mempools. Some discussion regarding the fee market introduces the concept of light client servers as witness/state providers for transactions in a stateless system. Incentives may be introduced/encouraged via state channels, etc… See fee market section above.

**Relayer**

This term may or may not be deprecated. However, it is the actor which provides state data or witness data to a set of transactions. Older proposals gave the relayer additional responsibilities and power over blocks to be included. See Fee market discussion for more information.

**Scout**

Scout is an eth 2 phase 2 execution prototyping engine. It currently supports reading and outputting shard/beacon states in a YAML format and will be expanded to a client tool. See section on Scout.

**State Provider**

A suggestion for extended capabilities of light client servers. Users may open a state channel with a light client provider and pay to include the appropriate witness/state data needed for a stateless system. These actors can be defined as state providers.

**Stateless**

The basis for the current phase 2 proposals assume the entire system will be stateless. This means general clients or other nodes should be incentivized to provide state. The only state maintained within shards would be a state root at the end of each slot/block for each execution environment. Stateless systems can decrease complexity significantly in the process of shuffling validator nodes from shard to shard. This enables more security collectively across the system. Additionally, I/O requirements are significantly reduced and have acted as a bottleneck in computation/execution speed in the past. The theory around a stateless system suggests execution speed should increase significantly. Transactions would now have additional requirements. Each transaction would need to provide state data or witness data for the state it interacts/reads/edits. This can be verified/provided by including a merkle branch/proof in accordance with the shard execution environment’s current state root.

**Switchover**

Term to refer to the inevitable process of moving eth 1 into eth 2. There will need to be a community consensus on this switchover as current wallets, etc. interact with eth 1 as part of an eth 2 shard instead of the older POW chain.

**Witness Data**

As part of a stateless system, witness data provides the state data a transaction needs. One may sumarize it as providing each transaction with its own database. Any state a stransaction reads/writes from must be provided as part of the witness data. The witness data provides a Merkle proof in accordance with a state root to verify the state included is correct.

**Wasm-spawning-wasm**

In order to execute arbitrary user code \(e.g. smart contracts\) it is crucial for the node to provide functionality to execute wasm code blobs from inside an EE. This would likely mean that an executing wasm runtime would “spawn” a new wasm runtime to execute the user code. It may also provide the user code with additional host functions.

**Umbrella execution environment**

An umbrella execution environment takes advantage of wasm-spawning-wasm to allow users to deploy arbitrary code. It maintains the account structure and balance tracking to facilitate transactions to these user contracts.


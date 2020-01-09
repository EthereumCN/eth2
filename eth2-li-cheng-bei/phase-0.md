# Phase 0

#### 📌 关键词：PoS，信标链

[阶段0](https://github.com/ethereum/eth2.0-specs#phase-0)的主要任务是启动信标链 \(Beacon Chain\)。作为eth2的核心，信标链将为其自身和将来所有的分片链管理Casper权益证明协议，引导着eth2其他所有方面的发展。

正如[Ben Edgington](https://media.consensys.net/state-of-ethereum-protocol-2-the-beacon-chain-c6b6a9a69129)所提到的，该阶段的工作涉及许多方面，包括管理验证者及其押金、选择区块提议者、组织验证者进入委员会、对提议区块进行投票、应用共识规则、验证者的奖惩机制、促进跨分片交易等。

信标链上的主要负载来源将是“证明” \(attestations\)。证明是针对分片区块可用性的见证信息，同时也是信标区块的PoS见证信息。当一个分片区块取得了足够数量的证明，将创建一个“交联” \(crosslink\)，该“交联”可以确认将信标片段（到该分片区块为止）整合到信标链中。

阶段0将使用 Caspe FFG \(the Friendly Finality Gadget/友好的最终确定性小工具\) 来保障最终确定性 \(finality\)。简单来说，最终确定性意味着某项特定操作一旦完成，就将永远铭刻在历史中，并且无法还原。



#### 🔸 ETH2/BETH：信标链新ETH代币

阶段0将引入ETH2/BETH，成为供信标链验证者使用的新资产，主要有两种产生方式：

* 作为信标链的验证奖励分发（阶段1后还包括分片中的验证奖励）；
* 所有ETH1.x用户都通过[注册合约](https://github.com/ethereum/beacon_chain/blob/master/contracts/validator_registration.v.py)（registration contract）以1 ETH的价格购买，合约将其称作deposit。

需要清楚的是，阶段0不支持从信标链中撤回或转移ETH2，ETH1一经存入验证者注册合约后，将在以太坊1.0链中被销毁。信标链验证者会跟踪该合约，并向信标链提交存款信息，然后再由信标链将ETH2发放给存款人。

一旦阶段0激活，将存在两条以太坊区块链：Eth1链（PoW主链）和Eth2链（信标链/PoS链）。 信标链是eth2的基础，也是核心组件，能够起到管理验证者并且协调分片链的作用。



#### 🔸信标**节点和客户端**

Eth2区分了信标节点和验证者客户端，验证者需要这两者才能履行其职责。信标节点（即节点）负责维护整个信标链以及用户或验证者可能需要使用的任意分片。

顾名思义，验证者客户端（即客户端）负责处理的是单个验证者的逻辑。具体实现体现为通过与信标节点进行通信以了解信标链的当前状态，适时证明和提议区块，最后请求信标节点将区块信息发送给其他节点。

_**注：**如果没有运行验证者客户端，那么信标节点包含所有与eth2进行去信任交互所需的所有信息，这类似于eth1中的全节点。_

![](https://blog.ethereum.org/img/2019/11/carlimg1.png)

以下摘取了一些区分信标节点和验证者客户端的原因：

* 要成为验证者，首先需要抵押32个ETH，因此想要质押更多数量ETH的用户就需要运行多个验证者实例。将节点和客户端区分开使得这些用户在仅运行一个信标节点的情况下连接多个验证者客户端，从而减少了计算、内存和存储需求。
* 独立区分的验证者节点能够更容易编写、推理并审核较小的代码块，因此其安全性可能会更高。
* 对于担心出现冗余的用户来说，并行运行多个节点，降低了验证者离线的几率。
* 由于验证者客户端只能通过信标节点与eth2网络的其他部分进行交互，甚至到时还需要通过一个[受限的API](https://github.com/ethereum/eth2.0-APIs/blob/master/apis/validator/beacon-node-validator-api.md)，这样大大缩小了验证者节点的受攻击面。
* 如果希望与eth2进行交互但又不想成为验证者，用户只需运行一个信标节点，这将授予他们访问信标链和分片的权限。

## 延伸阅读

* [信标链规范](https://github.com/ethereum/eth2.0-specs/blob/master/specs/core/0_beacon-chain.md)
* [阶段0规范](https://github.com/ethereum/eth2.0-specs/releases)
* [Phase 0 for Humans](https://notes.ethereum.org/jDcuUp3-T8CeFTv0YpAsHw?view)
* [如何参与ETH2 Staking](https://blog.ethereum.org/2019/11/27/Validated-Staking-on-eth2-0/)


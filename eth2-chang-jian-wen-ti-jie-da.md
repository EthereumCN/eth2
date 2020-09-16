# Eth2常见问题解答

### **以太坊2.0是什么？**

以太坊2.0 \(Eth2/Serenity\) 是以太坊区块链的下一次重大更新升级，将于2020年开始分阶段推进，首先上线的是阶段0 \(Phase 0\)。每个阶段都将从不同方面对以太坊区块链的功能和性能进行优化。

推荐阅读：《详解以太坊2.0信标链》、Eth2术语库

### 以太坊1.0和以太坊2.0的区别是什么？

相对于以太坊1.0，以太坊2.0会带来**两大创新和改变**：Proof of Stake和分片链。

**Proof of Stake \(权益证明\)：**以太坊1.0所采用的共识机制是Proof of Work \(PoW, 工作量证明\)，主要依靠物理算力 \(矿工\) 和电力资源在区块链上构建区块。Proof of Stake \(PoS, 权益证明\) 则运作于验证者 \(validators, 虚拟矿工\) 和ETH存款的基础上，能够避免能源浪费，并且提升安全性和扩容性。

**分片链 \(Shard Chains\)：**分片链是一个扩容性机制，能够大幅提升以太坊区块链的吞吐量。以太坊1.0作为一条完整的区块链，其中区块连续排列，其优点在于安全性强且易于验证。但是每个全节点都需要处理并验证区块中的每笔交易，这就限制了交易的处理速度，尤其体现在主网交易活动频繁的时期。通过分片，以太坊区块链会被“切分”为64条独立的链，从而将处理数据的任务分配给大量节点，使得交易能够被并行处理，而不再是次序处理，这样就能实现吞吐量的大幅提升。以太坊2.0阶段1 \(Phase 1\) 计划实现分片机制。

_More information about Proof of Stake & Shard Chains:_ [_**What is Ethereum 2.0?**_](https://consensys.net/blog/blockchain-explained/what-is-ethereum-2/) _&_ [_**What is Proof of Stake?**_](https://consensys.net/blog/blockchain-explained/what-is-proof-of-stake/)

### 以太坊2.0的发展路线是什么？分为哪几个阶段？

以太坊2.0升级目前至少包含三个阶段，即阶段0、阶段1和阶段2。阶段0将于2020年发布，其他两个阶段将在接下来的几年内陆续发布。

**阶段0：**以太坊2.0的第一个阶段，目标是实现信标链 \(Beacon Chain\)。信标链负责存储和管理验证者的注册，还承担了为以太坊2.0实现Proof of Stake \(PoS, 权益证明\) 机制的任务。而原本的以太坊PoW链会与新的以太坊PoS链并行运作，以保障数据信息的连贯和延续。

**阶段1：**以太坊2.0的第二个阶段，预计会在2021推出。阶段1的主要目标是集成分片链。通过分片，以太坊区块链会被“切分”为64条独立的链，能够并行处理和存储交易信息。保守估计届时以太坊的吞吐量会提升64倍，但根据设计，分片后的以太坊理论上能够处理相较1.0数百倍的数据。

**阶段2：**以太坊2.0的第三个阶段，可能会在2021年或2022年发布。相较于前两个阶段，阶段2的定义暂时没有那么明晰，但计划中包含引入以太坊账户、转账提款、跨分片转账和合约调用以及执行环境，以支持在以太坊2.0中构建可扩容的应用。除此之外，还会将以太坊1.0链与2.0链进行合并，从而完全停止使用PoW机制。许多关于阶段2的研发仍在推进当中。

_More information about the Ethereum 2.0 roadmap:_ [_**A Short History of Ethereum**_](https://consensys.net/blog/blockchain-explained/a-short-history-of-ethereum/) _&_ [_**What is Ethereum 2.0?**_](https://consensys.net/blog/blockchain-explained/what-is-ethereum-2/)

### **以太坊2.0实现之后会带来什么改变？**

2.0升级会大大提升以太坊公共主网的**扩容性、吞吐量和安全性**。以太坊2.0不会抹去1.0链上的任何数据历史、交易记录以及资产所有权。信标链作为以太坊2.0的核心，将与现有的1.0链并行运行，以确保连贯性。关于Eth1和Eth2的区别，我们可以将其类比公路和高速公路。

_More information about the distinctions between 1.0 and 2.0:_ [_**What is Ethereum 2.0?**_](https://consensys.net/blog/blockchain-explained/what-is-ethereum-2/)

### **以太坊1.0链会发生什么？**

按照目前的计划，在阶段1中以太坊1.0链会成为以太坊2.0的首个分片。在那之前，以太坊1.0链会如常运行，同时还会经历一些升级，以便最终成功合并为以太坊2.0的分片。

_More information about the future of Ethereum’s current chain:_ [_**Eth1 to Eth 2 Transition Metaphor**_](https://twitter.com/JimmyRagosa/status/1189917753907535873?s=19)

### **以太坊2.0的上线日期？**

阶段0会在2020年实现，阶段1计划于2021年上线，阶段2及其之后阶段计划在2021年及之后推出。

_More information about the launch of Ethereum 2.0:_ [_**What is Ethereum 2.0?**_](https://consensys.net/blog/blockchain-explained/what-is-ethereum-2/)

### **以太坊的Proof of Stake \(权益证明\) 是什么？**

Proof of Stake \(PoS\) is an upgrade from Ethereum 1.0’s current Proof of Work consensus model and allows for improved security and scalability. PoS is a consensus mechanism that relies on validators and staked ETH for the continuation of blocks on the blockchain, and is necessary for sharding. Validators are people who elect to continue the blockchain by depositing \(or “staking”\) 32 ETH into the deposit contract. On a continuous basis, validators are randomly selected from the pool of all validators to be given the opportunity to create the next block. Should a validator successfully validate a block, they will receive an ETH reward. If a validator attempts to compromise the truthful continuation of the blockchain, their deposit will be ‘slashed’ – meaning they will lose some or all of their 32 staked ETH.

A Proof of Stake mechanism offers more crypto-economic security compared to the more abstract disincentive of losing the cost associated with electricity. Rather than investing in an enormous mining facility to defray the cost of electricity to mine blocks in PoW, staking on Ethereum 2.0 will only require a consumer laptop \(some software clients aim to be lightweight enough to run on a cell phone, thus reducing the barrier to entry to participating in the consensus process, consequently increasing the decentralization of the network\). Proof of Stake will go live in Phase 0 of Ethereum 2.0.

_More information about the launch of Ethereum 2.0:_ [_**What is Proof of Stake?**_](https://consensys.net/blog/blockchain-explained/what-is-proof-of-stake/) _&_ [_**The Proof of Stake FAQ**_](https://github.com/ethereum/wiki/wiki/Proof-of-Stake-FAQ)

### 我可以购买以太坊2.0中的ETH吗？

There is no way to buy Ethereum 2.0 ether, since there will not be a new type of ETH token. Instead, users will deposit ETH in the Ethereum 2.0 deposit contract. Right now, this is planned to be a one-way, non-reversible transaction.

There are two ways ETH holders can participate and earn rewards for staking on Ethereum 2.0. First, an ETH holder may run their own validator\(s\) by staking ETH in increments of 32 on the network. Running your own validator node means you have the responsibility to validate and organize blocks – not doing so could result in a penalty of ETH \(see “Staking Rewards” FAQ\). Another option for ETH holders is to stake their rewards through a staking provider or join a staking pool with smaller amounts of ETH, through which anyone can stake whatever small amount of ETH they are able to and still receive rewards proportional to their contribution.

_More information about staking on Ethereum 2.0:_ [_**What Happens to my ETH on Ethereum 2.0?**_](https://consensys.net/blog/blockchain-explained/what-happens-to-my-eth-on-ethereum-2/)

### 如何成为以太坊2.0中的验证者？

The switch from Proof of Work to Proof of Stake will create a unique revenue-generating capability for ETH holders. ETH holders can become validators on the Ethereum network and stake their ETH in order to receive rewards when they successfully validate and attest a new block.

One can become a validator on the Ethereum 2.0 network by depositing 32 ETH. This can be done in one of two ways. You can run your own validator node and stake the ETH yourself. The second option is to stake your ETH using a staking provider, a number of which will likely come to market in the weeks and months before the launch. There will be both custodial and non-custodial staking services offered.

_More information about becoming a validator on Ethereum 2.0:_ [_**What is Proof of Stake?**_](https://consensys.net/blog/blockchain-explained/what-is-proof-of-stake/)

### 在以太坊2.0中Staking如何获得奖励？

As a validator on Ethereum 2.0, you get rewarded for proposing and attesting the next block in the chain. You will receive rewards in ETH for making valid proposals and attestations.

Rewards are dynamically calculated based on the state of the network upon epoch completion. Network level reward issuance rates are a function of the total amount of ETH staked and average % online of validator\(s\). Individual validator reward rates depend on the number of validators run and % uptime of the validator.

Rewards minus penalties are transferred to validators every epoch \(384 seconds ~6.5 minutes\). As a result, the reward you expect to receive when being randomly selected to be a validator may be different than what a validator actually receives. Check out the [Ethereum 2.0 Calculator](https://docs.google.com/spreadsheets/d/15tmPOvOgi3wKxJw7KQJKoUe-uonbYR6HF7u83LR5Mj4/edit#gid=1548910165) for an idea of the types of rewards for staking on Ethereum 2.0.

_More information about rewards on Ethereum 2.0:_ [_**What is Proof of Stake?**_](https://consensys.net/blog/blockchain-explained/what-is-proof-of-stake/) _&_ [_**The Eth2 Calculator**_](https://docs.google.com/spreadsheets/d/15tmPOvOgi3wKxJw7KQJKoUe-uonbYR6HF7u83LR5Mj4/edit#gid=1548910165)

### 成为验证者和质押ETH的风险有哪些？

An upside to participating as a validator is that you can earn rewards of ETH. There is, however, a risk of losing funds through the ‘slashing’ of the ETH you staked on the network. With a small amount of care, this risk is negligible. The first way a validator might lose funds is by being offline and not performing its duties correctly. This incurs a relatively mild penalty: roughly the same as the reward you could have made. As long as you are currently participating for at least 50% of the time, you will not lose your stake. The other way a validator can lose funds is to publish contradictory information about the chain. In this case, the validator is slashed and ejected from the system. The amount slashed is between 1 ETH and the entire stake amount, depending on other factors. Being slashed is easy to protect against and ought never to happen unless a validator is deliberately acting maliciously.

_More information about risk incentives on Ethereum 2.0:_ [_**What is Proof of Stake?**_](https://consensys.net/blog/blockchain-explained/what-is-proof-of-stake/)

### 在信标连中我如何被选中提议或是证明新区块？

After you have registered your 32 ETH stake in the deposit contract and your validator has become active, it will be assigned duties from time to time by the Beacon Chain. Validators will be called on to attest to blocks on the Beacon Chain once every 6.4 minutes \(once per epoch\), and randomly selected from the whole validator set to propose blocks periodically. If there are 100,000 validators in total, your validator will be asked to propose a block about once every two weeks on average. This is all completely automatic and entirely handled by the validator software.

_More information about attesting blocks on the Beacon Chain:_ [_**What is Ethereum 2.0?**_](https://consensys.net/blog/blockchain-explained/what-is-ethereum-2/)

### 我现在所持有的ETH会怎么样？

There is no need to do anything special with the ETH you currently own. It continues to be fully usable on the Ethereum 1.0 chain. At some point, the Ethereum 1.0 chain will become part of Ethereum 2.0, and your ETH will continue to function just as it does now, with no action required on your part.

For those who want to participate in staking, you can choose to become a validator on the Ethereum 2.0 beacon chain by depositing your ETH into the validator deposit contract on the Ethereum 1.0 chain. It then becomes a validator balance on the Ethereum 2.0 beacon chain. This process is non-reversible. Transfers are disabled during Phase 0 so validators will have to wait until Phase 2 until withdraws to a specific shard are possible, at which point your ETH stake and the rewards accrued will be fully usable within Ethereum 2.0.

_More information about ETH:_ [_**What Happens to my ETH on Ethereum 2.0?**_](https://consensys.net/blog/blockchain-explained/what-happens-to-my-eth-on-ethereum-2/)

### 谁在开发以太坊2.0？

Hundreds of people! The work is largely led and coordinated by the Ethereum Foundation research team, but many other research and implementation teams are making substantial contributions. The main work is to collaborate on defining the specification for Ethereum 2.0, which is maintained on the[ Ethereum Foundation GitHub pages](https://github.com/ethereum/eth2.0-specs). Seven independent teams are building Ethereum 2.0 clients in a variety of different programming languages for different use cases and are constantly feeding back into the design and specifications.

_More information about the people behind Ethereum 2.0:_ [_**What’s New in Eth2**_](https://hackmd.io/@benjaminion/eth2_news)

### 以太坊区块链此前经历过哪些升级？

Ethereum has undergone four planned upgrades since its public mainnet launch in July 2015 \(called “Homestead”\). In order the four upgrades were: Homestead \(March 2016\), Metropolis Byzantium \(October 2017\), Metropolis Constantinople \(February 2019\), and Istanbul \(December 2019\). Together, these upgrades improved the functionality of the Ethereum 1.0 chain while setting the stage for Ethereum 2.0

_More information about the people behind Ethereum 2.0:_ [_**A Short History of Ethereum**_](https://consensys.net/blog/blockchain-explained/a-short-history-of-ethereum/)


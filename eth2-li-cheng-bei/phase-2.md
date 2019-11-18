# Phase 2

## 相关概念

ECN\(ethereum.cn\)会及时跟踪EF\(以太坊基金会\)在eth 2 阶段2\(phase 2\)的开发进度，相关讨论与阶段性形成的概念。

我们属于开源社区，这里需要你的支持！ 

\*\*\*\*

## 内容列表

* [Getting Started](https://hackmd.io/UzysWse1Th240HELswKqVA?view#Getting-Started)
* [Introducing Scout](https://hackmd.io/UzysWse1Th240HELswKqVA?view#Introducing-Scout)
* [Execution Environments](https://hackmd.io/UzysWse1Th240HELswKqVA?view#Execution-Environments)
* [Eth 1 -&gt; Eth 2 Switchover](https://hackmd.io/UzysWse1Th240HELswKqVA?view#Eth-1--gt-Eth-2-Switchover)
* [Cross Shard Transactions](https://hackmd.io/UzysWse1Th240HELswKqVA?view#Cross-Shard-Transactions)
  * [Asynchronous Cross Shard Transactions](https://hackmd.io/UzysWse1Th240HELswKqVA?view#Asynchronous-Cross-Shard-Transactions)
  * [Optimistic Asynchronous Cross Shard Transactions](https://hackmd.io/UzysWse1Th240HELswKqVA?view#Optimistic-Asynchronous-Cross-Shard-Transactions)
  * [Synchronous Cross Shard Transactions](https://hackmd.io/UzysWse1Th240HELswKqVA?view#Synchronous-Cross-Shard-Transfers)
* [Light Client Servers and Infrastructure](https://hackmd.io/UzysWse1Th240HELswKqVA?view#Light-Client-Servers-and-Infrastructure)
* [Fee Markets](https://hackmd.io/UzysWse1Th240HELswKqVA?view#Fee-Markets)
* [Open Questions](https://hackmd.io/UzysWse1Th240HELswKqVA?view#Open-Questions)
* [FAQ](https://hackmd.io/UzysWse1Th240HELswKqVA?view#FAQ)
* [Glossary of Terms](https://hackmd.io/UzysWse1Th240HELswKqVA?view#Glossary-of-Terms)
* [Jobs](https://hackmd.io/UzysWse1Th240HELswKqVA?view#Jobs)

### 从这里开始 <a id="Getting-Started"></a>

了解Vitalik Buterin关于EHT2的提案:  
[https://notes.ethereum.org/s/Bkoaj4xpN](https://notes.ethereum.org/s/Bkoaj4xpN) 

For an **introduction**, start here:

* Scaling Ethereum - [Phase 2 Overview](https://www.youtube.com/watch?v=RW7K3JQOZOg&t=73m35s)
* Scaling Ethereum - [Phase 2 Execution, Scout and History of Serenity](https://www.youtube.com/watch?v=RW7K3JQOZOg&t=104m33s)
* [A journey through Phase 2](https://medium.com/@william.j.villanueva/a-journey-through-phase-2-of-ethereum-2-0-c7a2397a36cb)
  * **Outdated points from article:**
    * Bitfield waking mechanism \(leave it to each execution environment\)
    * Beacon Chain Contracts currently called `Execution Environment`s \(EE\)s
    * Relayers or fee markets
* [Eth 2 Fee Market \(Relayers, State Providers, Mempool\)](https://ethresear.ch/t/state-providers-relayers-bring-back-the-mempool/5647)
* [Phase 2 Design Space](https://www.youtube.com/watch?v=RW7K3JQOZOg&t=34m50s)

### Introducing Scout <a id="Introducing-Scout"></a>

[https://github.com/ewasm/scout](https://github.com/ewasm/scout) \(Rust\)  
[https://webassembly.studio/?f=isz2bypxpy](https://webassembly.studio/?f=isz2bypxpy) \(Javascript + Typescript for writing EEs\) - This is in active development and not as mature as the Rust version above  
[https://ethresear.ch/t/phase-2-execution-prototyping-engine-ewasm-scout/5509](https://ethresear.ch/t/phase-2-execution-prototyping-engine-ewasm-scout/5509)

Scout is an eth 2 phase 2 execution prototyping engine. It currently supports reading and outputting shard/beacon states in a YAML format and will be expanded to a client tool.

**Goals**:

* Create a \(black boxed\) execution prototyping engine
* Create some example contracts \(“execution scripts”\)
* Formalize [runtime host functions](https://github.com/ewasm/scout/blob/ef9a11e83248e120ff830747fcbcadc29b62b868/src/main.rs#L64-L126) available to EEs
* Determine efficient method for executing arbitrary wasm code
* Ask other teams to create useful scripts
* By having actual real world use cases in scripts, we can benchmark the design \(such as stateless\) and identify bottlenecks

End of year goal to produce a full Eth 2 testnet \(phase 1 with execution\) integrated with scout and sample execution environments.

### Execution Environments <a id="Execution-Environments"></a>

A list of execution environments currently being prototyped:

* Simple in-shard ETH transfers as described in the [original proposal](https://notes.ethereum.org/s/Bkoaj4xpN)
* Generic Assets \(Token/ERC20\)
* Rollup verification
* Basic data checkin
* Intel SGX verifier

Longer term execution environments that need to be built:

* Eth 1 EE
* Eth 2 EE
* Delayed State Execution Framework

Suggested set of execution environments to build:

* ZEXE
* Plasma checkins across shards
* Libra/Bitcoin other chains?

Early suggestion on what an eth 2 EE may look like:  
[https://ethresear.ch/t/eth-execution-environment-proposal/5507](https://ethresear.ch/t/eth-execution-environment-proposal/5507)

### Eth 1 -&gt; Eth 2 Switchover <a id="Eth-1--gt-Eth-2-Switchover"></a>

Open questions on the exact mechanism, however the general consensus has been to have a community-led switchover to a shard on Eth 2. This switchover would require a hard fork on the Beacon Chain to bring the current funds into the Eth 1 execution environment as beacon eth. The hard fork would also need to provide the initial state root for the execution environment on the particular shard.

The eth 1 execution environment could also expand to be shard-aware. This would add additional abilities to how eth 1 currently operates.

The switchover would likely include writing the EVM in Ewasm and using it within the execution environment.

A good twitter discussion between Casey & Vitalik:  
[https://twitter.com/VitalikButerin/status/1134988921165758466](https://twitter.com/VitalikButerin/status/1134988921165758466)

Eth research post on open questions:  
[https://ethresear.ch/t/work-to-natively-integrate-eth1-into-eth2/5573](https://ethresear.ch/t/work-to-natively-integrate-eth1-into-eth2/5573)

### Cross Shard Transactions <a id="Cross-Shard-Transactions"></a>

Currently an open space/discussion. The general goal is to prepare an eth 2 testnet and then begin testing different models and assumptions.

#### Asynchronous Cross Shard Transactions <a id="Asynchronous-Cross-Shard-Transactions"></a>

Most discussions around the yanking/receipt model. Requires a crosslink on the Beacon Chain for finality \(~6 minutes\)

* [https://ethresear.ch/t/phase-2-pre-spec-cross-shard-mechanics/4970](https://ethresear.ch/t/phase-2-pre-spec-cross-shard-mechanics/4970)
* [https://ethresear.ch/t/cross-shard-contract-yanking/1450](https://ethresear.ch/t/cross-shard-contract-yanking/1450)

#### Optimistic Asynchronous Cross Shard Transactions <a id="Optimistic-Asynchronous-Cross-Shard-Transactions"></a>

These models create a framework around fork choice rules and how to reorg as a result. In these models, a cross shard transaction should have a latency of one slot or block \(~4 seconds\).

* [https://ethresear.ch/t/fast-cross-shard-transfers-via-optimistic-receipt-roots/5337/9](https://ethresear.ch/t/fast-cross-shard-transfers-via-optimistic-receipt-roots/5337/9)
* Scaling Ethereum Talk, Barry Whitehat - [Cross Shard Payments using Rollups](https://www.youtube.com/watch?v=RW7K3JQOZOg&t=178m25s)

#### Synchronous Cross Shard Transfers <a id="Synchronous-Cross-Shard-Transfers"></a>

Discussions around synchronous transfers generally involve a concept known as [delayed state execution](https://ethresear.ch/t/delayed-state-execution-in-practice/1041). This concept uses the main chain as an organization and ordering layer for transactions. A number of incentive games can be introduced to have a second layer of light clients responsible for executing the transactions on the current state. A [recent post](https://ethresear.ch/t/layer-2-state-schemes/5691/8) referred to some versions of delayed state execution as “State Schemes”

* [https://ethresear.ch/t/synchronous-cross-shard-transactions-with-consolidated-concurrency-control-and-consensus-or-how-i-rediscovered-chain-fibers/2318](https://ethresear.ch/t/synchronous-cross-shard-transactions-with-consolidated-concurrency-control-and-consensus-or-how-i-rediscovered-chain-fibers/2318)
* [https://ethresear.ch/t/simple-synchronous-cross-shard-transaction-protocol/3097](https://ethresear.ch/t/simple-synchronous-cross-shard-transaction-protocol/3097)
* Discussion around delayed execution models - [https://ethresear.ch/t/a-data-availability-blockchain-with-sub-linear-full-block-validation/5503](https://ethresear.ch/t/a-data-availability-blockchain-with-sub-linear-full-block-validation/5503)
* [https://ethresear.ch/t/various-kinds-of-scaling-execution-models-and-multi-chains/5488](https://ethresear.ch/t/various-kinds-of-scaling-execution-models-and-multi-chains/5488)
* [https://ethresear.ch/t/layer-2-state-schemes/5691/8](https://ethresear.ch/t/layer-2-state-schemes/5691/8)

### State Providers and Infrastructure <a id="State-Providers-and-Infrastructure"></a>

Scout efforts are currently benchmarking the viability/throughput and more regarding the stateless model for execution environments. Assuming the stateless model is used, proper infrastructure needs to be in place. For example, there needs to be a set of actors responsible for maintaining the current state and including witness data on behalf of transactions. Archival nodes or full nodes can also exist around various execution environments per shard to keep a historical picture of the state. All of these actors need further exploration.

Discussion around how to receive current state or add witness/state data to transactions has been [discussed by Vitalik](https://ethresear.ch/t/one-fee-market-ee-to-rule-them-all/5608/5). `Light client servers` are a natural candidate for providing this state data. Keep in mind, a light client server operates only on one shard. It does leave certain questions open:

* Do we have separate light client servers operate state on separate execution environments?
* How do we build a simple, quick runnable daemon to promote a distributed network vs. centralized set of servers?
* Unified state channel setup for users to discover and pay light client servers for their service?
* How do nodes combine packages from multiple users/providers? Some discussion on this has occured [here](https://ethresear.ch/t/state-providers-relayers-bring-back-the-mempool/5647).

### Fee Markets <a id="Fee-Markets"></a>

This discussion has evolved quite a bit. Originally, a relayer market was proposed. For a general background and understanding of the current proposal: [https://ethresear.ch/t/state-providers-relayers-bring-back-the-mempool/5647](https://ethresear.ch/t/state-providers-relayers-bring-back-the-mempool/5647).

Recent discussions have suggested an alternative approach \(eth research post coming soon\). It is a relayer market that allows any relayer to package your transactions and just requires the block producer to make one call to the fee market EE at the end of a block. This call transfers funds from the relayers to the block producer verifying that the hash of the transactions have included. This requires one major addition to the consensus layer - there needs to be a lookback mechanism. A lookback mechanism allows for an additional wasm host function that enables a transaction to read the hashes of transactions that came before it within the same block. This can allow for a simple way to pay relayers for the transaction hashes that have been included.

Specifics of the fee market \(similar to EIP 1559\) within the eth1 or eth2 EEs is an open topic and has not been explored. Additionally, `Light client server`s have been suggested as a mechanism for providing state data via state channels. It is important that the fee market construction works for well in the case of unique EE \(e.g. ZK-based EEs\). Some dicussions on the impact of a fee market and L2 schemes can be found [here](https://ethresear.ch/t/layer-2-state-schemes/5691).

### Open Questions <a id="Open-Questions"></a>

There are numerous open questions around implementation details, viability and throughput. Here are a general preliminary list of current open questions:

* Upgradability of execution environments without forking.
  * Some discussion around allowing contracts to “yank” themselves into a new execution environment. However, this assumes contracts are owned by a particular party and only updates contracts within an EE
* Execution Environment governance \(related to question above\)
* Fee for launching an execution environment
  * Separate charge for launch on each shard vs. launching the script on the Beacon Chain?
  * How much is appropriate to charge?
* Required supporting infrastructure for the fee market, state providers \(witness providers\), light client servers, etc…
* Throughput, viability of stateless model
* Support for synchronous calls between execution environments on the same shard
* Cross shard transactions, calls and further mechanics
* Specifics behind the Eth 1 execution environment
* Specifics behind a main Eth 2 execution environment that the community/EF supports
* Launch Phase 1 separately or hold off on launching phase 2 as part of phase 1 with primitive execution environments \(allow for a testground and later introduce the benchmarked/tested eth1/eth2 environments\)
* Mempool introduced as part of a validator node or other methods to share transactions

### FAQ <a id="FAQ"></a>

_What is the general timeline and roadmap for phase 2?_

It depends on dicussion within the community. For example, there is talk on having two main execution environments built. One is focused on eth1 and migrating the current contract state etc. over. The other is focused on being optimized for eth2, enabling contracts and funds to easily bridge over. This can provide more flexibility since it would not be constrained by the current eth 1 design. However, both these execution environments will need significant care, time, benchmarking and testing to complete. We project phase 2 will be ready to launch before these execution environments are completed. As a result, it is up to the needs of the community. Would it be helpful to have simple transfer, rollups, layer 2 checkins and other simpler execution environments launch first? Having an open system may be helpful before initiating the switchover or launching the eth 2/eth 1 execution environment.

_What about account abstraction and conversations regarding it?_

This is now delegated to the actual execution environment itself. The rules can be established on an execution environment basis.

### Glossary of Terms <a id="Glossary-of-Terms"></a>

**Delayed Execution**

Execution does not occur within the consensus or core protocol layer, but occurs within a 2nd layer market that allows for re-executions as more transactions or re-orgs are introduced. It assumes a separate class of light clients dedicated to execution. The main chain would only act as a mechanism for ordering and organizing transactions. This approach is commonly discussed as a solution for atomic or synchronous cross shard transactions. See Cross Shard transaction section above.

**Dynamic Host Function \(DHF\)**

Additional host functions that are dynamically linked into an execution evnvironment at runtime.

**Execution Environment \(EE\)**

A pure, reducing function deployed to the Beacon Chain. Execution that happens within the consensus layer on each shard will occur within the guidelines/framework of an execution environment. Essentially, an execution environment is the framework/set of rules that determine how the state transition can occur using Ewasm as the VM. An execution environment would also set the rules by with further Ewasm code can be executed under \(smart contracts an example\) within its system. It bounds/limits the way state can be stored and changed. See Getting Started resources to understand more.

**Execution Environment Shard State**

As described in Vitalik’s [proposal 2](https://notes.ethereum.org/s/Bkoaj4xpN), each shard contains a list of state roots that map to the execution environments defined on the Beacon Chain. Each execution environment maintains a state root on a shard. There are current questions on if the state root/capability appears on every shard or if payment is required to include it per each shard.

**Eth 1 EE**

The Eth 1 execution environment will define the rule/system for how current eth1 accounts, etc. will operate within eth 2. Current discussions state a shard will be dedicated to the eth 1 EE and additional rules will be introduced to allow cross shard transactions and interactions. The idea is to eliminate interruptions in current ethereum accounts and transactions as a switchover occurs.

**Ethereum Environment Interface \(EEI\)**

The EEI is a set of DHFs that provide the executing EE, and its children, Ethereum-specific functionality, such as retrieving the current block number, calling contracts, deterining the transaction sender, etc.

**Eth 2 EE**

Eth 2 opens up significantly more possiblities and constraining those to stay compatible with the current ethereum 1 EVM, rules, and contracts should be reduced. As a result, there is discussion around introducing a more expanded eth 2 EE which can easily bridge from the eth 1 EE.

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

#### 英语文档来源：[ETH 2 Phase 2 WIKI](https://hackmd.io/UzysWse1Th240HELswKqVA?view)，我们是及时更新。


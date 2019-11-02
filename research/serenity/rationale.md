# Serenity设计理念

## Serenity Design Rationale <a id="Serenity-Design-Rationale"></a>

See also: the 1.0 design rationale doc from 3-4 years ago [https://github.com/ethereum/wiki/wiki/Design-Rationale](https://github.com/ethereum/wiki/wiki/Design-Rationale)

[Serenity Design Rationale](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Serenity-Design-Rationale)[Principles](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Principles)[The Layer 1 vs Layer 2 Tradeoff](https://notes.ethereum.org/@vbuterin/rkhCgQteN#The-Layer-1-vs-Layer-2-Tradeoff)[Why proof of stake](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Why-proof-of-stake)[Why Casper](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Why-Casper)[Slashing](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Slashing)[Choice of consensus algorithm](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Choice-of-consensus-algorithm)[Sharding - or, why do we hate supernodes?](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Sharding---or-why-do-we-hate-supernodes)[Security models](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Security-models)[Why are the Casper incentives set the way they are?](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Why-are-the-Casper-incentives-set-the-way-they-are)[Base rewards](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Base-rewards)[Inactivity leak](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Inactivity-leak)[Slashing and anti-correlation penalties](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Slashing-and-anti-correlation-penalties)[BLS Signatures](https://notes.ethereum.org/@vbuterin/rkhCgQteN#BLS-Signatures)[Why 32 ETH validator sizes?](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Why-32-ETH-validator-sizes)[Random sampling](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Random-sampling)[Seed selection](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Seed-selection)[Shuffling](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Shuffling)[Crosslink committees](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Crosslink-committees)[Persistent committees](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Persistent-committees)[LMD GHOST fork choice rule](https://notes.ethereum.org/@vbuterin/rkhCgQteN#LMD-GHOST-fork-choice-rule)[Beacon chain / shard chain structure](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Beacon-chain--shard-chain-structure)[Shard chain design](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Shard-chain-design)[Crosslink data](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Crosslink-data)[The proof of custody game](https://notes.ethereum.org/@vbuterin/rkhCgQteN#The-proof-of-custody-game)[SSZ](https://notes.ethereum.org/@vbuterin/rkhCgQteN#SSZ)[Generalized indices](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Generalized-indices)[The validator lifecycle](https://notes.ethereum.org/@vbuterin/rkhCgQteN#The-validator-lifecycle)[Depositing](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Depositing)[Activation](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Activation)[Exiting](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Exiting)[Withdrawal](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Withdrawal)[Effective balances](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Effective-balances)[Fork mechanism](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Fork-mechanism)

### Principles <a id="Principles"></a>

* **Simplicity**: especially since cryptoeconomic proof of stake and quadratic sharding are inherently complex, the protocol should strive for maximum simplicity in its decisions as much as possible. This is important because it \(i\) minimizes development costs, \(ii\) reduces risk of unforeseen security issues, and \(iii\) allows protocol designers to more easily convince users that parameter choices are legitimate. See [https://radicalxchange.org/blog/posts/2018-11-26-4m9b8b/](https://radicalxchange.org/blog/posts/2018-11-26-4m9b8b/) for some philosophical background on \(iii\) specifically. When complexity is unavoidable to achieve a given level of functionality, the preference order for where the complexity goes is: layer 2 protocols &gt; client implementations &gt; protocol spec.
* **Long-term stability**: the low levels of the protocol should ideally be built so that there is no need to change them for a decade or longer, and any needed innovation can happen on higher levels \(client implementations or layer 2 protocols\).
* **Sufficiency**: it should be fundamentally possible to build as many classes of applications as possible on top of the protocol.
* **Defense in depth**: the protocol should continue to work as well as possible under a variety of possible security assumptions \(eg. regarding network latency, fault count, the motivations of users\)
* **Full light-client verifiability**: given some assumptions \(eg. network latency, bounds on attacker budget, 1-of-N or few-of-N honest minority\), a client verifying O© data \(ideally just the beacon chain\) should be able to gain indirect assurance that all of the data in the full system is available and valid, even under a 51% attack \(note: this is a subset of the “defense in depth” desideratum\)

### The Layer 1 vs Layer 2 Tradeoff <a id="The-Layer-1-vs-Layer-2-Tradeoff"></a>

See also: [https://vitalik.ca/general/2018/08/26/layer\_1.html](https://vitalik.ca/general/2018/08/26/layer_1.html) and [https://vitalik.ca/general/2019/06/12/plasma\_vs\_sharding.html](https://vitalik.ca/general/2019/06/12/plasma_vs_sharding.html)

There is a tradeoff in any blockchain protocol design between introducing more features at layer 1 \(ie. at consensus layer\) versus building a more simplified protocol and allowing those features to be built at layer 2 \(ie. as applications on top\).

Arguments in favor of layer 2 include:

* Reduced complexity of the consensus layer \(see **simplicity** [above](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Principles)\)
* Reduced need to modify the consensus layer \(see **long-term stability** [above](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Principles)\)
  * Reduced consensus failure risks
  * Reduced load on protocol governance and political risk
* More flexibility and ability to implement new ideas over time

Arguments in favor of layer 1 include:

* Reduced risk of stalled progress due to lack of mechanism to force everyone to upgrade to a new protocol \(the hard fork\)
* Possibly reduced complexity of the total system
* If layer 1 is not _powerful enough_, then it’s simply not possible to build layer 2 systems on top of it with desired properties \(eg. consider building ethereum on top of bitcoin without relying on a centralized or federated trust model\) \(see **sufficiency** [above](https://notes.ethereum.org/@vbuterin/rkhCgQteN#Principles)\)

Large parts of ethereum 2.0 are an effort to carefully balance between the two. The inclusion of **\(i\)** quasi-Turing-complete and richly-stateful code execution, **\(ii\)** scalable \[data availability\] and computation and **\(iii\)** fast block times are necessary for sufficiency, as:

* **Without \(i\)** one cannot build layer-2 applications with robust trust models
* **Without \(ii\)** scalability is limited to channel and Plasma-like techniques which have challenges generalizing as well as capital lockup and/or mass-exit issues
* **Without \(iii\)** one cannot have fast transactions without using channels, which have challenges generalizing as well as capital lockup and/or mass-exit issues

But there are other features that ethereum 2.0 deliberately leaves to layer 2: \(i\) privacy, \(ii\) high-level programming languages, \(iii\) scalable state storage, \(iv\) signature schemes. These are left to layer 2 because they are all areas of rapid innovation with many schemes existing that have different properties and inevitable tradeoffs with the possibility of better newer schemes. For example:

* **Privacy**: ring-signatures + confidential-values vs ZK-SNARKs vs ZK-STARKs; rollup vs ZEXE vs…
* **High-level programming languages**: declarative vs imperative, syntax, formal verification features, type systems, protective features \(eg. banning using impure functions inside arithmetic expressions\), native support for privacy features…
* **Scalable state storage**: accounts vs UTXOs, different rent schemes, raw Merkle branch witnesses vs SNARK/STARK compression vs RSA accumulators, sparse Merkle trees vs AVL trees vs usage-based imbalanced trees… \(and in addition to this, different schemes for _validating_ state transitions\)
* **Signature schemes**: M of N multisig, social key revocation/recovery, Schnorr sigs, BLS sigs, Lamport sigs…

### Why proof of stake <a id="Why-proof-of-stake"></a>

See:

* [https://github.com/ethereum/wiki/wiki/Proof-of-Stake-FAQ](https://github.com/ethereum/wiki/wiki/Proof-of-Stake-FAQ)
* [https://medium.com/@VitalikButerin/a-proof-of-stake-design-philosophy-506585978d51](https://medium.com/@VitalikButerin/a-proof-of-stake-design-philosophy-506585978d51)

### Why Casper <a id="Why-Casper"></a>

There are currently three major schools of proof of stake consensus algorithm:

* **Nakamoto-inspired** \(Peercoin, NXT, Ouroboros…\)
* **PBFT-inspired** \(Tendermint, Casper FFG, Hotstuff…\)
* **CBC Casper** \(descriptions [here](https://vitalik.ca/general/2018/12/05/cbc_casper.html) and [here](https://medium.com/@aditya.asgaonkar/casper-cbc-simplified-2370922f9aa6); classification of [Avalanche](https://hackernoon.com/avalanche-ava-blockchain-3-0-a-novel-metastable-consensus-protocol-28cdc4ee8984) is controversial but [there’s arguments](https://ethresear.ch/t/casper-cbc-lite-via-committees/3916) that it fits in here\)

Within the latter two camps, there is also the question of whether and how to use security deposits and slashing \(Nakamoto-inspired algorithms are incompatible with non-trivial slashing\). All three are superior to proof of work, but we want to defend our own approach.

#### Slashing <a id="Slashing"></a>

Ethereum 2.0 uses a **slashing** mechanism where a validator that is detected to have misbehaved can be penalized, in the best case ~1% but in the worst case up to its entire deposit.

We defend our use of slashing as follows:

1. **Raising the cost of attack**: We want to be able to make a hard claim that a 51% attack on a proof of stake blockchain forces the attacker to incur a very large amount of expense \(think: hundreds of millions of dollars worth of coins\) that get burned, and any attack can be recovered from quickly. This makes the attack/defense calculus very unfavorable for attackers, and in fact makes attacks potentially _counterproductive_, because the disruption to service is outweighed by price gains to legitimate coin holders.
2. **Overcoming the validator’s dilemma**: the most realistic immediate way for nodes to start to deviate from “honest” behavior is _laziness_ \(ie. not validating things that one should be validating, signing everything just in case, etc\). See [the validator’s dilemma paper](https://eprint.iacr.org/2015/702.pdf) for theoretical reasoning and [the Bitcoin SPV mining fork](https://bitcoin.stackexchange.com/questions/38437/what-is-spv-mining-and-how-did-it-inadvertently-cause-the-fork-after-bip66-wa) for examples of this happening and leading to very harmful consequences in the wild. Having very large penalties for self-contradicting or for signing incorrect things helps to alleviate this.

A more subtle instance of \(2\) can be seen as follows. In July 2019 [a validator on Cosmos was slashed](https://twitter.com/VitalikButerin/status/1145576103089602560) for signing two conflicting blocks. An investigation revealed that this happened because that validator was running a primary and a backup node \(to ensure that one of the two going offline would not prevent them from getting rewards\) and the two were accidentally turned on at the same time, leading to them contradicting each other.

If it became standard practice to have a primary and backup node, then an attacker could partition the network and get the primaries and the backups of all the validators to commit to different blocks, and thereby lead to two conflicting blocks being finalized. Slashing penalties help to heavily disincentivize this practice, reducing the risk of such a scenario taking place.

#### Choice of consensus algorithm <a id="Choice-of-consensus-algorithm"></a>

Only the BFT-inspired and CBC schools of consensus algorithm have a notion of finality, where a block is confirmed in such a way that a large portion \(1/3 in BFT-inspired, 1/4 in CBC\) of validators would need to misbehave and get slashed for that block to get reverted in favor of some conflicting block; Nakamoto-inspired \(ie. longest-chain-rule\) consensus algorithms have no way of achieving finality in this sense.

Note that finality requires a \(super\)majority of validators being online, but this is a requirement of the sharding mechanism already, as it requires 2/3 of a randomly sampled committee of validators to sign off on a crosslink for that crosslink to be accepted.

Our choice of [Casper FFG](https://arxiv.org/abs/1710.09437) was simply a matter of it being the simplest algorithm available at the time that part of the protocol was being finalized. We are [actively exploring](https://github.com/ethereum/eth2.0-specs/issues/701) a switch to CBC Casper in phase 3.

### Sharding - or, why do we hate supernodes? <a id="Sharding---or-why-do-we-hate-supernodes"></a>

The main alternative to sharding for layer-1 scaling is the use of supernodes - simply requiring every consensus node to have a powerful server so that it can individually process every transaction. Supernode-based scaling is convenient because it is simple to implement: it works just the same way blockchains do now, except that a little more software-engineering work is required to build things in a way that is more parallelizable.

Our main objections to this approach are as follows:

* **Pool centralization risk**: in a supernode-based system, running a node has a high fixed cost, so far fewer users can participate. This is usually rebutted with “well consensus in most PoW and PoS coins is dominated by 5-20 pools anyway, and the pools will be able to run nodes just fine”. However, this ignores the risk of centralization pressure even between pools that can afford it. If the fixed cost of running a validator is significant relative to the returns, then larger pools will be able to offer smaller fees than smaller ones \(eg. see [concern about this in Cosmos](https://twitter.com/maigoh91/status/1107276971715645441)\) and this could lead to smaller pools being pushed out or feeling pressure to merge. In a sharded system, on the other hand, validators with more ETH need to verify more transactions, so costs are not fixed.
* **AWS centralization risk**: in a supernode-based system, home staking is infeasible and so it’s more likely that most staking will happen inside cloud computing environments. This creates a single point of failure.
* **Reduced censorship resistance**: making it impossible to participate in consensus without high computation+bandwidth requirements makes detection and censorship of validators easier.
* **Scalability**: as transaction throughput increases, in a supernode-based system the above risks increase, whereas sharded systems can more easily handle the increased load.

These centralization risks are also why we are NOT attempting to achieve super-low-latency \(&lt;1s\) of the blockchain, instead opting for \(relatively!\) conservative numbers.

In the eth2 sharded system, it’s possible to participate with as little or as much ETH and as little or as much computing power as you have \(though you need the same amount of both; you cannot stake a large amount of ETH with very little computing power or vice versa\), and fixed costs are minimized, though at very high levels of ETH costs are still sublinear \(once you have &gt;32,768 ETH then you’re verifying most of the shards most of the time anyway, so additional technical costs from having even more ETH above that are low\)

### Security models <a id="Security-models"></a>

It’s commonly assumed that blockchains depend on an “honest majority” assumption for their security: that &gt;=50% of participants will faithfully follow a prescribed protocol, even forgoing opportunities to defect for their own personal interest. In reality, \(i\) an honest majority model is unrealistic, with participants being “lazy” and signing off on blocks without validating them \(see [the validator’s dilemma paper](https://eprint.iacr.org/2015/702.pdf) and [the Bitcoin SPV mining fork](https://bitcoin.stackexchange.com/questions/38437/what-is-spv-mining-and-how-did-it-inadvertently-cause-the-fork-after-bip66-wa)\) being a very common form of defection, but fortunately \(ii\) blockchains maintain many or all of their security properties under models that assume _much_ less of their fellow man than honest majority models.

A common harsher model is the _uncoordinated rational majority_ model, which states that participants act in their own self-interest, but no more than some percentage \(eg. [23.21% in simple PoW chains](https://arxiv.org/abs/1507.06183)\) are cooperating with each other. An even harsher model is the worst-case model where there is a single actor that controls more than 50% of hashpower or stake, and the question becomes:

* Can we, even under that scenario, force the attacker to have to pay a very high cost to break the chain’s guarantees?
* What guarantees can we unconditionally preserve?

Slashing in proof of stake chains accomplishes the first objective. In non-sharded chains, every node verifying every block accomplishes te second objective for two specific guarantees: \(i\) that the longest chain is valid, and \(ii\) that the longest chain is _available_ \(see [here](https://github.com/ethereum/research/wiki/A-note-on-data-availability-and-erasure-coding) for philosophical arguments on the significance of “data availability”\).

Our defense-in-depth approach with sharding is to combine together random committee sampling to achieve validity and availability guarantees under an honest majority model, with proof of custody to protect against lazy actors, and [fraud proofs and data availability proofs](https://arxiv.org/abs/1809.09044) to allow detection of invalid or unavailable chains without downloading and verifying all of the data; this allows clients to reject invalid or unavailable chains even if they are supported by a majority of all proof of stake validators.

Censorship of transactions can potentially be detected by clients in a consensus-preserving way \(see [https://ethresear.ch/t/censorship-detectors-via-99-fault-tolerant-consensus/2878](https://ethresear.ch/t/censorship-detectors-via-99-fault-tolerant-consensus/2878)\), but this research has not yet been incorporated into the ethereum roadmap.

Here is the current expected security properties expressed in a table:

|  | Network delay &lt;3s | Network delay 3s - 6 min | Network delay &gt; 6 min |
| :--- | :--- | :--- | :--- |
| &gt;2/3 validators honest | Perfect operation | Imperfect but acceptable operation. No rigorous proof of liveness, but liveness expected in practice. | Likely intermittent liveness failures, no safety failures |
| &gt;2/3 validators rational, &lt;1/3 coordinated | Perfect operation | Imperfect but acceptable operation, heightened centralization risk | Likely intermittent liveness failures, no safety failures, very high centralization risk |
| 51% attacker | Can revert finality or censor, but at high cost; cannot force through invalid or unavailable chains | Can revert finality or censor, but at high cost; cannot force through invalid or unavailable chains | Can revert finality or censor or force through invalid or unavailable chains |

### Why are the Casper incentives set the way they are? <a id="Why-are-the-Casper-incentives-set-the-way-they-are"></a>

#### Base rewards <a id="Base-rewards"></a>

During each epoch, every validator is expected to make an “attestation”, a signature that expresses that validator’s opinion on what the head of the chain is. There is a reward for having one’s attestation included, with five components:

1. Reward for the attestation getting included at all
2. Reward for the attestation specifying the correct epoch checkpoint
3. Reward for the attestation specifying the correct chain head
4. Reward for the attestation being included quickly on chain \(full if included after 1 slot, 1/n of the full reward if after n slots\)
5. Reward for the attestation specifying the correct shard block

In each case, the actual reward is computed as follows. If BB is the base reward \(see below\), and PP is the portion of validators that did the desired action, then any validator that performed the desired action gets a reward of B∗PB∗P, and any validator that did not gets a penalty −B−B. The purpose of this “collective reward” scheme where “if anyone performs better, everyone performs better” is to bound griefing factors \(see [https://github.com/ethereum/research/raw/master/papers/discouragement/discouragement.pdf](https://github.com/ethereum/research/raw/master/papers/discouragement/discouragement.pdf) for one description of griefing factors and why they are important\).

Note that case \(4\) is an exception; there the reward depends only on the delay, not on the behavior of other validators, and there is no risk of penalty.

The base reward BB is itself calculated as k∗Di∑nj=1Dj√k∗Di∑j=1nDj where D1...DnD1...Dn are deposit sizes and kk is a constant; this is a halfway compromise between two common models, \(i\) fixed reward rate, ie. k∗Dik∗Di, and \(ii\) fixed total reward, ie. k∗Di∑nj=1Djk∗Di∑j=1nDj.

The main argument against \(i\) is that it imposes too much uncertainty on the network of two kinds: uncertainty of the total level of issuance, and uncertainty of the total level of deposits \(as if a fixed reward rate is set too low then almost no one will participate, threatening the network, and if a rate is set too high then very many validators will participate, leading to unexpectedly high issuance\). The main argument against \(ii\) is greater vulnerability to discouragement attacks, see [https://github.com/ethereum/research/raw/master/papers/discouragement/discouragement.pdf](https://github.com/ethereum/research/raw/master/papers/discouragement/discouragement.pdf). The inverse-square-root approach compromises between the two and avoids the worst consequences of each one.

The proposer gets 1/8 of a base reward for including an attestation. This is to encourage proposers to listen well for messages and accept as many as possible.

**Break-even uptime**

Assuming there are two kinds of validators, \(i\) fully functioning online validators, and \(ii\) offline validators, with portion PP in category 1, then a validator’s expected reward will be: B∗4PB∗4P for cases \(1, 2, 3, 5\) above plus 78∗B∗\(P+P∗\(1−P\)2+P∗\(1−P\)23+...\)78∗B∗\(P+P∗\(1−P\)2+P∗\(1−P\)23+...\) for case \(4\) \(due to the possibility inclusion will be delayed by absent validators\) plus 18∗B∗P18∗B∗P for proposer rewards. Being absent has a penalty of B∗4B∗4. Hence, if everyone else is online, a validator earns B∗5B∗5 when online and loses B∗4B∗4 when offline, so they are breakeven if they stay online ≥44+5≈44.44%≥44+5≈44.44% of the time. If P=23P=23, then a validator earns ≈B∗\(23∗4.125+78∗0.81\)≈B∗3.46≈B∗\(23∗4.125+78∗0.81\)≈B∗3.46 when online, so they are breakeven if they stay online ≥53.6%≥53.6% of the time. If PP falls below 2323, however, the inactivity leak will quickly disincentivize being offline.

#### Inactivity leak <a id="Inactivity-leak"></a>

If the chain fails to finalize for tsf&gt;4tsf&gt;4 epochs \(tsftsf = “time since finality”\), then a penalty is added so that the maximum possible reward is zero \(validators performing imperfectly get penalized\), and a second penalty component is added, proportional to tsftsf. This ensures that if more than 1/3 of validators drop off, validators that are not online get penalized much more heavily, and the penalty increases quadratically over time.

This has three consequences:

* Penalizes being offline much more heavily in the case where you being offline is actually preventing blocks from being finalized
* Serves the goals of being an anti-correlation penalty \(see section below\)
* Ensures that if more than 1/3 do go offline, eventually the portion online goes back up to 2/3 because of the declining deposits of the offline validators

With the current parametrization, if blocks stop being finalized, validators lose 1% of their deposits after 2.6 days, 10% after 8.4 days, and 50% after 21 days. This means for example that if 50% of validators drop offline, blocks will start finalizing again after 21 days.

#### Slashing and anti-correlation penalties <a id="Slashing-and-anti-correlation-penalties"></a>

If a validator is caught violating the Casper FFG slashing condition, they get penalized a portion of their deposit equal to three times the portion of validators that were penalized around the same time as them \(specifically, between 18 days before they were penalized and roughly the time they withdrew\). This is motivated by several goals:

* A validator misbehaving is only really bad for the network if they misbehave at the same time as many other validators, so it makes sense to punish them more in that case
* It heavily penalizes actual attacks, but applies very light penalties to single isolated failures that are likely to be honest mistakes
* It ensures that smaller validators take on less risk than larger validators \(as in the normal case, a large validator would be the only one failing at the same time as themselves\)
* It creates a disincentive against everyone joining the largest pool

### BLS Signatures <a id="BLS-Signatures"></a>

BLS signatures are used because of their aggregation-friendliness: any two signatures S1S1 and S2S2 of a message MM signed by keys k1k1 and k2k2 \(corresponding pubkeys K1=G∗k1K1=G∗k1 and K2=G∗k2K2=G∗k2 where GG is the generator of the elliptic curve\) can simply be aggregated by elliptic curve point addition: S1+S2S1+S2, which verifies against the public key K1+K2K1+K2. This allows many thousands of signatures to be aggregated, with the marginal cost of one signature being one bit of data \(to express that a particular public key is present in the aggregate signature\) and one elliptic curve addition for computation.

Note that BLS signatures of this form are vulnerable to _rogue key attacks_: if you see that other validators have already published public keys K1...KnK1...Kn, then you can generate a private key rr and publish a public key G∗r−K1−...−KnG∗r−K1−...−Kn. The aggregate public key would simply be G∗rG∗r, so you would be able to make a signature that verifies against the combined public key by yourself. The standard way to get around this is to require a _proof of possession_: basically, a signature of a message \(that depends on the public key, and that would normally not be signed\) that verifies against the public key by itself \(ie. sign\(message=H′\(K\),key=k\)sign\(message=H′\(K\),key=k\) for privkey kk and pubkey KK, where H′H′ is a hash function\). This ensures that you personally control the private key connected to the public key that you publish.

We use the signature of a deposit message \(which specifies the signing key but also other important data such as the withdrawal key\) as a proof of possession.

### Why 32 ETH validator sizes? <a id="Why-32-ETH-validator-sizes"></a>

Any BFT consensus algorithm with accountable fault tolerance \(ie. if two conflicting blocks get finalized you can identify which 1/3 of nodes were responsible\) must have all validators participate, and furthermore for technical reasons you need two rounds of every validator participating to finalize a message.

This leads to the [decentralization / finality time / overhead tradeoff](https://medium.com/@VitalikButerin/parametrizing-casper-the-decentralization-finality-time-overhead-tradeoff-3f2011672735): if nn is the number of validators in a network, ff is the time to finalize a block, and ωω is the overhead in messages per second, then we have:

ω≥2∗nfω≥2∗nf

For example, if we are ok with an overhead of 10 messages per second, then a 10000-node network could only have a finality time of at least 2000 seconds \(~33 minutes\).

In Ethereum’s case, if we assume a total ETH supply of ≈227≈227 ETH, then with 32 ETH deposit sizes, there are at most 222222 validators \(and that’s if everyone validates; in general we expect ~10x less ETH validating\). With a finality time of 2 epochs \(2 \* 64 \* 6 = 768 seconds\), that implies a max overhead of 222768≈5461222768≈5461 messages per second. We can tolerate such high overhead due to BLS aggregation reducing the marginal size of each signature to 1 bit and the marginal verification complexity to one elliptic curve addition.

64 slots is a safe minimum for another reason: if an attacker manipulates the randomness used for proposer selection, this number still provides enough space to ensure that there will be at least one honest proposer in each epoch, which is sufficient to ensure blocks keep finalizing. Our calculations suggest that current levels of overhead are acceptable, but higher levels would make running a node too difficult. Finally, the validator deposit size is ideal for shard crosslinking \(see below\).

### Random sampling <a id="Random-sampling"></a>

#### Seed selection <a id="Seed-selection"></a>

The seed used for randomness is updated every block by “mixing in” \(ie. `seed <- hash(seed, new_data)`\) a value that must be revealed by the proposer of the block. Just like proof of custody subkeys, a validator’s values are all pre-determined once the validator has deposited, third parties cannot compute subkeys but can verify subkeys that are revealed voluntarily \(this mechanism is sometimes called RANDAO\).

This ensures that each proposer has one “bit of manipulation” over the seed: they can either make a block or not make a block. Not making a block is expensive in that the proposer misses out on many rewards. Furthermore, because the persistent and crosslink committee sizes \(see below\) are large, manipulation of the randomness almost certainly cannot allow minority attackers to get 2/3 of any committee.

In the future we plan to use verifiable delay functions \(VDFs\) to further increase the random seeds’ robustness against manipulation.

#### Shuffling <a id="Shuffling"></a>

We use the swap-or-not shuffle from [https://link.springer.com/content/pdf/10.1007%2F978-3-642-32009-5\_1.pdf](https://link.springer.com/content/pdf/10.1007%2F978-3-642-32009-5_1.pdf) to shuffle the validator set and assign responsibilities every epoch. This algorithm ensures that:

* As the shuffle is a permutation, each validator is assigned to be a member of exactly one crosslink committee during each epoch \(keeping their load stable and reducing the chance manipulation of randomness can be profitable\)
* As the shuffle is a permutation, each validator is assigned to be a member of exactly one persistent committee during each epoch
* As the shuffle is pointwise-evaluable in the forward direction, a validator can determine their own responsibilities in O\(1\) time
* As the shuffle is pointwise-evaluable in the reverse direction, the members of any specific committee or the proposer of any specific block can be computed in O\(1\) time

#### Crosslink committees <a id="Crosslink-committees"></a>

In each epoch, a crosslink is created for each shard; this means that 2/3 of a randomly selected pool \(“committee”\) of ~128 validators signs a hash that represents all data that was included in that shard since the most recent crosslink, up to a maximum of 64 epochs’ worth of data \(so if there are many failed crosslinks in a row, it could take multiple successful crosslinks to catch up\). 128 is chosen because it’s the minimum size which is reasonably safe against attackers with less than 1/3 of the total validator set getting 2/3 of the committee by random chance \(by binomial theorem, the probability is 5.55∗10−155.55∗10−15\).

Because there are 1024 shards, this means that to get one crosslink per epoch we need 131072 validators, or ~4.4m ETH staking \(in practice, if less ETH than this is staking, crosslinks happen more rarely\). Increasing the minimum deposit size eg. to 1024 ETH would mean that we cannot get enough validators to make crosslinks on every shard in every epoch unless literally all ETH is staking.

The purpose of rapid reshuffling is to ensure that an attacker would need to corrupt any single committee very quickly to be able to launch an attack against any single shard.

#### Persistent committees <a id="Persistent-committees"></a>

During each ~27-hour period, a persistent committee is chosen for each shard. Each validator is a member of one persistent committee at any time. Persistent committees are responsible for proposing shard blocks, providing users with some level of guarantee about shard blocks until they are included in a crosslink, and light clients can piggyback off of persistent committees. To preserve P2P network stability and to preserve efficiency of light clients, persistent committees are changed relatively infrequently. Persistent committees are capped to 128, so if more than 131072 validators are present any given validator will sometimes not be selected for any shard; this reduces needless wasted validation.

To further preserve network stability, not all validators are rotated from their period nn persistent committee to their period n+1n+1 persistent committee at the same time; instead, each validator’s rotation is delayed until a random point in time during the next period.

### LMD GHOST fork choice rule <a id="LMD-GHOST-fork-choice-rule"></a>

The beacon chain uses an LMD GHOST fork choice rule, described here: [https://github.com/ethereum/eth2.0-specs/blob/master/specs/core/0\_fork-choice.md](https://github.com/ethereum/eth2.0-specs/blob/master/specs/core/0_fork-choice.md)

The LMD GHOST fork choice rule incorporates information from all validators, hundreds in each slot, making it extremely unlikely in the normal case that even a single block will be reverted. Because the fork choice is dependent on all validators, this also ensures that blocks cannot be reverted unless an attacker really does control close to 50% of the entire validator set; one cannot achieve a large advantage by manipulating the randomness.

### Beacon chain / shard chain structure <a id="Beacon-chain--shard-chain-structure"></a>

The structure of the sharded system features a central “beacon chain” that coordinates all activity, and a chain for each of 1024 shards. The shards are periodically linked into the becon chain via “crosslinks”.

Possible alternatives to this are:

1. Putting _all_ blocks of shards directly into the beacon chain with committees signing off on them
2. Not having a beacon chain, and connecting shard chains to each other in some other structure

\(1\) was rejected for efficiency reasons: it’s desirable to have a block time on shards of 6 seconds, but having 1024 crosslinks per 6 seconds in the beacon chain would incur an unacceptably high load on the beacon chain.

\(2\) was rejected for simplicity reasons: the hub-and-spoke beacon chain structure with a hierarchical fork choice \(find the beacon head first, then based on the beacon chain compute which shard blocks are eligible and hence the head of the shard chains\) is simpler to implement and reason about than any more complex construction.

#### Shard chain design <a id="Shard-chain-design"></a>

Each shard has a semi-independent chain, which can process blocks much more quickly than crosslinks aggregate blocks \(the goal is 3-6 seconds\). This allows transactions to quickly get some degree of confirmation from the shard’s persistent committee before they are confirmed into the beacon chain via a crosslink. The shard chain structure is such that every block is attested to by every validator in the shard committee; this preserves simplicity and ensures that even a single shard block has a fairly high degree of confirmation; most lower-value applications should be okay with relying on a single confirmation.

Each shard block contains a pointer to its parent as well as a pointer to the beacon block at the start of the epoch. This semi-tight coupling between the beacon chain and shard chains is done to \(i\) ensure that shard chains are aware of what their persistent committees are \(as this information is generated on the beacon chain\) and \(ii\) to allow verifying shard chain blocks to be a viable way of determining the canonical beacon chain.

The shard chain state \(rewards, penalties and history accumulator\) is deliberately designed to be less than the size of a block to ensure that it can be entirely put into the beacon chain if needed for fraud proofs \(though this may be relaxed in phase 2, where the state of _each individual execution environment_ would be limited to that size, but the combined state would be larger, so Merkle proofs would be required for fraud proofs.

#### Crosslink data <a id="Crosslink-data"></a>

A crosslink contains a `data_root`, which is a Merkle root of a data structrure that contains all shard blocks in a given shard since the last crosslink \(and state roots for slots that do not have blocks\). The crosslink data structure+root has multiple purposes:

* To make the beacon chain aware of the canonical shard chain blocks.
* To create a simple byte-array that can be verified for availability through different means \(proof of custody, data availability proof\), with the guarantee that from an available crosslink the shard blocks can be fully recovered.
* To create a simple byte-array that fraud proofs can be evaluated against, and specifically so that the only kind of fraud proof required is a proof that points to two adjacent slots and verifies whether or not applying the state transition function to the post-state of slot N passing as input the data in slot N+1 \(possibly empty\) actually leads to the provided post-state of slot N+1.

### The proof of custody game <a id="The-proof-of-custody-game"></a>

For each 9-day period, each validator has the ability to privately generate a “period subkey”. The validator’s public key uniquely determines their period subkey for every period, so once a validator has deposited they have no further freedom to choose what their subkeys are. No one can compute any given validator’s subkey except the validator themselves, but once a validator reveals a subkey voluntarily, anyone can verify its correctness \(this is all done via BLS magic, and if quantum-safety is required in the future it can be done with hash-based commitments\).

When attesting to a crosslink with data DD with root RR during period jj, letting ss being the period-jj secret of that validator, a validator is required to compute a bitfield MM as follows:

* Split DD into 512-byte chunks D\[0\]...D\[n−1\]D\[0\]...D\[n−1\]
* Set MM to be the bitfield where the i’th bit is M\[i\]=mix\(s,D\[i\]\)M\[i\]=mix\(s,D\[i\]\)

They include `get_chunk_bits_root(M)` \(this is called the **custody bit**\) as part of what they are signing. `mix` and `get_chunk_bits_root` can both be viewed as hash-like functions that output a single bit \(but are designed for multi-party-computation friendliness\).

If a validator publishes their period jj subkey during or before period jj, any other validator can publish a proof-of-knowledge of the subkey to the chain, which then penalizes the validator whose subkey was revealed. The proof of knowledge also proves which validator created it; this prevents block proposers from “stealing” the whistleblowing reward \(once again all done via BLS magic, if quantum-safety is required in the future this can be done with STARKs\). The goal of this is to make it dangerous to outsource computation of MM.

The proof of custody mechanism features two challenge-response games: **chunk challenges** and **bit challenges**. A chunk challenge involves a challenger specifying an index of some slice of data that an attester committed to; the responder is required to provide a Merkle proof of the contents of that slice of data. A bit challenge involves a challenger providing an alternate bitfield M′M′ \(that the challenger believes to be correct\) where `get_chunk_bits_root(M')` _does not_ equal the bit originally signed by the responder. The challenge can be responded to by providing a Merkle branch of a slice of data D\[i\]D\[i\] where mix\(s,D\[i\]\)!=M′\[i\]mix\(s,D\[i\]\)!=M′\[i\] \(ie. the provided alternate bitfield is incorrect\). If a bit challenge is correctly responded to, the challenger is slashed. If either type of challenge is not responded to for &gt;72 days, the responder is slashed.

The purpose of this mechanism is to mitigate the [validator’s dilemma](https://eprint.iacr.org/2015/702.pdf) problem, where validators have an incentive to avoid verifying data out of laziness and piggyback on the assumption that all _other_ validators are honest; if too many validators think in this way, it could lead to a tragedy of the commons leading to the chain accepting invalid blocks. With this scheme, if a validator attempts to commit to data that they did not personally process, then they would not be able to compute MM, and so would lose the interactive challenge game.

Validators submit only one bit of MM for efficiency reasons, keeping the overhead down to 1 bit per validator in the normal case and reducing the number of pairings needed to compute the BLS multi-signature to 3 \(BLS multisignatures require n+1n+1 pairings for nn distinct messages; each validator submitting either 1 or 0 for each attestation ensures that for each attestation there are only 2 distinct messages signed\).

### SSZ <a id="SSZ"></a>

The SimpleSerialize suite contains the following algorithms:

* A serialization algorithm
* A hashing algorithm \(called `SSZTreeHash` or `hash_tree_root`\)
* An algorithm for computing a hash used for signatures: [https://github.com/ethereum/eth2.0-specs/pull/625](https://github.com/ethereum/eth2.0-specs/pull/625)
* A generalized Merkle proof algorithm \(called “SSZ partials”\) that can handle proofs for multiple values and optimally deduplicates Merkle tree sister nodes in such cases.

The serialization algorithm has the following design goals:

* Simplicity \(eg. no three clauses like RLP has for long / list encoding depending on item length\)
* Being equivalent to simple concatenation in the case of entirely fixed-size objects
* Being usable as both a consensus-layer serialization algorithm and an application-layer ABI

Note that the resulting SSZ serialization spec is very similar to the ethereum 1.0 ABI, with the major differences being \(i\) different basic data types and \(ii\) replacing the 32 byte length/position record size with a 4 byte size.

The hashing algorithm has the following design goals:

* Efficiency of computing the hash of an updated object, especially in the case where the object is very large and/or complex and the change is relatively small
* Efficiency \(in terms of verification complexity _and_ witness size\) of proving the value of a specific field even in a large or complex object with a given hash

These requirements together make a Merkle tree structure the obvious choice.

#### Generalized indices <a id="Generalized-indices"></a>

See [https://github.com/ethereum/eth2.0-specs/blob/dev/specs/light\_client/merkle\_proofs.md](https://github.com/ethereum/eth2.0-specs/blob/dev/specs/light_client/merkle_proofs.md) for a description of generalized indices, and how they allow for very easy verification of Merkle proofs “poking into” arbitrary positions in an object by representing paths as an integer or bitfield.

### The validator lifecycle <a id="The-validator-lifecycle"></a>

#### Depositing <a id="Depositing"></a>

A validator deposits by sending a transaction that calls a function on the deposit contract on the eth1 chain \(eventually, a way to deposit from inside eth2 will also be added\). A deposit specifies:

* The public key corresponding to the private key that will be used to sign messages
* The withdrawal credentials \(hash of the public key that will be used to withdraw funds once the validator is done validating\)
* The deposit amount

These values are all signed by the signing key. The goal of having separate signing and withdrawal keys is to allow the more dangerous withdrawal key to be kept more securely \(offline, not shared with any staking pools, etc\) while the signing key is used to actively sign a message every epoch.

The deposit contract maintains a Merkle root of all deposits made so far. Once a merkle root containing the deposit gets included into the eth2 chains \(via the Eth1Data voting mechanism\), an eth2 block proposer can submit a Merkle proof of the deposit and start the deposit process.

#### Activation <a id="Activation"></a>

The validator immediately joins the validator registry, but is at first inactive. The validator becomes active after N≥4N≥4 epochs; the minimum of 4 is there to ensure the RANDAO is not manipulable, and NN may exceed 4 if too many validators try to join at the same time. If the validator set has size \|V\|\|V\|, a maximum of max\(4,\|V\|65536\)max\(4,\|V\|65536\) valdators can join per epoch; if more validators try to join, they are put in a queue and processed as quickly as possible.

#### Exiting <a id="Exiting"></a>

When a validator exits \(whether by publishing a voluntary exit message or being slashed\), they are similarly put into an exit queue with the same maximum throughput.

The reason for the entrance/exit queue limits is to ensure that the validator set cannot change too quickly between any two points in time, which ensures that finality guarantees still remain between two chains as long as a validator logs on often enough \(once every ~1-2 months if \|V\|≥262144\|V\|≥262144\). See here [https://ethresear.ch/t/rate-limiting-entry-exits-not-withdrawals/4942](https://ethresear.ch/t/rate-limiting-entry-exits-not-withdrawals/4942) for rationale \(and specifically why to use a rate limit instead of a fixed waiting time\) and [https://ethresear.ch/t/weak-subjectivity-under-the-exit-queue-model/5187](https://ethresear.ch/t/weak-subjectivity-under-the-exit-queue-model/5187) for how to calculate safety margin for a client that has been offline for some amount of time.

#### Withdrawal <a id="Withdrawal"></a>

Once a validator leaves the exit queue, there is a ~27 hour period until they can withdraw. This period has several functions:

* It ensures that if a validator misbehaved there is a period of time within which the error can be caught and the validator can be slashed even if the exit queue is nearly empty.
* It provides time for the last period of shard rewards to be included.
* It provides time for proof of custody challenges to be made.

If a validator is slashed, a further delay of ~36 days is imposed. This further penalizes them \(and forces them to hold the ETH; this makes the penalty somewhat larger for malicious validators that are trying to destroy the ethereum blockchain than those validators that want to support the platform but just made a mistake, as the former category would have to risk the exposure or pay for derivatives to cancel it out\), but also allows for a period during which the number of other validators that got slashed can be calculated.

In phase 0, a “withdrawn” validator cannot actually withdraw to anywhere yet; the only distinction is that it is protected from validator penalties and does not have any responsibilities. In later phases, the ability to move funds from a withdrawn validator slot to an execution environment will be made available.

#### Effective balances <a id="Effective-balances"></a>

Most calculations based on a validator’s balance use the validator’s “effective balance”; the only exception is calculations that increase or decrease the validator’s balance. Only when the validators’s balance BB falls below EBEB or goes above EB+1.5EB+1.5 is EBEB adjusted to equal floor\(B\)floor\(B\). This is done to ensure that effective balance changes infrequently, reducing the amount of hashing needed to do to recompute the state every epoch; on average, only the balances need to all be updated, and the effective balances only get updated relatively rarely per validator. Balances are all stored in a dedicated vector, so 2∗N∗832=N22∗N∗832=N2 hashes are needed to recompute a balance array, whereas effective balances are stored in validator record objects, where at least 5N5N hashes would be needed per validator to adjust the SSZ hash roots. Additionally, EBEB can be compressed more easily into a CompactValidator object, as it’s only one byte.

### Fork mechanism <a id="Fork-mechanism"></a>

The `Fork` data structure contains \(i\) the current “fork ID”, \(ii\) the previous fork ID and \(iii\) the switchover slot. The fork ID at the current height influences the valid signatures of all messages; hence, a message signed with one fork ID is invalid to a verification function using any other fork ID.

A fork is done by adding a state transition at some “fork slot” nn which sets the previous fork ID to the current fork ID, the current fork ID to a new value, and the switchover slot to nn. Signature verification functions will verify messages using the fork ID at the slot the message is for, which could be the previous fork ID or the current one \(eg. consider the case of attestations included after a delay; an attestation from before the fork slot could be included after the fork slot\).

If any users do not want to join the fork, they can simply continue the chain that does not change the fork ID at the fork slot. The two chains would be able to proceed and validators would be free to validate on both without getting slashed.

\[宁静\]设计理念：[Serenity Design Rationale](https://notes.ethereum.org/@vbuterin/rkhCgQteN)




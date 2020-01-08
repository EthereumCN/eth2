# Specs

## 客家酿豆腐

简单，但美味！

这个版本主要将注意力放在Phase 0 的简化 \([\#1329](https://github.com/ethereum/eth2.0-specs/pull/1329), [\#1428](https://github.com/ethereum/eth2.0-specs/pull/1428), [\#1443](https://github.com/ethereum/eth2.0-specs/pull/1443)\) ，为phase 1简化版本的到来做好准备，避免产生某些偏见。特别需要指出的是，这个版本对旧phase 0版本进行了修枝剪叶，以最和谐的方法，确保[最新的分片提案](https://news.ethereum.cn/archives/845)能够在其上凌波微步。

除了这些更改之外，一个简单的证明聚合策略\([\#1440](https://github.com/ethereum/eth2.0-specs/pull/1440)\) 被添加到到验证者和网络特性里。这个策略规定了gossipsub的子网，哪个证明应该被发送，以及哪些验证者组被选出来作为“聚合器”并广播到全局频道里。

虽然，目前就Phase 1和轻客户端已经做了大量的工作，但是，这些内容的稳定性高度不确定，在未来的几个星期里有可能被改头换面。目前为止，phase 1的测试版已经被移除，因为自从这个修改后，再也不能运行其上了。

## 更新日志

_关于相关的讨论，可以来这里查阅:_ [_\#1453_](https://github.com/ethereum/eth2.0-specs/pull/1453)

### Phase 0

#### 信标链（Beacon chain）

* 特性
  * 改变信标链提交者选取逻辑 \([\#1413](https://github.com/ethereum/eth2.0-specs/pull/1413)\)
  * 添加了一些种子\(seed\)域名 \([\#1415](https://github.com/ethereum/eth2.0-specs/pull/1415)\)
  * 修正包含基于延迟的证明的奖励 \([\#1434](https://github.com/ethereum/eth2.0-specs/pull/1434)\)
  * 使用`eth1_block_hash` 作为`randao_mix` 初始值 \([\#1447](https://github.com/ethereum/eth2.0-specs/pull/1447)\)
* 修枝剪叶
  * 移除 phase 0 的`active_index_roots` 和 `compact_committees_roots` \([\#1329](https://github.com/ethereum/eth2.0-specs/pull/1329)\)
  * 移除 phase 0 的分片/交联（shards/crosslinks）\([\#1428](https://github.com/ethereum/eth2.0-specs/pull/1428)\)
  * 移除 phase 0 的转移 \([\#1443](https://github.com/ethereum/eth2.0-specs/pull/1443)\)

#### 分叉选择

* 认证分叉选择测试的状态根和其余微小改动\([\#1454](https://github.com/ethereum/eth2.0-specs/pull/1454)\)

#### 验证者

* 增加简单证明聚合策略 \([\#1440](https://github.com/ethereum/eth2.0-specs/pull/1440)\)
* 去掉验证者API，并迁移到 [eth2 APIs repo](https://github.com/ethereum/eth2.0-apis) \([\#1366](https://github.com/ethereum/eth2.0-specs/pull/1366)\)

#### 网络

* 增加简化证明聚合策略 \([\#1440](https://github.com/ethereum/eth2.0-specs/pull/1440)\)

#### 存储合约

自最新版本发布以来，存款合同已进行了一些小改动\([\#1362](https://github.com/ethereum/eth2.0-specs/pull/1362)\) 以及形式验证。 目前稳定，可以投入使用。

### 简单序列化

* 定义概要和扩展 \([\#1360](https://github.com/ethereum/eth2.0-specs/pull/1360)\)
* 增加反序列化声明 \([\#1381](https://github.com/ethereum/eth2.0-specs/pull/1381)\)

### BLS

警告:在现在的规范里， BLS 散列到 G2中存在漏洞。 标准化后将不推荐使用散列和增量方法，因此该bug暂时懒得理它。

_期望重要更新的到来_[_：对跨区块链版本BLS12-381的标准化_ ](https://github.com/ethereum/eth2.0-specs/issues/605)

### Phase 1 规范 \(_警告：不稳定_\)

目前正在根据[最新的分片提案](https://news.ethereum.cn/archives/845)重新设计第一阶 phase 1 的规范。 由于进行了重新设计，因此该规范变化很大，并且当前无法执行，因此当前在CI中禁用了 phase 1 的测试。

### 轻客户端规范 \(_警告：不稳定_\)

目前，轻客户端核心规范已经准备就绪，但仍然受限于目前正在重新设计的第一阶段规范的组件。 当前的轻客户端规范可用于一般教育目的，方便了解我们所考虑的方法，但是在phase 1稳定之后，轻客户端规范将被重度重新设计。

## Github链接：[V0.9.0版本](https://github.com/ethereum/eth2.0-specs/releases/tag/v0.9.0)


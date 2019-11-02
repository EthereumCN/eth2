---
description: 2019年9月20日 作者：Ben Edgington
---

# ETH2 双周刊

![&#x4EE5;&#x592A;&#x574A;2.0&#x4E92;&#x64CD;&#x4F5C;&#x6027;&#x7814;&#x8BA8;&#x4F1A;](../.gitbook/assets/eth-2.0-testnet-interlop-sep-9-2019.jpg)

在过去的三周里，有关 Eth2 的新闻消息都异常平静。但该现象的原因意义十分重大：所有人都完全专注于**客户端互操作性封闭研讨会（Interop Lock-in）。**

## **客户端互操作性封闭研讨会**

前两周，除了一个团队外，其他所有以太坊2.0客户端开发团队都聚集在安大略省的偏远地区，讨论如何使信标链节点能够互相沟通。加入我们的还有以太坊基金会、Whiteblock 团队和以太坊2.0阶段2的研究人员（ConsenSys 的 Quilt 团队和 EF 的 Ewasm 团队）。

在此我就不赘述整个讨论过程了。要了解详细过程，可以查看 Danny Ryan 在以太坊基金会的博客上发表的回顾文章\[1\]，我也就此在ConsenSys的博客上发表了一篇文章。总的来说，这次讨论的成功大大超乎了我们的预料。

**在此给大家分享一些推特上的高光时刻：**

![\#Eth2Interop &#x5982;&#x706B;&#x5982;&#x837C;](https://mmbiz.qpic.cn/mmbiz_jpg/4EL2Q3tnbKib8ClDQkxBoZIdJWnxH9mg8F58W0BNHfvh96VuPkseNJ1jjKyomvf20qzEZ3c9xT3RmH1o6vgbTOw/640?wx_fmt=jpeg)

![Lighthouse &#x548C; Nimbus &#x5BA2;&#x6237;&#x7AEF;&#x5BA3;&#x5E03;&#x5B9E;&#x73B0;&#x4E92;&#x64CD;&#x4F5C;&#x6027;](https://mmbiz.qpic.cn/mmbiz_jpg/4EL2Q3tnbKib8ClDQkxBoZIdJWnxH9mg8icmT8hsgZXicGsRs3Qaw2rd7t3BtBJRgzKnibicW6BUyNFgvgrNscXibT0A/640?wx_fmt=jpeg)

![Artemis &#x548C; Nimbus &#x5BA2;&#x6237;&#x7AEF;&#x968F;&#x540E;&#x4E5F;&#x5B9E;&#x73B0;&#x4E86;&#x4E92;&#x64CD;&#x4F5C;&#x6027;](https://mmbiz.qpic.cn/mmbiz_jpg/4EL2Q3tnbKib8ClDQkxBoZIdJWnxH9mg8DicG1icEU58bV8ZMYgj6uMTlwgnjYzH5Wj39LkibImM2EiazZC9nAAAdew/640?wx_fmt=jpeg)

![Lodestar &#x548C; Lighthouse &#x5BA2;&#x6237;&#x7AEF;&#x5B9E;&#x73B0;&#x4E92;&#x64CD;&#x4F5C;&#x6027;](https://mmbiz.qpic.cn/mmbiz_jpg/4EL2Q3tnbKib8ClDQkxBoZIdJWnxH9mg8t0EMWawgbz0LsyROWWOwGaNfVt8fmn2Xj6HdBJD0XPiczTHzGYUMhRg/640?wx_fmt=jpeg)

![Prysm &#x548C; Lighthouse &#x5BA2;&#x6237;&#x7AEF;&#x5B9E;&#x73B0;&#x4E92;&#x64CD;&#x4F5C;&#x6027;](https://mmbiz.qpic.cn/mmbiz_jpg/4EL2Q3tnbKib8ClDQkxBoZIdJWnxH9mg8Kwxck2tyLXpcYzCmjTX8r2eKuz3J2mGrkJ7Lew71aV4A34lAxohKKw/640?wx_fmt=jpeg)

![Artemis &#x548C; Trinity &#x5BA2;&#x6237;&#x7AEF;&#x5B9E;&#x73B0;&#x4E92;&#x64CD;&#x4F5C;&#x6027;](https://mmbiz.qpic.cn/mmbiz_jpg/4EL2Q3tnbKib8ClDQkxBoZIdJWnxH9mg8ULSJN0lhXwhKFxKTQ9Hdr983C7sfvpaQOX3R3yVefHxiaERMk9DVsSw/640?wx_fmt=jpeg)

![Trinity &#x548C; Lodestar &#x5B9E;&#x73B0;&#x4E92;&#x64CD;&#x4F5C;&#x6027;](https://mmbiz.qpic.cn/mmbiz_jpg/4EL2Q3tnbKib8ClDQkxBoZIdJWnxH9mg8W8AlOpGnqBzbSS4HzW1UXhhRWdPBDV7rgDCGxGv7Y3xF8tDlACzjmA/640?wx_fmt=jpeg)

![Artemis&#x3001;Lighthouse&#x3001;Nimbus&#x3001;Lodestar &#x56DB;&#x4E2A;&#x5BA2;&#x6237;&#x7AEF;&#x5B9E;&#x73B0;&#x4E86;&#x4E92;&#x64CD;&#x4F5C;&#x6027;](https://mmbiz.qpic.cn/mmbiz_jpg/4EL2Q3tnbKib8ClDQkxBoZIdJWnxH9mg8msNX7tVxh8X9mkaSNztpdwBpjr6W81WA4JhBGC3OL8V9HSd9ZLOwqQ/640?wx_fmt=jpeg)

![Artemis&#x3001;Prysm&#x3001;Lighthouse&#x3001;Nimbus&#x3001;Trinity &#x4E94;&#x4E2A;&#x5BA2;&#x6237;&#x7AEF;&#x5B9E;&#x73B0;&#x4E86;&#x4E92;&#x64CD;&#x4F5C;&#x6027; ](https://mmbiz.qpic.cn/mmbiz_jpg/4EL2Q3tnbKib8ClDQkxBoZIdJWnxH9mg8ss7OIvK2JYRnJpARZVqgEwib7mTqBCQGuFJm5fNO1JvgTkTFmNiaWg1g/640?wx_fmt=jpeg)

![&#x7EC8;&#x4E8E;&#xFF01;&#x6240;&#x6709;&#x8FD9;7&#x4E2A; Eth2.0 &#x5BA2;&#x6237;&#x7AEF;&#x90FD;&#x5B9E;&#x73B0;&#x4E86;&#x4E92;&#x64CD;&#x4F5C;&#x6027;](https://mmbiz.qpic.cn/mmbiz_png/4EL2Q3tnbKib8ClDQkxBoZIdJWnxH9mg8V9ic9ssrrjrRicvn1UAJDDAaoSeIs7HUGNwgG0lrMzgB5qmBN9X9brmw/640?wx_fmt=png)

![](https://mmbiz.qpic.cn/mmbiz_jpg/4EL2Q3tnbKib8ClDQkxBoZIdJWnxH9mg8FXuEM54VYuibicxpAkMnYb9g7bAjibtnJmibN70zQia0WL0vm058KaiaeG0Q/640?wx_fmt=jpeg)

特别需要提到 Parity 团队的 Wei Tang，他没能来现场，但依旧成功地实现了 Shasper 客户端与 Lighthouse 客户端之间的通信

![&#x5404;&#x5BA2;&#x6237;&#x7AEF;&#x56E2;&#x961F;&#x5728;&#x8BA8;&#x8BBA;&#x6709;&#x5173;&#x94FE;&#x540C;&#x6B65;&#x7684;&#x95EE;&#x9898;](https://mmbiz.qpic.cn/mmbiz_jpg/4EL2Q3tnbKib8ClDQkxBoZIdJWnxH9mg8dpNl45KlwSTPuRfW4ziaBmgZjIbAk0JAU5OZwdMMVicpd8bKuJrVrojw/640?wx_fmt=jpeg)

![Nimbus &#x548C; Lighthouse &#x5BA2;&#x6237;&#x7AEF;&#x5728;&#x4E24;&#x53F0;&#x6811;&#x8393;&#x6D3E; \(Raspberry Pi\) &#x8BBE;&#x5907;&#x4E0A;&#x5B9E;&#x73B0;&#x4E86;&#x901A;&#x4FE1; ](https://mmbiz.qpic.cn/mmbiz_jpg/4EL2Q3tnbKib8ClDQkxBoZIdJWnxH9mg8DnqjNCvUiatCswY45Bhib9qrNVy1OSHjxKBibpw7Emx7eP1K1eHdR9syQ/640?wx_fmt=jpeg)

![Greg &#x8868;&#x793A;&#x4E0D;&#x89E3;](https://mmbiz.qpic.cn/mmbiz_jpg/4EL2Q3tnbKib8ClDQkxBoZIdJWnxH9mg8eBszqibJGGRLia1eotxcr9HHGq8swmRU2PxcLTZUo4BSRdPE65Yp7iahQ/640?wx_fmt=jpeg)

![&#x5DE5;&#x4F5C;&#x4E4B;&#x4F59;&#x7684;&#x4F11;&#x95F2;&#x4E00;&#x523B;](https://mmbiz.qpic.cn/mmbiz_jpg/4EL2Q3tnbKib8ClDQkxBoZIdJWnxH9mg8UicMqnlzam2NAujVSibVpkfHrbPUibF8A32ibpkt7bgTE7nboJic9jkxjIw/640?wx_fmt=jpeg)

![&#x51A5;&#x601D;&#x82E6;&#x60F3;&#xFF08;&#x73BB;&#x7483;&#x95E8;&#x4E5F;&#x4E0D;&#x5BB9;&#x6613;&#xFF09;](https://mmbiz.qpic.cn/mmbiz_png/4EL2Q3tnbKib8ClDQkxBoZIdJWnxH9mg8l3efRqmQmkhQefVo1SC9ECglJeKKM6fTcibOoGp5hsIUUqBrr24BYicA/640?wx_fmt=png)

![&#x6211;&#x4ECE;&#x591A;&#x4F26;&#x591A;&#x673A;&#x573A;&#x56DE;&#x5BB6;&#x7684;&#x8DEF;&#x4E0A;&#x7684;&#x611F;&#x601D;](https://mmbiz.qpic.cn/mmbiz_jpg/4EL2Q3tnbKib8ClDQkxBoZIdJWnxH9mg8ia50UkULOS42xBWKxwx9wz4iaicLFse8yplIlEzmKsibHHwOMqDvmDUeOg/640?wx_fmt=jpeg)

我把这次聚会的一些照片做成了一个相册，放在这个网址了\[2\]。

## **以太坊2.0实现者会议**

第25次通话于9月19号进行。

* 会议议程；\[3\]
* 会议视频；\[4\]
* 我的速记 \[5\] 和 Pooja Ranjan 的详细笔记 \[6\]。

这次通话很快就结束了，只耗时45分钟。我认为每个参与者在这次互操作性讨论会后都很疲惫，需要在举办 DevCon 之前稍作调整。

值得注意的是：**规范版本0.8.4将在未来几天发布。**将包括网络规范更新，以及一些特殊测试向量 \[7\]，以修复在互操作期间发生的一些共识故障。**核心规范仍处于冻结状态，预计不会有所更改。**

## **BLS 签名方案标准化**

以太坊2.0 将使用的 BLS 签名方案的标准化工作 \[8\] 是一个尚未被广泛讨论的重要主题。与以太坊2.0一样，好几个下一代区块链（如Algorand、Chia、Dfinity），也计划在 BLS12-381 曲线上使用 BLS 签名。在未来采用一种通用方法来促进互操作性是非常有意义的。

**如今，以太坊2.0 客户端正在使用的 BLS 签名实现与提议标准有所不同。**特别是关于将哈希映射到曲线上的算法 \(将待签名数据映射到椭圆曲线上某个点的方法\)。

Sigma Prime 的 Kirk Baird 已开始起草 Eth2 BLS 规范的更新计划 \[9\]。目前我们执行 hash-to-curve 算法（“try and increment”技术）的方法非常简单。**不幸的是，它并没有成为标准，主要是因为该方法并不是常量时间。**常量时间并不是ETH2.0中必要的特性——所有转换为哈希值的输入信息都是公开的。然而，**我们需要执行新的 BLS 签名算法，以符合新的 hash to curve 标准 \[10\]。**

作为参考，我用 Java 实现了这个新方案，它通过了所有的测试向量 \[11\]。Kirk 也正在开发一个 Python 版本的实现 \[12\]。与我们当前的 Java 版本相比 \[12\]，在不包括测试的前提下，我的实现版本多出了50倍代码行。

这些待完成工作的一个明显影响就是，**在以太坊1.0链上部署验证者押金合约（Validator Deposit contract）\[13\] 的计划可能会延迟。**最初的计划是在 DevCon 会议期间部署验证者押金合约，现在看来不太可能实现。原因是一部分验证者注册过程涉及生成 BLS 签名：在该方案标准冻结之前，我们无法确定登记流程不会被更改。然而，**我们应该能在几周内做好准备，使得明年第一季度的信标链启动计划如期进行。**

## **其他研究**

简单地介绍两件事。

Vitalik 对以太坊阶段2的实现方式有了一些不同的想法 \[14\]。研究阶段2的团队在互操作性讨论会期间对此进行了深入的讨论。在对此发表意见之前，我需要先进行消化。

Ryuya Nakamura也一直在思考针对 Casper FFG 的攻击。通过对 FFG 的 Flip-flop 攻击进行分析 \[15\]，他发表了相关文章：_《针对 FFG bouncing 攻击的分析》_\[16\] 以及_《FFG 如何抵御 bouncing 攻击》_\[17\]。

## **其他新闻**

近来事务繁杂，如有遗漏，敬请海涵。

* 除了实现互操作性以外，Lighthouse和Prysm客户端都更新了。\[18\]\[19\]
* Lighthouse客户端团队成员 Mehdi 在 EthBerlin 会议期间的演讲PPT：_《以太坊2.0的性能与安全性》_\[20\]。
* David Hoffman在推特上分享了 Ethereal 特拉维夫峰会上 Vitalik 的问答内容 \[21\]。其中不乏关于以太坊2.0的干货。
* Colin Schwartz 在 Medium 上发表文章：_《以太坊2.0：Ewasm的全面向导》_\[22\]。
* Julin Chiu 对 Casper FFC 的解释性文章：_《Casper FFG：实现 PoS 的共识机制》_\[23\]。



本文涉及的链接：

\[1\]:https://blog.ethereum.org/2019/09/19/eth2-interop-in-review/

\[2\]:https://photos.app.goo.gl/djJrUreWytBbkYhcA

\[3\]:https://github.com/ethereum/eth2.0-pm/issues/85

\[4\]:https://youtu.be/pEdqjXO6euY?t=188

\[5\]:https://docs.google.com/document/d/1tTeEwHoOL3twseTsoZwBvjMlqjgZngF8a6-5Krs49so/edit\#

\[6\]:https://github.com/ethereum/eth2.0-pm/blob/213decb59f9f78d0791b6273332b6aa11e760122/eth2.0-implementers-calls/call\_025.md

\[7\]:https://github.com/djrtwo/interop-test-cases/

\[8\]:https://github.com/cfrg/draft-irtf-cfrg-bls-signature

\[9\]:https://github.com/ethereum/eth2.0-specs/pull/1398

\[10\]:https://tools.ietf.org/html/draft-irtf-cfrg-hash-to-curve-04

\[11\]:https://github.com/PegaSysEng/artemis/pull/898

\[12\]:https://github.com/ethereum/py\_ecc/pull/79

\[13\]:https://github.com/ethereum/eth2.0-specs/tree/dev/deposit\_contract

\[14\]:https://notes.ethereum.org/YNnC-fakRxixbMCTEnNDXQ?view

\[15\]:https://ethresear.ch/t/decoy-flip-flop-attack-on-lmd-ghost/6001?u=benjaminion

\[16\]:https://ethresear.ch/t/analysis-of-bouncing-attack-on-ffg/6113?u=benjaminion

\[17\]:https://ethresear.ch/t/prevention-of-bouncing-attack-on-ffg/6114?u=benjaminion

\[18\]:https://lighthouse.sigmaprime.io/update-15.html

\[19\]:https://medium.com/prysmatic-labs/ethereum-2-0-development-update-35-prysmatic-labs-d1f7515000cd

\[20\]:https://github.com/sigp/presentations/blob/master/Sigma%20Prime%20-%20Lighthouse%20-%20ETHBerlinZwei.pdf

\[21\]:https://twitter.com/TrustlessState/status/1173117084085170176

\[22\]:https://medium.com/chainsafe-systems/ethereum-2-0-a-complete-guide-ewasm-394cac756baf

\[23\]:https://medium.com/unitychain/intro-to-casper-ffg-9ed944d98b2d

_原文链接：https://notes.ethereum.org/@ChihChengLiang/Sk8Zs–CQ/https%3A%2F%2Fbenjaminion.xyz%2Fnewineth2%2F20190920.html?type=book_


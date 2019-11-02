---
description: 专为以太坊开发的客户端
---

# Trinity

## 简介

Trinity 团队由6名开发者组成，其中有5名服务于以太坊基金会，这个项目隶属于以太坊基金会。

## Trinity客户端

Trinity 是用 Python 编写的以太坊客户端，在 Python 虚拟机上运行，将对即将到来的以太坊2.0规范起重大影响。

Trinity 和 Py-EVM 的目标是取代现有的 Python 以太坊客户端，最终成为 Python 生态系统的实际标准。

虽然 Trinity 目前只发布了公共预览版本，但可以连接并同步到以太坊主网，也可供公众下载。

```text
$ trinity
INFO 06-06 10:29:44    logging  Trinity DEBUG log file is created at /Users/piper/.local/share/trinity/mainnet/logs/trinity.log
INFO 06-06 10:29:44       main  Started DB server process (pid=17034)
INFO 06-06 10:29:45       main  Started networking process (pid=17037)
INFO 06-06 10:29:46       main
   ______     _       _ __
  /_  __/____(_)___  (_) /___  __
   / / / ___/ / __ \/ / __/ / / /
  / / / /  / / / / / / /_/ /_/ /
 /_/ /_/  /_/_/ /_/_/\__/\__, /
                        /____/
INFO 06-06 10:29:46       main  Trinity/0.1.0a11/darwin/cpython3.6.3
INFO 06-06 10:29:46        ipc  IPC started at: /Users/piper/.local/share/trinity/mainnet/jsonrpc.ipc
INFO 06-06 10:29:46     server  Running server...
INFO 06-06 10:29:51     server enode://7b8fb3e32de9aa5d7930fe0dd0e2365361b85c97daa1eb042ac37005f527bb80a450e9ec9012d53d8fcb94d015b115630f4556153fcf4e746993a29b14e13734@0.0.0.0:30304
INFO 06-06 10:29:51     server  network: 1
INFO 06-06 10:29:51     server  peers: max_peers=25
INFO 06-06 10:29:51       peer  Running PeerPool...
INFO 06-06 10:29:51       peer  Connected peers: 0 inbound, 0 outbound
INFO 06-06 10:29:51       sync  Starting fast-sync; current head: #2219711
INFO 06-06 10:30:04       peer  Successfully connected to ETHPeer <Node(0x4ef8@159.65.131.192>
INFO 06-06 10:30:04      chain  Starting sync with ETHPeer <Node(0x4ef8@159.65.131.192)>
INFO 06-06 10:30:10      chain  Imported 192 headers in 5.95 seconds, new head: #2219711 (b5571e)
```

## 进度

Trinity客户端目前处于Alpha发布阶段，不适用于关键任务生产用例。

## 安装

```text
pip install -U trinity
```

## 关键文档

#### [详细说明](https://trinity-client.readthedocs.io/en/latest/guides/quickstart.html#installation)

#### [快速入门指南](https://trinity-client.readthedocs.io/en/latest/guides/quickstart.html)

####  [Serenity \(Eth 2.0\) 信标链的实现](https://github.com/ethereum/trinity/blob/master/eth2/README.md)

## 团队成员

| 成员 | 简介 | Github账号 |
| :--- | :--- | :--- |
| **Piper Merriam** | 首席架构师 | [Github](https://github.com/pipermerriam) |
| **Jason Carver** | Python 黑客 \(很友好的那种哦！\) | [Github](https://github.com/carver) |
| **Christoph Burgdorf** | 软件工程师 | [Github](https://github.com/cburgdorf) |
| **Brian Cloutier** | 软件工程师 | [Github](https://github.com/lithp) |

## **资助情况**

获得以太坊资助8万美元。

## 资源

* [Website](https://trinity.ethereum.org/)网站
* [Github](https://github.com/ethereum/py-evm)






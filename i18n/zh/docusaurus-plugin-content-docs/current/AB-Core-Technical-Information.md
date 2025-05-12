---
sidebar_position: 2
slug: /core
title: "AB Core 技术信息"
---

## 基本资料

1. 项目方官网
   - [https://ab.org/](https://ab.org/)
2. 区块链浏览器地址
   - 主网： [N/A]
   - 测试网：[https://explorer.core.testnet.ab.org/](https://explorer.core.testnet.ab.org/)
3. 区块链源码：
   - [https://github.com/ABFoundationGlobal/abcore](https://github.com/ABFoundationGlobal/abcore)
4. 发行量和流通量：
   - [https://ab.org/](https://ab.org/)

## AB Core 与 Ethereum 的主要区别：

AB Core 与 Ethereum 完全兼容，支持所有标准 EVM 合约与开发工具。

不过，AB Core 当前仅支持至 `Berlin` 硬分叉，不支持 London 分叉中引入的 EIP-1559（含 BaseFee 与 Gas 销毁机制），也未启用其后的 Shanghai、Dencun 等升级。

## 区块链相关信息

1. 币的精度
   - AB 的最小单位是 ISSAC，1AB == 1000000000000000000 ISSAC。
2. 区块间隔时间
   - 3 秒
3. 普通交易安全到账所需的确认区块数量
   - 20 个区块确认后可以认为安全。
4. 自建节点
   - [https://github.com/ABFoundationGlobal/ab-deploy](https://github.com/ABFoundationGlobal/ab-deploy)

## API

1. RPC 服务地址

   - 主网(MainNet):
     - N/A
   - 测试网(TestNet):
     - [https://rpc.core.testnet.ab.org](https://rpc.core.testnet.ab.org)

2. ChainID

   - 主网(MainNet): `36888`
   - 测试网(TestNet): `26888`

3. 目前 AB Core 提供的 RPC 服务开放使用的 API 包括如下：（如需更多接口请自建节点）

```
    "net_version",
    "net_peerCount",
    "net_listening",
    "eth_protocolVersion",
    "eth_syncing",
    "eth_mining",
    "eth_hashrate",
    "eth_gasPrice",
    "eth_blockNumber",
    "eth_getBalance",
    "eth_getStorageAt",
    "eth_getTransactionCount",
    "eth_getBlockTransactionCountByHash",
    "eth_getBlockTransactionCountByNumber",
    "eth_getUncleCountByBlockHash",
    "eth_getUncleCountByBlockNumber",
    "eth_getCode",
    "eth_sendRawTransaction",
    "eth_call",
    "eth_estimateGas",
    "eth_getBlockByHash",
    "eth_getBlockByNumber",
    "eth_getTransactionByHash",
    "eth_getTransactionByBlockHashAndIndex",
    "eth_getTransactionByBlockNumberAndIndex",
    "eth_getTransactionReceipt",
    "eth_getUncleByBlockHashAndIndex",
    "eth_getUncleByBlockNumberAndIndex",
    "eth_getCompilers",
    "eth_compileLLL",
    "eth_compileSolidity",
    "eth_compileSerpent",
    "eth_newFilter",
    "eth_newBlockFilter",
    "eth_newPendingTransactionFilter",
    "eth_uninstallFilter",
    "eth_getFilterChanges",
    "eth_getFilterLogs",
    "eth_getLogs",
    "eth_chainId",
    "eth_getProof",
```

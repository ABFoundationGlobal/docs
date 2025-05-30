---
sidebar_position: 2
slug: /iot
title: "AB IoT 技术信息"
---

## 基本资料

1. 项目方官网
   - https://ab.org/
2. 区块链浏览器地址
   - 主网： https://explorer.ab.org/
   - 测试网： https://explorer.testnet.ab.org/
3. 区块链源码：
   - https://github.com/newtonproject/newchain/
4. 发行量和流通量：
   - https://ab.org/

## AB IoT 与 Ethereum 的主要区别：

1. 签名算法：将 Ethereum 用的 secp256k1 改成了 AB IoT 用的 secp256r1
2. 地址需要通过转换后再展现给用户（用户看到的是 NEW 开头的地址，示例：NEW182F3f3q8CFM3od4RkjWPPEx6vAcBJpVdurC）。
3. SDK 里面已经提供的地址双向转换的代码。
4. 请务必对用户提交的地址进行校验，确保地址解析出来的 ChainID 与当前网络的 ChainID 一致，否则会造成交易失败或者资产丢失。具体地址解析方法请参考 example 代码。

## 区块链相关信息

1. 币的精度
   - AB 的最小单位是 ISSAC，1AB == 1000000000000000000 ISSAC。
2. 区块间隔时间
   - 3 秒
3. 普通交易安全到账所需的确认区块数量
   - 20 个区块确认后可以认为安全。
4. 自建节点
   - https://github.com/newtonproject/newchain-deploy

## API

1. RPC 服务地址

   - 主网(MainNet):
     - https://global.rpc.iot.ab.org
     - https://apne1.rpc.iot.ab.org
   - 测试网(TestNet):
     - https://rpc.iot.testnet.ab.org

2. ChainID

   - 主网(MainNet): 1012
   - 测试网(TestNet): 1007

3. 示例代码：

   - https://github.com/newtonproject/newchain-sdk-example

4. 目前 AB IoT 提供的 RPC 服务开放使用的 API 包括如下：（如需更多接口请自建节点）

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

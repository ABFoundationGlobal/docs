---
sidebar_position: 2
slug: /core
title: "AB Core Technical Information"
---

## Basic Information

- **Official Website**:  
  [https://ab.org/](https://ab.org/)

- **Blockchain Explorer**:  
  - **Mainnet**: [https://explorer.core.ab.org/](https://explorer.core.ab.org/)
  - **Testnet**: [https://explorer.core.testnet.ab.org/](https://explorer.core.testnet.ab.org/)

- **Blockchain Source Code**:  
  [https://github.com/ABFoundationGlobal/abcore](https://github.com/ABFoundationGlobal/abcore)

- **Circulation and Total Supply**:  
  [https://ab.org/](https://ab.org/)

---

## Key Differences Between AB Core and Ethereum

AB Core is fully compatible with Ethereum, supporting standard EVM contracts and developer tools.

However, AB Core currently supports up to the `Berlin` hard fork and does not implement EIP-1559 (BaseFee and gas burning) introduced in the London upgrade, nor any subsequent upgrades such as Shanghai or Dencun.

---

## Blockchain-Related Information

- **Token Precision**:  
  The smallest unit of AB is `ISSAC`.  
  **1 AB = 1,000,000,000,000,000,000 ISSAC.**

- **Block Interval**:  
  3 seconds.

- **Number of Confirmations for Transaction Security**:  
  A transaction is considered secure after 20 block confirmations.

- **Node Deployment**:  
  [https://github.com/ABFoundationGlobal/ab-deploy](https://github.com/ABFoundationGlobal/ab-deploy)

---

## API

- **RPC Service Endpoints**:
  - **Mainnet (MainNet)**:  
    - [https://rpc1.core.ab.org](https://rpc1.core.ab.org)
  - **Testnet (TestNet)**:
    - [https://rpc.core.testnet.ab.org](https://rpc.core.testnet.ab.org)

- **ChainID**:

  - **Mainnet (MainNet)**: `36888`
  - **Testnet (TestNet)**: `26888`

- **Available RPC APIs**:  
  Currently, AB Core RPC provides the following APIs for open use. For additional APIs, deploy your own node:

```plaintext
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
"eth_getProof"
```

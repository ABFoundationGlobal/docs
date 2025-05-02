---
sidebar_position: 3
slug: /abconnect
title: "AB Connect"
---

## Basic Information

AB is a blockchain network built on a Hybrid Blockchain architecture. With AB Core as the main chain, it connects multiple dedicated sidechains (AB IoT) via AB Connect, which serves as the primary component to enable efficient transfers of AB tokens between AB Core and each dedicated sidechain.

AB Connect, operated in a distributed manner through multiple nodes, establishes a decentralized network architecture to ensure security, reliability, and efficiency.

In simple terms, AB Connect, as the core connector, links AB Core and the dedicated sidechains, enabling efficient and decentralized transfers of AB tokens across the chains.

---

## API

### **API Service Endpoints**:
  - **Mainnet (MainNet)**:  
    - N/A
  - **Testnet (TestNet)**:
    - [https://api.connect.testnet.ab.org](https://api.connect.testnet.ab.org)


### Struct

<details>
 <summary><code><b>Blockchain</b></code></summary>

####

> | name         | value                                                    | desc                                                                        |
> |--------------|----------------------------------------------------------|-----------------------------------------------------------------------------|
> | `network`    | `ABCore`, `ABIoT` | blockchain network name of AB network|
> | `chain_id`   | `1`, `1012` or `main`, `test`                            | get from rpc, `eth_chainId` for ethereum or `getblockchaininfo` for bitcoin |
> | `base_chain` | `Ethereum`, `NewChain`          | Base chain                                                                  |
> | `slug`       | uuid                                                     | uid string                                                                  |

##### Example

> | network   | chain_id | base_chain | slug              |
> |-----------|----------|------------|-------------------|
> | ABIoT    | 1012     | NewChain   | abiot            |
> | ABCore  | 36888        | Ethereum   | abcore          |
> | ABIoTTestnet    | 1007     | NewChain   | abiottestnet    |
> | ABCoreTestnet  | 26888 | Ethereum   | abcoretestnet  |

</details>


<details>
 <summary><code><b>Asset</b></code></summary>

####

> | name       | desc                                       |
> |------------|--------------------------------------------|
> | asset      | empty for native coin or address for token | 
> | name       | name                                       |
> | symbol     | symbol                                     |
> | decimals   | 0-18, for AB is 18                         |
> | asset_type | `Coin`, `ERC-20`, `NRC-6`, `BRC-20`        |
> | network    | Blockchain.network                         |
> | chain_id   | Blockchain.chain_id                        |
> | base_chain | Blockchain.base_chain                      |
> | Slug       | Blockchain.slug                            |

##### Example

> | asset| name| symbol| decimal | asset_type | network  | chain_id | base_chain | slug     | desc                     |
> |----- |-----|-------|---------|------------|----------|----------|------------|----------|--------------------------|
> |      | AB  | AB    | 18      | Coin       | ABIoT    | 1012     | NewChain   | abiot    | AB IoT native asset      |
> |      | AB  | AB    | 18      | Coin       | ABCore   | 36888    | Ethereum   | abcore   | AB Core native asset     |

</details>

---


### API

<details>
 <summary><code>GET</code> <code><b>/v1/networks</b></code> <code>(get networks)</code></summary>

#### Parameters

> None

#### Responses

array of `Blockchain`

#### Example cURL

> ```javascript
>  curl http://localhost:9399/v1/networks
> ```

```json
{
  "networks": [
    {
      "network": "ABCore",
      "chain_id": "26888",
      "base_chain": "Ethereum",
      "slug": "abcore"
    },
    {
      "network": "ABIoT",
      "chain_id": "1007",
      "base_chain": "NewChain",
      "slug": "abiot"
    }
  ]
}
```

</details>

<details>
 <summary><code>GET</code> <code><b>/v1/connects</b></code> <code>(get connects)</code></summary>

#### Parameters

> None

#### Responses

> | name                     | value                | desc                                |
> |--------------------------|----------------------|-------------------------------------|
> | `bc1`                | `Blockchain`              | blockchain a                             |
> | `bc2`                | `Blockchain`              | blockchain b                             |

#### Example cURL

> ```javascript
>  curl http://localhost:9399/v1/connects
> ```

```json
{
  "networks": [
    {
      "network": "ABCore",
      "chain_id": "26888",
      "base_chain": "Ethereum",
      "slug": "abcore"
    },
    {
      "network": "ABIoT",
      "chain_id": "1007",
      "base_chain": "NewChain",
      "slug": "abiot"
    }
  ]
}
```

</details>

<details>
 <summary><code>GET</code> <code><b>/v1/pairs</b></code> <code>(get pairs)</code></summary>

#### Parameters

> None

#### Responses

> | name                     | value                | desc                                |
> |--------------------------|----------------------|-------------------------------------|
> | `id`                     | pair id              | the id of pair                      |
> | `asset_a_id`             | asset id             | the id of asset A                   |
> | `asset_b_id`             | asset id             | the id of asset  B                  |
> | `asset_a`                | `Asset`              | asset_a                             |
> | `asset_b`                | `Asset`              | asset_b                             |
> | `a2b_min_deposit_amount` | string, unit is AB   | min deposit amount for asset a to b |
> | `b2a_min_deposit_amount` | string, unit is AB   | min deposit amount for asset b to a |
> | `a2b_fee_percent`        | float, base on 10000 | fee percent for asset a to b        |
> | `b2a_fee_percent`        | float, base on 10000 | fee percent for asset b to a        |
> | `a2b_fee_min_amount`     | string, unit is AB   | min fee for asset a to b            |
> | `b2a_fee_min_amount`     |string, unit is AB    | min fee for asset b to a            |
> | `b2a_fee_min_amount`     |string, unit is AB    | min fee for asset b to a            |
> | `connect_pair`            | string               | merge of blockchain slug for a-b    |


#### Example cURL

> ```javascript
>  curl http://localhost:9399/v1/pairs
> ```

```json
{
  "pairs": [
    {
      "id": "1",
      "asset_a_id": "1",
      "asset_b_id": "2",
      "asset_a": {
        "id": "1",
        "asset": "",
        "name": "AB",
        "symbol": "AB",
        "decimals": 18,
        "asset_type": "Coin",
        "network": "ABCoreTestnet",
        "chain_id": "26888",
        "base_chain": "Ethereum",
        "slug": "abcoretestnet"
      },
      "asset_b": {
        "id": "2",
        "asset": "",
        "name": "AB",
        "symbol": "AB",
        "decimals": 18,
        "asset_type": "Coin",
        "network": "ABIoTTestnet",
        "chain_id": "1007",
        "base_chain": "NewChain",
        "slug": "abiottestnet"
      },
      "a2b_min_deposit_amount": "12",
      "b2a_min_deposit_amount": "12",
      "a2b_fee_percent": "0.000000",
      "b2a_fee_percent": "0.000000",
      "a2b_fee_min_amount": "11.55",
      "b2a_fee_min_amount": "11.55",
      "connect_pair": "abcoretestnet-abiottestnet"
    }
  ]
}
```

</details>

<details>
 <summary><code>GET</code> <code><b>/v1/account</b></code> <code>(get account's deposit address)</code></summary>

#### Parameters

> | name                   | value     | desc                                                                       |
> |------------------------|-----------|----------------------------------------------------------------------------|
> | `recipient_address`    | `address` | recipient address on recipient blockchain, user's address to receive asset |
> | `recipient_blockchain` | `slug`    | slug of recipient blockchain                                               | 
> | `deposit_blockchain`   | `slug`    | slug of deposit blockchain                                                 |

#### Responses

> | name                   | value     | desc                                                                       |
> |------------------------|-----------|----------------------------------------------------------------------------|
> | `recipient_address`    | `address` | recipient address on recipient blockchain, user's address to receive asset |
> | `recipient_blockchain` | `slug`    | slug of recipient blockchain                                               | 
> | `deposit_blockchain`   | `slug`    | slug of deposit blockchain                                                 |
> | `deposit_address`      | `address` | deposit address on deposit blockchain, which used for use to send asset to |


#### Example cURL

> ```bash
>  curl http://127.0.0.1:9399/v1/account?recipient_address=0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045&recipient_blockchain=abcore&deposit_blockchain=abiot
> ```

```json
{
  "recipient_address": "0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045",
  "recipient_blockchain": "abcore",
  "deposit_address": "NEW17zWPekqx7GKGQFvzk3wqF4SbYFgv1xoCpMo",
  "deposit_blockchain": "abiot"
}
```

</details>

<details>
 <summary><code>GET</code> <code><b>/v1/history</b></code> <code>(get all history or account's history)</code></summary>

#### Parameters

> | name                     | value                                | desc                                        |
> |--------------------------|--------------------------------------|---------------------------------------------|
> | `page_id`                | uint64                               | `Optional`, page id, default 0              |
> | `page_size`              | 50                                   | `Optional`, page size, default 50           |
> | `source_deposit_address` | `address` on `source_blockchain`     | `deposit_address` get by `v1/account`       |
> | `source_sender`          | `address` on `source_blockchain`     | the address who send AB to `deposit_address`|
> | `source_blockchain`      | `slug` of `blockchain`               | slug of blockchain, get by `v1/networks`    |
> | `destination_address`    | `address` on `destination_blockchain`| `deposit_address` get by `v1/account`       |
> | `destination_blockchain` | `slug` of `blockchain`               | slug of blockchain                          |

if `address` and `blockchain` is empty, return all history 

#### Responses


> | name     | value     | desc           |
> |----------|-----------|----------------|
> | `status` | `Deposit`,`Pending`,`Confirmed` | current status |
> | `list`   | `History` | history list   |


the  `History` is as follow:
 
| Name | Type | Description |
|------|------|-------------|
| id | integer | Unique ID of the history record |
| pair_id | integer | Pair ID related to this transfer |
| source_slug | string | Slug of the source blockchain |
| source_network | string | Source network name |
| source_chain_id | string | Source blockchain chain ID |
| source_base_chain | string | Source blockchain base chain |
| destination_slug | string | Slug of the destination blockchain |
| destination_network | string | Destination network name |
| destination_chain_id | string | Destination blockchain chain ID |
| destination_base_chain | string | Destination blockchain base chain |
| source_deposit_address | string | Deposit address on the source blockchain |
| source_sender | string | Sender address on the source blockchain |
| destination_address | string | Destination address on the destination blockchain |
| source_block_number | string | Block number of source blockchain transaction |
| destination_block_number | string | Block number of destination blockchain transaction |
| source_block_timestamp | string | Block timestamp of source blockchain transaction |
| destination_block_timestamp | string | Block timestamp of destination blockchain transaction |
| source_tx_hash | string | Transaction hash on the source blockchain |
| destination_tx_hash | string | Transaction hash on the destination blockchain |
| source_asset_id | integer | Asset ID |
| source_asset_address | string | Asset address on the source blockchain (empty if native) |
| source_asset_name | string | Asset name |
| source_asset_symbol | string | Asset symbol |
| source_asset_decimals | integer | Asset decimals |
| source_asset_type | string | Asset type (e.g., Coin, ERC20) |
| destination_asset_id | integer | Asset ID |
| destination_asset_address | string | Asset address on the destination blockchain (empty if native) |
| destination_asset_name | string | Asset name |
| destination_asset_symbol | string | Asset symbol |
| destination_asset_decimals | integer | Asset decimals |
| destination_asset_type | string | Asset type (e.g., Coin, ERC-20) |
| source_amount | string | Amount sent on the source blockchain |
| destination_amount | string | Amount received on the destination blockchain |
| fee | string | Fee amount charged during the transfer |
| status | string | Status of the transfer (`Deposit`,`Pending`,`Confirmed`,`Error`) |


##### Example cURL

> ```javascript
>  curl http://localhost:9399/v1/history
> ```

```json
{
  "page_id": "1",
  "page_size": "1",
  "total_page": "4",
  "total_history": "3",
  "list": [
    {
      "id": "3",
      "pair_id": "1",
      "source_slug": "abiottestnet",
      "source_network": "ABIoTTestnet",
      "source_chain_id": "1007",
      "source_base_chain": "NewChain",
      "destination_slug": "abcoretestnet",
      "destination_network": "ABCoreTestnet",
      "destination_chain_id": "26888",
      "destination_base_chain": "Ethereum",
      "source_deposit_address": "NEW17zVctFa42dC1rBNFPf775Bq34yiwWLz4GM1",
      "source_sender": "NEW17zS9ZvgGV1EaT8KT2tLjqRvQbcApjFot8xj",
      "destination_address": "0x7EdC0CaDD6c20811058D4FB3EDA6F9218cCC7332",
      "source_block_number": "15368195",
      "destination_block_number": "4579902",
      "source_block_timestamp": "1746118154",
      "destination_block_timestamp": "1746118194",
      "source_tx_hash": "0x7abaedaaed2f2da1ebc9c0622e06a80725149db5adf1df363c92011644de0b0f",
      "destination_tx_hash": "0xd4d5cea2d5ae6b89a70257cff068587938c367c6f5729a4929b974060ac3db1b",
      "source_asset_id": "2",
      "source_asset_address": "",
      "source_asset_name": "AB",
      "source_asset_symbol": "AB",
      "source_asset_decimals": 18,
      "source_asset_type": "Coin",
      "destination_asset_id": "1",
      "destination_asset_address": "",
      "destination_asset_name": "AB",
      "destination_asset_symbol": "AB",
      "destination_asset_decimals": 18,
      "destination_asset_type": "Coin",
      "source_amount": "100",
      "destination_amount": "88.45",
      "fee": "11.55",
      "status": "Confirmed"
    }
  ],
  "source_deposit_address": "",
  "source_sender": "",
  "source_blockchain": "",
  "source_asset_id": "",
  "destination_address": "",
  "destination_blockchain": "",
  "destination_asset_id": "",
  "pairId": "",
  "status": ""
}
```

</details>

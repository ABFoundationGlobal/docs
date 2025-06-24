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
    - [https://api.connect.ab.org](https://api.connect.ab.org)
  - **Testnet (TestNet)**:
    - [https://api.connect.testnet.ab.org](https://api.connect.testnet.ab.org)


### Struct

<details>
 <summary><code><b>Blockchain</b></code></summary>

####

> | name         | value                                                           | desc                                 |
> |--------------|-----------------------------------------------------------------|--------------------------------------|
> | `network`    | `ABCore`, `ABIoT`, `ABCoreTestnet`, `ABIoTTestnet`              | blockchain network name of AB network|
> | `chain_id`   | `1`, `1012` or `main`, `test`                                   | get from rpc, `eth_chainId` for evm  |
> | `base_chain` | `Ethereum`, `NewChain`                                          | Base chain                           |
> | `slug`       | uuid, one of `abcore`, `abiot`, `abcoretestnet`, `abiottestnet` | uid                                  |

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

> ```bash
>  curl http://localhost:9699/v1/networks
> ```

```json
{
  "networks": [
    {
      "network": "ABCore",
      "chain_id": "36888",
      "base_chain": "Ethereum",
      "slug": "abcore"
    },
    {
      "network": "ABIoT",
      "chain_id": "1012",
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

> ```bash
>  curl http://localhost:9699/v1/connects
> ```

```json
{
  "connects": [
    {
      "bc1": {
        "network": "ABCore",
        "chain_id": "36888",
        "base_chain": "Ethereum",
        "slug": "abcore"
      },
      "bc2": {
        "network": "ABIoT",
        "chain_id": "1012",
        "base_chain": "NewChain",
        "slug": "abiot"
      }
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

> ```bash
>  curl http://localhost:9699/v1/pairs
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
        "network": "ABCore",
        "chain_id": "36888",
        "base_chain": "Ethereum",
        "slug": "abcore"
      },
      "asset_b": {
        "id": "2",
        "asset": "",
        "name": "AB",
        "symbol": "AB",
        "decimals": 18,
        "asset_type": "Coin",
        "network": "ABIoT",
        "chain_id": "1012",
        "base_chain": "NewChain",
        "slug": "abiot"
      },
      "a2b_min_deposit_amount": "12",
      "b2a_min_deposit_amount": "12",
      "a2b_fee_percent": "0.000000",
      "b2a_fee_percent": "0.000000",
      "a2b_fee_min_amount": "11.55",
      "b2a_fee_min_amount": "11.55",
      "connect_pair": "abcore-abiot"
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

if recipient blockchain is AB Core network, the address must be in checksum.

#### Responses

> | name                   | value     | desc                                                                       |
> |------------------------|-----------|----------------------------------------------------------------------------|
> | `recipient_address`    | `address` | recipient address on recipient blockchain, user's address to receive asset |
> | `recipient_blockchain` | `slug`    | slug of recipient blockchain                                               | 
> | `deposit_blockchain`   | `slug`    | slug of deposit blockchain                                                 |
> | `deposit_address`      | `address` | deposit address on deposit blockchain, which used for use to send asset to |


#### Example cURL

> ```bash
>  curl http://127.0.0.1:9699/v1/account?recipient_address=0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045&recipient_blockchain=abcore&deposit_blockchain=abiot
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
| hash | string | Always 66 characters (0x + 64 hex digits), SHA-256 hash of concatenated network, chain ID, transaction hash, and transaction index |
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

#### Hash Calculation

The `hash` field is calculated using SHA-256 hash of the concatenated string with colon separator:
```
hash = SHA256(network:chainId:txHash:txIndex)
```

Where:
- `network`: The blockchain network name (e.g., "ABIoT", "ABCore")
- `chainId`: The blockchain chain ID (e.g., "1012", "36888")
- `txHash`: The transaction hash on the source blockchain
- `txIndex`: The transaction index within the block

The result is a 64-character hexadecimal string prefixed with "0x" (total 66 characters).

#### Example cURL

> ```bash
>  curl http://localhost:9699/v1/history
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
      "hash": "c78b39cbd08e12dd4357c4016592c3bd975f9fe32a55887dfa75ce8d79234488",
      "pair_id": "1",
      "source_slug": "abiot",
      "source_network": "ABIoT",
      "source_chain_id": "1012",
      "source_base_chain": "NewChain",
      "destination_slug": "abcore",
      "destination_network": "ABCore",
      "destination_chain_id": "36888",
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


</details>

<details>
 <summary><code>GET</code> <code><b>/v1/history/hash</b></code> <code>(get history by hash)</code></summary>

#### Parameters

> | name | value | desc |
> |------|-------|------|
> | `hash` | string | The hash of the history record (66 characters: 0x + 64 hex digits) |

#### Responses

Returns a single `History` object with the same structure as in the `/v1/history` endpoint.

#### Hash Calculation

The `hash` parameter should be calculated using the same method as described in the `/v1/history` endpoint:
```
hash = SHA256(network:chainId:txHash:txIndex)
```

Where:
- `network`: The blockchain network name (e.g., "ABIoT", "ABCore")
- `chainId`: The blockchain chain ID (e.g., "1012", "36888")
- `txHash`: The transaction hash on the source blockchain
- `txIndex`: The transaction index within the block

The result is a 64-character hexadecimal string prefixed with "0x" (total 66 characters).

#### Example cURL

> ```bash
>  curl http://localhost:9699/v1/history/hash?hash=0x7abaedaaed2f2da1ebc9c0622e06a80725149db5adf1df363c92011644de0b0f
> ```

```json
{
  "history": {
    "id": "3",
    "hash": "0x7abaedaaed2f2da1ebc9c0622e06a80725149db5adf1df363c92011644de0b0f",
    "pair_id": "1",
    "source_slug": "abiot",
    "source_network": "ABIoT",
    "source_chain_id": "1012",
    "source_base_chain": "NewChain",
    "destination_slug": "abcore",
    "destination_network": "ABCore",
    "destination_chain_id": "36888",
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
}
```

</details>


<details>
 <summary><code>GET</code> <code><b>/v1/ab</b></code> <code>(get supply of AB)</code></summary>

#### Parameters

> None

#### Responses


> | name     | value     | desc           |
> |----------|-----------|----------------|
> | `chains`   | `Chain` | chain list   |


the  `Chain` is as follow:
 
> | name                     | value                | desc                                |
> |--------------------------|----------------------|-------------------------------------|
> | `slug`                   | `abcore`,`abiot`     | slug of blockchain, get by `/v1/networks`|
> | `network`             | `ABCore`,`ABIoT` | network of blockchain |
> | `chain_id`   | string, `1`, `1012` or `main`, `test` | get from rpc, `eth_chainId` |
> | `base_chain` | `Ethereum`, `NewChain`          | Base chain |
> | `status`                | `OK`,`STUCK`, `OFFLINE`, `SYNCING` | status of chain |
> | `latest_height`        | number | latest block number        |
> | `name`     | `AB`   |  the name of AB in this chain |
> | `symbol`            | `AB`               | the symbol of AB in this chain |
> | `decimals`            | `18`               | the decimals of AB in this chain |
> | `supply`            | string               | the amount of AB in unit `AB` |

The `totalSupply` of `AB` is the sum of the `supply` from each chain.

#### Example cURL

> ```bash
>  curl http://localhost:9699/v1/ab
> ```

```json
{
  "chains": [
    {
      "slug": "abcore",
      "network": "ABCore",
      "chain_id": "36888",
      "base_chain": "Ethereum",
      "status": "OK",
      "latest_height": "4648796",
      "name": "AB",
      "symbol": "AB",
      "decimals": 18,
      "supply": "80.05"
    },
    {
      "slug": "abiot",
      "network": "ABIoT",
      "chain_id": "1012",
      "base_chain": "NewChain",
      "status": "OK",
      "latest_height": "15391173",
      "name": "AB",
      "symbol": "AB",
      "decimals": 18,
      "supply": "99999999919.95"
    }
  ]
}
```

</details>

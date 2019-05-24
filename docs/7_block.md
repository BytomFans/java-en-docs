---
id: block
title: Block API
sidebar_label: Bytom.Block.API
---

## get-block-count

Returns the current block height for blockchain.

#### Parameters

none

#### Returns

- `Integer` - *block_count*, recent block height of the blockchain.

#### Example
```java
Client client = TestUtils.generateClient();
int count = Block.getBlockCount(client);
```
```bash
// Result
get-block-count:220928
```

## get-block-hash

Returns the current block hash for blockchain.

#### Parameters

none

#### Returns

- `String` - *block_hash*, recent block hash of the blockchain.

#### Example
```java
Client client = TestUtils.generateClient();
String blockHash = Block.getBlockHash(client);
```
```bash
// Result
get-block-hash:1f95cdb223af190f2a9aced5931e0845e3e9f89d5e6bbb1605a2df725bcda67c
```

## get-block

Returns the detail block by block height or block hash.

#### Parameters

`Object`: block_height | block_hash

Optional:

- `String` - *block_hash*, hash of block.
- `Integer` - *block_height*, height of block.

#### Returns

`Object`:

- `String` - *hash*, hash of block.

- `Integer` - *size*, size of block.

- `Integer` - *version*, version of block.

- `Integer` - *height*, height of block.

- `String` - *previous_block_hash*, previous block hash.

- `Integer` - *timestamp*, timestamp of block.

- `Integer` - *nonce*, nonce value.

- `Integer` - *bits*, bits of difficulty.

- `String` - *difficulty*, difficulty value(String type).

- `String` - *transaction_merkle_root*, merkle root of transaction.

- `String` - *transaction_status_hash*, merkle root of transaction status.

- `Array of Object`- * transactions*, transaction object:

  - `String` - *id*, transaction id, hash of the transaction.

  - `Integer` - *version*, version of transaction.

  - `Integer` - *size*, size of transaction.

  - `Integer` - *time_range*, the unix timestamp for when the requst was responsed.

  - `Boolean` - *status_fail*, whether the state of the request has failed.

  - `String` - *mux_id*, the previous transaction mux id(source id of utxo).

  - `Array of Object`- *inputs*, object of inputs for the transaction.

    - `String` - *type*, the type of input action, available option include: 'spend', 'issue', 'coinbase'.
    - `String` - *asset_id*, asset id.
    - `String` - *asset_alias*, name of asset.
    - `Object` - *asset_definition*, definition of asset(json object).
    - `Integer` - *amount*, amount of asset.
    - `Object` - *issuance_program*, issuance program, it only exist when type is 'issue'.
    - `Object` - *control_program*, control program of account, it only exist when type is 'spend'.
    - `String` - *address*, address of account, it only exist when type is 'spend'.
    - `String` - *spent_output_id*, the front of outputID to be spent in this input, it only exist when type is 'spend'.
    - `String` - *account_id*, account id.
    - `String` - *account_alias*, name of account.
    - `Object` - *arbitrary*, arbitrary infomation can be set by miner, it only exist when type is 'coinbase'.

  - `Array of Object` - *outputs* , object of outputs for the transaction.

    - `String` - *type*, the type of output action, available option include: 'retire', 'control'.
    - `String` - *id*, outputid related to utxo.
    - `Integer` - *position*, position of outputs.
    - `String` - *asset_id*, asset id.
    - `String` - *asset_alias*, name of asset.
    - `Object` - *asset_definition*, definition of asset(json object).
    - `Integer` - *amount*, amount of asset.
    - `String` - *account_id*, account id.
    - `String` - *account_alias*, name of account.
    - `Object` - *control_program*, control program of account.
    - `String` - *address*, address of account.

#### Example

get specified block information by block_hash or block_height, if both exists, the block result is querying by hash.

```java
Client client = TestUtils.generateClient();
int height = Block.getBlockCount(client);
String blockHash = Block.getBlockHash(client);

Block block = new Block.QueryBuilder()
    .setBlockHeight(height)
    .setBlockHash(blockHash)
    .getBlock(client);
```
```bash
// Result
{
  "bits": 2305843009222082600,
  "difficulty": "5549086336",
  "hash": "886a8e85b275e7d65b569ba510875c0e63dece1a94569914d7624c0dac8002f9",
  "height": 43,
  "nonce": 3,
  "previous_block_hash": "2c72ccbd53b92a4f9423c5b610b4e106bbe8fbf3ecf2e16a1266b17ee323ff9d",
  "size": 386,
  "timestamp": 1521614189,
  "transaction_merkle_root": "77d40262cfeca3a16d4587132974552ef00951e43ce567a26801ebc3dbdb4d96",
  "transaction_status_hash": "53c0ab896cb7a3778cc1d35a271264d991792b7c44f5c334116bb0786dbc5635",
  "transactions": [
    {
      "id": "4576b1b1ec251da3263dbdd5486bcbf9a1cd1f712172dbe7a7a5fe46ab194629",
      "inputs": [
        {
          "amount": 0,
          "arbitrary": "09",
          "asset_definition": "7b7d",
          "asset_id": "0000000000000000000000000000000000000000000000000000000000000000",
          "type": "coinbase"
        }
      ],
      "mux_id": "2383cefe8a34ea5810cc0706f2cf8cf08a106f90fc3eb3441f723cecdbc61331",
      "outputs": [
        {
          "address": "sm1q4pkg8msjumtep7ecsdzuct3tsuzk5pmnm3p8nr",
          "amount": 624000000000,
          "asset_definition": "7b7d",
          "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
          "control_program": "0014f3403bcd8b443d03882a280b50f6f98986e1a255",
          "id": "da87b40854a9b93be72ecdc24fe7bb03986ea3530e344b0f918f0788c3d83717",
          "position": 0,
          "type": "control"
        }
      ],
      "size": 77,
      "status_fail": false,
      "time_range": 0,
      "version": 1
    }
  ],
  "version": 1
}
```

## get-block-header

Returns the detail block header by block height or block hash.

#### Parameters

`Object`: block_height | block_hash

Optional:

- `String` - *block_hash*, hash of block.
- `Integer` - *block_height*, height of block.

#### Returns

- `Object` - *block_header*, header of block.
- `Integer` - *reward*, reward.

#### Example
```java
Client client = TestUtils.generateClient();
int height = Block.getBlockCount(client);
String blockHash = Block.getBlockHash(client);

Block.BlockHeader blockHeader = new Block.QueryBuilder()
    .setBlockHeight(height)
    .setBlockHash(blockHash)
    .getBlockHeader(client);
```
```bash
// Result
{
  "block_header": "01019601e87da37e7d73f31d54304c719c9058ec7bc7de7819deda89a7c8834a99bc05b8fbdbe6d60540eba9e5d5cb79fd87b3c0fad32f6772c1e4483f2a070e093a6176d85226d986a8c9c377e5192668bc0a367e4a4764f11e7c725ecced1d7b6a492974fab1b6d5bc00ad918480808080801e",
  "reward": 41250000000
}
```

## get-difficulty

Returns the block difficulty by block height or block hash.

#### Parameters

- `String` - *block_hash*, hash of block.
- `Integer` - *block_height*, height of block.

#### Returns

- `Integer` - *bits*, bits of block.
- `String` - *difficulty*, difficulty of block.
- `String` - *hash*, block hash.
- `Integer` - *height*, block height.

##### Example

Get difficulty for specified block hash / height.
```java
Client client = TestUtils.generateClient();
int height = Block.getBlockCount(client);
String blockHash = Block.getBlockHash(client);

Block.BlockDifficulty blockDifficulty = new Block.QueryBuilder()
    .setBlockHeight(height)
    .setBlockHash(blockHash)
    .getBlockDifficulty(client);
```
```bash
// Result
{
  "bits": 2161727821137910500,
  "difficulty": "15154807",
  "hash": "d1fce60caea5466eae2b812e4586b55120c52aca27b6c92bd7c51e9cda82dcdf",
  "height": 506
}
```

## get-hash-rate

Returns the block hash rate by block height or block hash, it returns the current block hash rate when request is empty.

#### Parameters

- `String` - *block_hash*, hash of block.
- `Integer` - *block_height*, height of block.

#### Returns

- `Integer` - *hash_rate*, difficulty of block.
- `String` - *hash*, block hash.
- `Integer` - *height*, block height.

#### Example

Get hash rate for specified block hash / height.
```java
Client client = TestUtils.generateClient();
int height = Block.getBlockCount(client);
String blockHash = Block.getBlockHash(client);

Block.BlockHashRate blockHashRate = new Block.QueryBuilder()
    .setBlockHeight(height)
    .setBlockHash(blockHash)
    .getHashRate(client);
```
```bash
// Result
{"hash":"1f95cdb223af190f2a9aced5931e0845e3e9f89d5e6bbb1605a2df725bcda67c","height":220928,"hash_rate":399323574}
```


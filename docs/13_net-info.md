---
id: net_info
title: Net_info API
sidebar_label: Bytom.New_info.API
---

## net-info

Returns the information of current network node.

#### Parameters

none

#### Returns

`Object`:

- `Boolean` - *listening*, whether the node is listening.
- `Boolean` - *syncing*, whether the node is syncing.
- `Boolean` - *mining*, whether the node is mining.
- `Integer` - *peer_count*, current count of connected peers.
- `Integer` - *current_block*, current block height in the node's blockchain.
- `Integer` - *highest_block*, current highest block of the connected peers.
- `String` - *network_id*, network id.
- `String` - *version*, current version of the running bytomd.

#### Example
```java
Client client = TestUtils.generateClient();
netInfo = CoreConfig.getNetInfo(client);
Assert.assertNotNull(netInfo);
```
```bash
// Result
{"listening":true,"syncing":false,"mining":false,"peer_count":4,"current_block":220923,"highest_block":220923,"network_id":"mainnet"}
```


---
id: gas
title: Gas_rate API
sidebar_label: Bytom.Gas.API
---

## gas-rate

Quary gas rate.

#### Parameters

none

#### Returns

- `Integer` - *gas_rate*, gas rate.

#### Example
```java
Client client = TestUtils.generateClient();
gasRate = CoreConfig.getGasRate(client);
Assert.assertNotNull(gasRate);
```
```bash
// Result
0    INFO  [2019-04-24 14:26:24]  gas-rate:
2    INFO  [2019-04-24 14:26:24]  200
```
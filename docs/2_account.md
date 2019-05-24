---
id: account
title: Account API
sidebar_label: Bytom.Account.API
---



## creat-account

Create account to manage addresses. single sign account contain only one root_xpubs and quorum; however multi sign account contain many number of root_xpubs and quorum, quorum is the number of verify signature, the range is [1, len(root_xpubs)].

#### Parameters

- `Array of Sring` -  *root_xpubs*, pubkey array.

- `String` - *alias*, name of the account.

- `Integer` - *quorum*, the default value is `1`, threshold of keys that must sign a transaction to spend asset units controlled by the account.

Optional:

- `String` - *access_token*, if optional when creating account locally. However, if you want to create account remotely, it's indispensable.

#### Returns

-  `String` - *id*, account id.

-  `String` - *alias*, name of account.

-  `Integer` - *key_index*, key index of account.

-  `Integer` - *quorum*, threshold of keys that must sign a transaction to spend asset units controlled by the account.

-  `Array of Object` -  *xpubs*, pubkey array.

#### Example
```java
Client client = TestUtils.generateClient();
String alias = "AccountTest.testAccountCreate.002";
Integer quorum = 1;
List<String> root_xpubs = new ArrayList<>();
root_xpubs.add("c4b25825e92cd8623de4fd6a35952ad0efb2ed215fdb1b40754f0ed12eff7827d147d1e8b003601ba2f78a4a84dcc77e93ed282633f2679048c5d5ac5ea10cb5");
Account.Builder builder = new Account.Builder().setAlias(alias).setQuorum(quorum).setRootXpub(root_xpubs);
Account account = Account.create(client, builder);
System.out.println(account);
```

```bash
// Result
INFO  [2019-04-23 16:39:23]  create-account
INFO  [2019-04-23 16:39:23]  Account{id='0RKNGHTRG0A08', alias='accounttest.testaccountcreate.002', key_index=3, quorum=1, xpubs=[c4b25825e92cd8623de4fd6a35952ad0efb2ed215fdb1b40754f0ed12eff7827d147d1e8b003601ba2f78a4a84dcc77e93ed282633f2679048c5d5ac5ea10cb5]}
Account{id='0RKNGHTRG0A08', alias='accounttest.testaccountcreate.002', key_index=3, quorum=1, xpubs=[c4b25825e92cd8623de4fd6a35952ad0efb2ed215fdb1b40754f0ed12eff7827d147d1e8b003601ba2f78a4a84dcc77e93ed282633f2679048c5d5ac5ea10cb5]}
```

## list-accounts

Returns the list of all available accounts.

#### Parameters
none
#### Returns
- `Array of Object`, account array.
  - `String` - *id*, account id.
  - `String` - *alias*, name of account.
  - `Integer` - *key_index*, key index of account.
  - `Integer` - quorum,  threshold of keys that must sign a transaction to spend asset units controlled by the account.
  - `Array of Object` - xpubs, pubkey array.
#### Example

```java
Client client = TestUtils.generateClient();
List<Account> accountList = Account.list(client);
```

```bash
// Result
INFO  [2019-04-23 16:47:25]  list-accounts:
INFO  [2019-04-23 16:47:25]  size of accountList:3
INFO  [2019-04-23 16:47:25]  [Account{id='0QRSNOQE00A02', alias='alice', key_index=1, quorum=1, xpubs=[872e6fbe0ad47b0ff6435bcc4c18fd0c00631afe6c4433938fd7059f32d9c26bb888d0f112cbc07880a1d9ef50111154fa34570233bda070503f6fbe94daf974]}, Account{id='0RKCD5TR00A04', alias='accounttest.testaccountcreate.002', key_index=1, quorum=1, xpubs=[c4b25825e92cd8623de4fd6a35952ad0efb2ed215fdb1b40754f0ed12eff7827d147d1e8b003601ba2f78a4a84dcc77e93ed282633f2679048c5d5ac5ea10cb5]}, Account{id='0RKCF7B800A06', alias='accounttest.testaccountcreate.002', key_index=2, quorum=1, xpubs=[c4b25825e92cd8623de4fd6a35952ad0efb2ed215fdb1b40754f0ed12eff7827d147d1e8b003601ba2f78a4a84dcc77e93ed282633f2679048c5d5ac5ea10cb5]}, Account{id='0RKNGHTRG0A08', alias='accounttest.testaccountcreate.002', key_index=3, quorum=1, xpubs=[c4b25825e92cd8623de4fd6a35952ad0efb2ed215fdb1b40754f0ed12eff7827d147d1e8b003601ba2f78a4a84dcc77e93ed282633f2679048c5d5ac5ea10cb5]}]
```

## delete-account

Delete existed account, please make sure that there is no balance in the related addresses.

#### Parameters
- `String` - *account-info*, account_alias | account_id
#### Returns
none if the account is deleted successfully.
#### Example
```java
Client client = TestUtils.generateClient();
String id = "0QRSNOQE00A02";
Account.delete(client, id);
```
```bash
//none
```
## create-account-receiver
create address and control program, the address and control program is are one to one relationship. in build-transaction API, receiver is address when action type is control_address, and receiver is control program when action type is control_program, they are the same result.
#### Parameters
`Object`: *account_alias | account_id*
可选：

- `String` - *account_alias*, alias of account.
- `String` - *account_id*, id of account.
#### Returns
- `String` - *address*, address of account.
- `String` - *control_program*, control program of account.
#### Example
```java
Client client = TestUtils.generateClient();
String alias = "test1";
String id = "0RKNGHTRG0A08";
Account.ReceiverBuilder receiverBuilder = new Account.ReceiverBuilder().setAccountAlias(alias).setAccountId(id);

Receiver receiver = receiverBuilder.create(client);
System.out.println(receiver);
```
```bash
// Result
{"address":"bm1q87xrkeha33sgyn0gtj2pdxfcn22u78263yqfx7","control_program":"00143f8c3b66fd8c60824de85c941699389a95cf1d5a"}
```

## list-addresses

Returns the sub list of all available addresses by account.

#### Parameters

- `String` - *account_alias*, alias of account.
- `String` - *account_id*, id of account.

#### Returns

  - `String` - *account_alias*, alias of account.
  - `String` - *account_id*, id of account.
  - `String` - *address*, address of account.
  - `Boolean` - *change*, whether the account address is change.

####  Example

```java
Client client = TestUtils.generateClient();
String alias = "test1";
String id = "0RKNGHTRG0A08";
Account.AddressBuilder addressBuilder = new Account.AddressBuilder().setAccountId(id).setAccountAlias(alias);

List<Account.Address> addressList = addressBuilder.list(client);
```
```bash
// Result
[
  {
    "account_alias": "alice",
    "account_id": "086KQD75G0A02",
    "address": "bm1qcn9lf7nxhswratvmg6d78nq7r7yupm36qgsv55",
    "change": false
  },
  {
    "account_alias": "alice",
    "account_id": "086KQD75G0A02",
    "address": "bm1qew4h5uvt5ssrtg2alms0j77r94c30m78ucrcxy",
    "change": false
  },
  {
    "account_alias": "alice",
    "account_id": "086KQD75G0A02",
    "address": "bm1qgnp4lte7wge0rsekevjlrdh39vkzz0c2alheue",
    "change": false
  }
]
```

## validate-address

Verify the address is valid, and judge the address is own.

#### Parameters

- `String` - *address*, address of account.

####　Returns

- `Boolean` - *vaild*, whether the account address is valid.

- `Boolean` - *is_local*, whether the account address is local.

#### Example

```java
Client client = TestUtils.generateClient();
String alias = "test1";
String id = "0RKNGHTRG0A08";

Account.AddressBuilder addressBuilder = new Account.AddressBuilder().setAccountId(id).setAccountAlias(alias);
List<Account.Address> addressList = addressBuilder.list(client);

Account.Address address = addressBuilder.validate(client, addressList.get(0).address);
```

```bash
// Result
{"is_local":true}
```
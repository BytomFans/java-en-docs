---
id: feed
title: Feed API
sidebar_label: Bytom.Feed.API
---

## create-transaction-feed

Create transaction feed.

#### Parameters

- `String` - *alias*, name of the transaction feed.
- `String` - *filter*, filter of the transaction feed.

#### Returns

none if the transaction feed is created success.

#### Example
```java
Client client = TestUtils.generateClient();
String filter = "asset_id='57fab05b689a2b8b6738cffb5cf6cffcd0bf6156a04b7d9ba0173e384fe38c8c' AND amount_lower_limit = 50 AND amount_upper_limit = 100";
String alias = "test";
new Transaction.Feed.Builder()
    .setAlias(alias)
    .setFilter(filter)
    .create(client);
```
```bash
// Result
//none
```

## get-transaction-feed

Query detail transaction feed by name.

#### Parameters

`Object`:

- `String` - *alias*, name of the transaction feed.

#### Returns

`Object`:

- `String` - *id*, id of the transaction feed.

- `String` - *alias*, name of the transaction feed.

- `String` - *filter*, filter of the transaction feed.

- `Object` - *param*, param of the transaction feed.
  - `String` - *assetid*, 资产id.
  - `Integer` - *lowerlimit*, the lower limit of asset amount.
  - `Integer` - *upperlimit*, the upper limit of asset amount.
  - `String` - *transtype*, type of transaction.

#### Example

list the available txfeed by alias:
```java
Client client = TestUtils.generateClient();
String alias = "test2";
Transaction.Feed transactionFeed = Transaction.Feed.getByAlias(client, alias);

Assert.assertNotNull(transactionFeed);
```
```bash
// Result
{"alias":"test2","filter":"asset_id\u003d\u002757fab05b689a2b8b6738cffb5cf6cffcd0bf6156a04b7d9ba0173e384fe38c8c\u0027 AND amount_lower_limit \u003d 50 AND amount_upper_limit \u003d 100","param":{"assetid":"57fab05b689a2b8b6738cffb5cf6cffcd0bf6156a04b7d9ba0173e384fe38c8c","lowerlimit":50,"upperlimit":100}}
```

## list-transaction-feeds

Returns the list of all available transaction feeds.

#### Parameters

none

#### Returns

- `Array of Object` , the transaction feeds.

  - `Object` :

    - `String` - *id*, id of the transaction feed.

    - `String` - *alias*, name of the transaction feed.

    - `String` - *filter*, filter of the transaction feed.

    - ` Object` - *param* , param of the transaction feed.
      - `String` - *assetid*, asset id.
      - `Integer` - *lowerlimit*, the lower limit of asset amount.
      - `Integer` - *upperlimit*, the upper limit of asset amount.
      - `String` - *transtype*, type of transaction.

#### Example

list all the available txfeed:
```java
Client client = TestUtils.generateClient();
List<Transaction.Feed> txFeedList = Transaction.Feed.list(client);
Assert.assertNotNull(txFeedList);
```
```bash
// Result
{"alias":"test1","filter":"asset_id\u003d\u002784778a666fe453cf73b2e8c783dbc9e04bc4fd7cbb4f50caeaee99cf9967ebed\u0027 AND amount_lower_limit \u003d 60 AND amount_upper_limit \u003d 80","param":{"assetid":"84778a666fe453cf73b2e8c783dbc9e04bc4fd7cbb4f50caeaee99cf9967ebed","lowerlimit":60,"upperlimit":80}}
{"alias":"test2","filter":"asset_id\u003d\u002757fab05b689a2b8b6738cffb5cf6cffcd0bf6156a04b7d9ba0173e384fe38c8c\u0027 AND amount_lower_limit \u003d 50 AND amount_upper_limit \u003d 100","param":{"assetid":"57fab05b689a2b8b6738cffb5cf6cffcd0bf6156a04b7d9ba0173e384fe38c8c","lowerlimit":50,"upperlimit":100}}
```

## delete-transaction-feed

Delete transaction feed by name.

#### Parameters

- `String` - *alias*, name of the transaction feed.

#### Returns

none if the transaction feed is deleted success.

#### Example
```java
Client client = TestUtils.generateClient();
String filter = "asset_id='57fab05b689a2b8b6738cffb5cf6cffcd0bf6156a04b7d9ba0173e384fe38c8c' AND amount_lower_limit = 50 AND amount_upper_limit = 100";
String alias = "test2";

Transaction.Feed.update(client, alias, filter);
```
```bash
// Result
update-transaction-feed successfully
```

## update-transaction-feed

Update transaction feed.

#### Parameters

- `String` - *alias*, name of the transaction feed.
- `String` - *filter*, filter of the transaction feed.

#### Returns

none if the transaction feed is updated success.

#### Example

deleted when the txfeed exists, and create it with alias and filter:
```java
Client client = TestUtils.generateClient();
String alias = "test2";
Transaction.Feed.deleteByAlias(client, alias);
```
```bash
// Result
delete-transaction-feed successfully
```
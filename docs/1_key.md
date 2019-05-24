---
id: key
title: Key API
sidebar_label: Bytom.Key.API
---

## create-key

It is to create private key essentially, returns the information of key. The private key is encrypted in the file and not visible to the user.

#### Parameters

- `String` - *alias*, name of the key.
- `String` - *password*, password of the key.

#### Returns

- `String` - *alias*, name of the key.

- `String` - *xpub*, root pubkey of the key.

- `String` - *file*, path to the file of key.
#### Example
```java
Client client = Client.generateClient();
String alias = "testJava1";
String password = "123456";
Key.Builder builder = new Key.Builder().setAlias(alias).setPassword(password);
Key key = Key.create(client, builder);
System.out.println(key);
```
```bash
// Result
Key{alias='testjava1', xpub='57011d2ed46aafe47c9c77f6f3b4cef95ba19474f50d918fefe71a675ac15413c8e733ff6581b311d89bbfb5fedc34de4e7f6aedf2f5ac1f1b56cedc5a23ece9', file='C:\Users\mumu\AppData\Roaming\Bytom\keystore\UTC--2019-04-23T07-19-41.724077700Z--532f7a7a-86d7-44c5-b624-c547be0bd050'}
```
## list-keys

Returns the list of all available keys.

#### Parameters

none

#### Returns

- `Array of Object` , keys owned by the client.
  - `object` :
    - `String`  - *alias*, name of the key.
    - `String` - *xpub*, pubkey of the key.
#### Example
```java
Client client = Client.generateClient();
List<Key> keyList = Key.list(client);
```
```bash
// Result
1    INFO  [2019-04-23 16:05:00]  list-key:
2    INFO  [2019-04-23 16:05:00]  size of key:3
3    INFO  [2019-04-23 16:05:00]  [Key{alias='alice', xpub='872e6fbe0ad47b0ff6435bcc4c18fd0c00631afe6c4433938fd7059f32d9c26bb888d0f112cbc07880a1d9ef50111154fa34570233bda070503f6fbe94daf974', file='C:\Users\mumu\AppData\Roaming\Bytom\keystore\UTC--2019-04-04T01-40-00.441340200Z--653ae5ff-84d2-4949-9784-28ca70809f58'}, Key{alias='bob', xpub='4874e557e062778cba85825064f41e2ca0f61478a1469df0eb5ea35d457de5c317a0520f672cbd98186cf5d26f823d93d926f6383db54bae7fcc92ff975b2215', file='C:\Users\mumu\AppData\Roaming\Bytom\keystore\UTC--2019-04-04T07-56-42.134038700Z--13a3e5cb-0fce-46ed-a845-9b6d2380dab9'}, Key{alias='testjava1', xpub='57011d2ed46aafe47c9c77f6f3b4cef95ba19474f50d918fefe71a675ac15413c8e733ff6581b311d89bbfb5fedc34de4e7f6aedf2f5ac1f1b56cedc5a23ece9', file='C:\Users\mumu\AppData\Roaming\Bytom\keystore\UTC--2019-04-23T07-19-41.724077700Z--532f7a7a-86d7-44c5-b624-c547be0bd050'}]
```

## delete-key
Delete existed key, please make sure that there is no balance in the related accounts.
#### Parameters
- `String` - *xpub*, pubkey of the key.
- `String` - *password*, password of the key.
#### Returns
none if the key is deleted successfully.
#### Example
```java
Client client = Client.generateClient();
List<Key> keyList = Key.list(client);
String xpub = keyList.get(keyList.size()-1).xpub;
//Delete the last key.
Key.delete(client, xpub, "123456");
```
```bash
// Result
INFO  [2019-04-23 16:25:52]  delete-key successfully.
```
##  reset-key-password

Reset key password.

#### Parameters

- `String` - *xpub*, pubkey of the key.
- `String` - *old_password*, old password of the key.
- `String` - *new_password*, new password of the key.

#### Returns

- `Boolean` - *changed*, result of reset key password, true is reset successfully, otherwise is false.

#### Example
```java
Client client = Client.generateClient();
List<Key> keyList = Key.list(client);
String xpub = keyList.get(keyList.size()-1).xpub;
Key.resetPassword(client, xpub, "123456", "123456789");
```
```bash
// Result
//none
```
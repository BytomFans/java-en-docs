---
id: access_token
title: Access_token API
sidebar_label: Bytom.Access_token.API
---

## create-access-token

Create access token, it provides basic access authentication for HTTP protocol, returns token contain username and password, they are separated by a colon.

#### Parameters

- `String` - *id*, token ID.

optional:

- `String` - *type*, type of token.

#### Returns

- `String` - *token*, access token, authentication username and password are separated by a colon.
- `String` - *id*, token ID.
- `String` - *type*, type of token.
- `Object` - *created_at*, time to create token.

#### Example
```java
Client client = TestUtils.generateClient();
AccessToken accessToken = new AccessToken.Builder().setId("token1").create(client);
```
```bash
// Result
{
  "token": "token1:1fee70f537128a201338bd5f25a3adbf33dad02eae4f4c9ac43f336a069df8f3",
  "id": "token1",
  "created_at": "2019-04-24T16:57:08.7091984+08:00"
}
```

## list-access-tokens

Returns the list of all available access tokens.

#### Parameters

none

#### Returns

- `Array of Object`, access token array.
  - `Object`:
    - `String` - *token*, access token.
    - `String` - *id*, token ID.
    - `String` - *type*, type of token. 
    - `Object` - *created_at*, time to create token.

#### Example

list all the available access tokens.
```java
Client client = TestUtils.generateClient();
List<AccessToken> tokenList = AccessToken.list(client);
```
```bash
// Result
[
  {
    "token": "token1:1fee70f537128a201338bd5f25a3adbf33dad02eae4f4c9ac43f336a069df8f3",
    "id": "token1",
    "created_at": "2018-03-20T18:56:01.043919771+08:00"
  },
  {
    "token": "alice:78598c6d9fb9e3258d01f78005d4e5725ad0d45e20af90a30b577b407d4a2edd",
    "id": "alice",
    "created_at": "2018-03-20T18:56:01.043919771+08:00"
  }
]
```

## delete-access-token

Delete existed access token.

#### Parameters

`Object`:

- `String` - *id*, token ID.

#### Returns

none if the access token is deleted successfully.

#### Example

delete access token.
```java
Client client = TestUtils.generateClient();
String secret = "1fee70f537128a201338bd5f25a3adbf33dad02eae4f4c9ac43f336a069df8f3";
AccessToken.delete(client, "token1", secret);
```
```bash
// Result
//none
```


## check-access-token

Check access token is valid.

#### Parameters

`Object`:

- `String` - *id*, token ID.
- `String` - *secret*, secret of token, the second part of the colon division for token.

#### Returns

none if the access token is checked valid.

#### Example

check whether the access token is vaild or not.
```java
Client client = TestUtils.generateClient();
String secret = "1fee70f537128a201338bd5f25a3adbf33dad02eae4f4c9ac43f336a069df8f3";
AccessToken.check(client, "token1", secret);
```
```bash
// Result
//none
```
---
id: message
title: Message API
sidebar_label: Bytom.Message.API
---

## sign-message

Sign a message with the key password(decode encrypted private key) of an address.

#### Parameters

- `String` - *address*, address for account.
- `String` - *message*, message for signature by address xpub.
- `String` - *password*, password of account.

#### Returns

- `String` - *derived_xpub*, derived xpub.
- `String` - *signature*, signature of message.

#### Example
```java
Client client = TestUtils.generateClient();
Message message = new Message.SignBuilder()
    .setAddress("bm1qx2qgvvjz734ur8x5lpfdtlau74aaa5djs0a5jn")
    .setMessage("test")
    .setPassword("123456")
    .sign(client);
Assert.assertNotNull(message);
```
```bash
// Result
{
  "signature": "74da3d6572233736e3a439166719244dab57dd0047f8751b1efa2da26eeab251d915c1211dcad77e8b013267b86d96e91ae67ff0be520ef4ec326e911410b609",
  "derived_xpub": "6ff8c3d1321ce39a3c3550f57ba70b67dcbcef821e9b85f6150edb7f2f3f91009e67f3075e6e76ed5f657ee4b1a5f4749b7a8c74c8e7e6a1b0e5918ebd5df4d0"
}
```

##  verify-message

Verify a signed message with derived pubkey of the address.

#### Parameters


- `String` - *address*, address for account.
- `String` - *derived_xpub*, derived xpub.
- `String` - *message*, message for signature by derived_xpub.
- `String` - *signature*, signature for message.

#### Returns

`Object`:

- `Boolean` - *result*, verify result.

#### Example
```java
Client client = TestUtils.generateClient();
String derived_xpub = "6e1efce70e2b29efa348aec7c148edc2beb72edc0d4422a03cfb0f40e6e4cfc6e6050b5863bbe84c44131280dff68614e0308a4d081e8b677d0f7f09fb3390c4";
String signature = "0d840d5b6a6df028013260e94e871c1443686c446a65db4ee93005c5395c3607feb0ac5bf583a3139c8a3d0afe757448ff49fa17ffd2377831ce5f925c846b0b";

Boolean verify = new Message.VerifyBuilder()
    .setDerivedXpub(derived_xpub)
    .setSignature(signature)
    .setAddress("bm1qx2qgvvjz734ur8x5lpfdtlau74aaa5djs0a5jn")
    .setMessage("test")
    .verifyMessage(client);
```
```bash
// Result
{
  "result": true
}
```


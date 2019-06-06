---
id: start
title: quick start
sidebar_label: SDK installation
---

## Installation

There are various ways to install and use this sdk. We'll provide three ways to get it. Note that the bytom-sdk requires JAVA 7 or newer.

### Apache Maven

```xml
<dependency>
    <groupId>io.bytom</groupId>
    <artifactId>java-sdk</artifactId>
    <version>1.0.0</version>
</dependency>
```

#### Gradle/Grails

```bash
compile 'io.bytom:bytom-sdk:1.0.1'
```

#### Building from source code

To clone, compile, and install in your local maven repository (or copy the artifacts from the target/ directory to wherever you need them):

```bash
git clone https://github.com/Bytom/bytom-java-sdk.git
cd java-sdk
mvn install -Dmaven.test.skip=true
```

## Usage

### Usage examples

```java
public static Client generateClient() throws BytomException {
    String coreURL = Configuration.getValue("bytom.api.url");
    String accessToken = Configuration.getValue("client.access.token");
    if (coreURL == null || coreURL.isEmpty()) {
        coreURL = "http://127.0.0.1:9888/";
    }
    return new Client(coreURL, accessToken);
}
```

Create a key

```java
import io.bytom.api.Key;
import io.bytom.http.Client;

public class Main {
    public static void main(String[] args) throws Exception {
        Client client = Client.generateClient();
        String alias = "testJava1";
        String password = "123456";
        Key.Builder builder = new Key.Builder().setAlias(alias).setPassword(password);
        Key key = Key.create(client, builder);
        System.out.println(key);
    }
}
```

Returns:

```bash
Key{alias='testjava1', xpub='57011d2ed46aafe47c9c77f6f3b4cef95ba19474f50d918fefe71a675ac15413c8e733ff6581b311d89bbfb5fedc34de4e7f6aedf2f5ac1f1b56cedc5a23ece9', file='C:\Users\mumu\AppData\Roaming\Bytom\keystore\UTC--2019-04-23T07-19-41.724077700Z--532f7a7a-86d7-44c5-b624-c547be0bd050'}
```

###  All usage examples

For more details you can see [doc](1_key.md)

## Support and Feedback

If you find a bug, please submit the issue in Github directly by using [Issues](https://github.com/Bytom/bytom-java-sdk/issues)

## license

[Bytom JAVA SDK is based on the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0.txt) protocol.


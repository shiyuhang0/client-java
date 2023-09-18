[![Maven Central](https://img.shields.io/maven-central/v/org.tikv/tikv-client-java.svg?label=Maven%20Central)](https://search.maven.org/search?q=g:%22org.tikv%22%20AND%20a:%22tikv-client-java%22)
[![Slack](https://img.shields.io/badge/chat-on%20Slack-brightgreen.svg)](https://slack.tidb.io/invite?team=tikv-wg&channel=client)
[![codecov](https://codecov.io/gh/tikv/client-java/branch/master/graph/badge.svg?token=nSAjGaN0EH)](https://codecov.io/gh/tikv/client-java)

## TiKV JAVA Client


A Java client for [TiKV](https://github.com/tikv/tikv).
It is supposed to:
+ Communicate via [gRPC](http://www.grpc.io/)
+ Talk to Placement Driver searching for a region
+ Talk to TiKV for reading/writing data

## Quick Start

> TiKV Java Client is designed to communicate with [PD](https://github.com/tikv/pd) and [TiKV](https://github.com/tikv/tikv), please run PD and TiKV in advance.

Build Java client from source file:

```sh
mvn clean install -Dmaven.test.skip=true
```

Add maven dependency to `pom.xml`:

```xml
<dependency>
	<groupId>org.tikv</groupId>
	<artifactId>tikv-client-java</artifactId>
	<version>3.3.0</version>
</dependency>
```

Create a transactional `KVClient` and communicates with TiKV:

```java
import org.tikv.common.TiConfiguration;
import org.tikv.common.TiSession;
import org.tikv.txn.KVClient;

public class Main {
	public static void main(String[] args) throws Exception {
		TiConfiguration conf = TiConfiguration.createDefault(YOUR_PD_ADDRESSES);
		TiSession session = TiSession.create(conf);
		KVClient client = session.createKVClient();
	}
}
```

Or create a `RawKVClient` if you don't need the transaction semantic:

```java
import org.tikv.common.TiConfiguration;
import org.tikv.common.TiSession;
import org.tikv.raw.RawKVClient;

public class Main {
	public static void main(String[] args) throws Exception {
		TiConfiguration conf = TiConfiguration.createRawDefault(YOUR_PD_ADDRESSES);
		TiSession session = TiSession.create(conf);
		RawKVClient client = session.createRawClient();
	}
}
```

Find more demo in [TiKV Java Client User Documents](https://tikv.github.io/client-java/examples/introduction.html)

## Documentation

See [Java Client Documents](/docs/README.md) for references about how to config and monitor Java Client.

A [Maven site](https://tikv.github.io/client-java/site) is also available. It includes:
1. [API reference](https://tikv.github.io/client-java/site/apidocs/index.html)
2. [Spotbugs Reports](https://tikv.github.io/client-java/site/spotbugs.html)
3. [Source Code Xref](https://tikv.github.io/client-java/site/xref/index.html)

## Community

### Forum

- User forum: [AskTUG](https://asktug.com/)
- Contributor forum: [https://internals.tidb.io/](https://internals.tidb.io/)

### Contribute to TiKV Java Client

See [Contribution Guide](https://tikv.github.io/client-java/contribution/introduction.html) for references about how to contribute to this project.

## License

Apache 2.0 license. See the [LICENSE](./LICENSE) file for details.

管理Milvus连接
==========

本主题介绍了如何连接和断开Milvus服务器。

 Ensure to connect to a Milvus server before any operations.

Milvus支持两个端口，端口`19530`和端口`9091`：

* 端口`19530`是用于gRPC的。当您使用不同的Milvus SDK连接到Milvus服务器时，它是默认端口。

* 端口`9091`是用于RESTful API的。当您使用HTTP客户端连接到Milvus服务器时，它被使用。

以下示例连接到主机为`localhost`，端口为`19530`或`9091`的Milvus服务器，并断开连接。如果连接被拒绝，请尝试取消对应端口的阻止。

连接到Milvus服务器
------------

构建Milvus连接。在进行任何操作之前，请确保连接到Milvus服务器。

[Python](#python)
[Java](#java)
[GO](#go)
[Node.js](#javascript)
[CLI](#shell)
[Curl](#curl)

```
# Run `python3` in your terminal to operate in the Python interactive mode.
from pymilvus import connections
connections.connect(
  alias="default",
  user='username',
  password='password',
  host='localhost',
  port='19530'
)

```

```
import { MilvusClient } from "@zilliz/milvus2-sdk-node";
const address = "localhost:19530";
const username = "username";
const password = "password";
const ssl = false;
const milvusClient = new MilvusClient({address, ssl, username, password});

```

```
milvusClient, err := client.NewGrpcClient(
  context.Background(), // ctx
  "localhost:19530",    // addr
)
if err != nil {
  log.Fatal("failed to connect to Milvus:", err.Error())
}

```

```
final MilvusServiceClient milvusClient = new MilvusServiceClient(
  ConnectParam.newBuilder()
    .withHost("localhost")
    .withPort(19530)
    .build()
);

```

```
connect -h localhost -p 19530 -a default

```

```
curl localhost:9091/api/v1/health
{"status":"ok"}

```

| Parameter | Description |
| --- | --- |
| `alias` | Alias of the Milvus connection to construct. |
| `user` | Username of the Milvus server. |
| `password` | Password of the username of the Milvus server. |
| `host` | IP address of the Milvus server. |
| `port` | Port of the Milvus server. |

| Parameter | Description |
| --- | --- |
| `address` | Address of the Milvus connection to construct. |
| `username` | The username used to connect to Milvus. |
| `password` | The password used to connect to Milvus. |
| `ssl` | SSL connection. It is false by default. |

| Parameter | Description |
| --- | --- |
| `ctx` | Context to control API invocation process. |
| `addr` | Address of the Milvus connection to construct. |

| Parameter | Description |
| --- | --- |
| `Host` | IP address of the Milvus server. |
| `Port` | Port of the Milvus server. |

| Option | Description |
| --- | --- |
| -h (Optional) | The host name. The default is "127.0.0.1". |
| -p (Optional) | The port number. The default is "19530". |
| -a (Optional) | The alias name of the Milvus link. The default is "default". |
| -D (Optional) | Flag to disconnect from the Milvus server specified by an alias. The default alias is "default". |

### 返回

通过传递的参数创建的Milvus连接。

### Raises

* **NotImplementedError**: 如果连接参数中的处理程序不是GRPC，则会引发此错误。

* **ParamError**: 如果连接参数中的池不受支持，则会引发此错误。

* **Exception**: 如果参数中指定的服务器未准备就绪，则无法连接到服务器。

从Milvus服务器断开连接
--------------

从Milvus服务器断开连接。

[Python](#python) 
[Java](#java)
[GO](#go)
[Node.js](#javascript)
[CLI](#shell)
[Curl](#curl)

```
connections.disconnect("default")

```

```
await milvusClient.closeConnection();

```

```
milvusClient.Close()

```

```
milvusClient.close()

```

```
connect -D

```

```
# Close your HTTP client connection.

```

| Parameter | Description |
| --- | --- |
| `alias` | Alias of the Milvus server to disconnect from. |

限制
--

最大连接数为65,536。

接下来是什么
------

连接到 Milvus 服务器后，您可以：

* [创建集合](create_collection.md)

* [管理数据](insert_data.md)

* [构建向量索引](build_index.md)

* [进行向量搜索](search.md)

* [进行混合搜索](hybridsearch.md)
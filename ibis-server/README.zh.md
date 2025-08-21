# Ibis Server 模块

该模块是 Wren Engine 的 API 服务器。它基于 [FastAPI](https://fastapi.tiangolo.com/) 构建，提供了多个用于 SQL 查询的 API。SQL 查询将由 [wren-core](../wren-core/) 进行规划，由 [sqlglot](https://github.com/tobymao/sqlglot) 进行转译，然后由 [ibis](https://github.com/ibis-project/ibis) 执行以查询数据库。

## 快速入门

### 在 Docker 上运行 Ibis Server

您可以按照以下步骤运行 Java 引擎和 ibis。

> Wren Engine 正在迁移到 [wren-core](../wren-core/)。但是，我们仍然建议启动 [Java 引擎](../wren-core-legacy/)以启用查询回退机制。

创建 `compose.yaml` 文件并添加以下内容，如果需要，请编辑环境变量（请参阅环境变量）。

```yaml
services:
  ibis:
    image: ghcr.io/canner/wren-engine-ibis:latest
    ports:
      - "8000:8000"
    environment:
      - WREN_ENGINE_ENDPOINT=http://java-engine:8080
  java-engine:
    image: ghcr.io/canner/wren-engine:latest
    expose:
      - "8080"
    volumes:
      - ./etc:/usr/src/app/etc
```

创建 `etc` 目录并在其中创建 `config.properties` 文件

```bash
mkdir etc
cd etc
vim config.properties
```

将以下内容添加到 `config.properties` 文件中

```bash
node.environment=production
```

运行 docker compose

```bash
docker compose up
```

设置 OpenTelemetry 环境变量以启用追踪日志。
请参阅使用 Jaeger 进行追踪以启动 Jaeger 服务器。

### 在本地运行 Ibis Server

要求：

- Python 3.11
- casey/just
- poetry
- Rust 和 Cargo

克隆仓库

```bash
git clone git@github.com:Canner/wren-engine.git
```

为查询重写功能启动 Java 引擎

```bash
cd example
docker compose --env-file .env up
```

导航到 `ibis-server` 目录

```bash
cd ibis-server
```

创建 `.env` 文件并填写环境变量（请参阅环境变量）

```bash
vim .env
```

安装依赖项

```bash
just install
```

运行服务器

```bash
just run
```

### 使用 Python 交互模式启动

安装依赖项

```bash
just install
```

使用以下命令启动一个带有活动 Wren 会话的 CLI：

```
python -m wren local_file <mdl_path> <connection_info_path>
```

这将创建一个交互式 CLI 环境，其中包含一个用于查询数据库的 `wren.session.Context` 实例。

```
会话已创建: Context(id=1352f5de-a8a7-4342-b2cf-015dbb2bba4f, data_source=local_file)
您现在可以使用 'wren' 变量与 Wren 会话进行交互：
> task = wren.sql('SELECT * FROM your_table').execute()
> print(task.results)
> print(task.formatted_result())
Python 3.11.11 (main, Dec  3 2024, 17:20:40) [Clang 16.0.0 (clang-1600.0.26.4)] on darwin
键入 "help"、"copyright"、"credits" 或 "license" 以获取更多信息。
(InteractiveConsole)
>>>
```

### 使用 Jupyter Notebook 启动

使用 Docker 启动一个带有 Wren 引擎依赖的 Jupyter notebook 服务器：

```
docker run --rm -p 8888:8888 ghcr.io/canner/wren-engine-ibis:latest jupyter
```

浏览示例 notebook 以了解如何使用 Wren 会话上下文：

```
http://localhost:8888/lab/doc/tree/notebooks/demo.ipynb
```

### 启用追踪

我们使用 OpenTelemetry 作为其追踪框架。请参考 OpenTelemetry 零代码检测来安装所需的依赖项。
然后，使用以下 just 命令启动 Ibis 服务器，它会将追踪日志导出到控制台：

```
just run-trace-console
```

OpenTelemetry 零代码检测是高度可配置的。您可以设置必要的导出器将追踪数据发送到您的追踪服务。

我们目前正在追踪的指标

### 使用 Jaeger 进行追踪

- 遵循 Jaeger 官方文档 在容器中启动 Jaeger。使用以下命令：

```
docker run --rm --name jaeger \
  -p 16686:16686 \
  -p 4317:4317 \
  -p 4318:4318 \
  -p 5778:5778 \
  -p 9411:9411 \
  jaegertracing/jaeger:2.5.0
```

- 安装 OpenTelemetry Python 零代码检测

```
pip install opentelemetry-distro opentelemetry-exporter-otlp
opentelemetry-bootstrap -a install
```

- 使用以下 `just` 命令启动 `ibis-server` 并将追踪日志导出到 Jaeger：

```
just run-trace-otlp
```

- 在 http://localhost:16686 打开 Jaeger UI 以查看您请求的追踪日志。

## 贡献

更多信息请参阅 CONTRIBUTING.md。

### 报告迁移问题

Wren 引擎正在迁移到 v3 API（由 Rust 和 DataFusion 提供支持）。但是，目前存在一些 SQL 问题。
如果您在日志中发现迁移消息，我们希望您能将该消息和相关信息提供给 Wren AI 团队。
只需在 GitHub 上提出一个 issue 或在我们的 Discord 频道中联系我们。

该消息将类似于以下日志：

```
2025-03-19 22:49:08.788 | [62781772-7120-4482-b7ca-4be65c8fda96] | INFO     | __init__.dispatch:14 - POST /v3/connector/postgres/query
2025-03-19 22:49:08.788 | [62781772-7120-4482-b7ca-4be65c8fda96] | INFO     | __init__.dispatch:15 - Request params: {}
2025-03-19 22:49:08.789 | [62781772-7120-4482-b7ca-4be65c8fda96] | INFO     | __init__.dispatch:22 - Request body: {"connectionInfo":"REDACTED","manifestStr":"eyJjYXRhbG9nIjoid3JlbiIsInNjaGVtYSI6InB1YmxpYyIsIm1vZGVscyI6W3sibmFtZSI6Im9yZGVycyIsInRhYmxlUmVmZXJlbmNlIjp7InNjaGVtYSI6InB1YmxpYyIsIm5hbWUiOiJvcmRlcnMifSwiY29sdW1ucyI6W3sibmFtZSI6Im9yZGVya2V5IiwidHlwZSI6InZhcmNoYXIiLCJleHByZXNzaW9uIjoiY2FzdChvX29yZGVya2V5IGFzIHZhcmNoYXIpIn1dfV19","sql":"SELECT orderkey FROM orders LIMIT 1"}
2025-03-19 22:49:08.804 | [62781772-7120-4482-b7ca-4be65c8fda96] | WARN    | connector.query:61 - 执行 v3 查询失败，回退到 v2：DataFusion 错误：ModelAnalyzeRule
由...引起
Schema 错误：没有名为 o_orderkey 的字段。
Wren 引擎正在迁移到 Rust 版本。如果您能为我们提供错误消息和相关日志，Wren AI 团队将不胜感激。
```

#### 报告问题的步骤

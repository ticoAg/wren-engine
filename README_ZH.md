<p align="center">
  <a href="https://getwren.ai">
    <picture>
      <source media="(prefers-color-scheme: light)" srcset="./misc/wrenai_logo.png">
      <img src="./misc/wrenai_logo.png">
    </picture>
    <h1 align="center">Wren Engine</h1>
  </a>
</p>

<p align="center">
  <a aria-label="关注我们" href="https://x.com/getwrenai">
    <img alt="" src="https://img.shields.io/badge/-@getwrenai-blue?style=for-the-badge&logo=x&logoColor=white&labelColor=gray&logoWidth=20">
  </a>
  <a aria-label="许可证" href="https://github.com/Canner/wren-engine/blob/main/LICENSE">
    <img alt="" src="https://img.shields.io/github/license/canner/wren-engine?color=blue&style=for-the-badge">
  </a>
  <a aria-label="加入社区" href="https://discord.gg/5DvshJqG8Z">
    <img alt="" src="https://img.shields.io/badge/-加入社区-blue?style=for-the-badge&logo=discord&logoColor=white&labelColor=grey&logoWidth=20">
  </a>
  <a aria-label="Canner" href="https://cannerdata.com/">
    <img src="https://img.shields.io/badge/%F0%9F%A7%A1-由Canner制作-blue?style=for-the-badge">
  </a>
</p>

> Wren Engine 是 MCP 客户端和 AI Agent 的语义引擎。
> [Wren AI](https://github.com/Canner/WrenAI) GenBI AI Agent 基于 Wren Engine 构建。

<img src="./misc/wren_engine_overview.png">

## 🔌 支持的数据源
- [BigQuery](https://docs.getwren.ai/oss/wren_engine_api#tag/BigQueryConnectionInfo)
- [Google Cloud Storage](https://docs.getwren.ai/oss/wren_engine_api#tag/GcsFileConnectionInfo)
- [本地文件](https://docs.getwren.ai/oss/wren_engine_api#tag/LocalFileConnectionInfo)
- [MS SQL Server](https://docs.getwren.ai/oss/wren_engine_api#tag/MSSqlConnectionInfo)
- [Minio](https://docs.getwren.ai/oss/wren_engine_api#tag/MinioFileConnectionInfo)
- [MySQL Server](https://docs.getwren.ai/oss/wren_engine_api#tag/MySqlConnectionInfo)
- [Oracle Server](https://docs.getwren.ai/oss/wren_engine_api#tag/OracleConnectionInfo)
- [PostgreSQL Server](https://docs.getwren.ai/oss/wren_engine_api#tag/PostgresConnectionInfo)
- [Amazon S3](https://docs.getwren.ai/oss/wren_engine_api#tag/S3FileConnectionInfo)
- [Snowflake](https://docs.getwren.ai/oss/wren_engine_api#tag/SnowflakeConnectionInfo)
- [Trino](https://docs.getwren.ai/oss/wren_engine_api#tag/TrinoConnectionInfo)

## 😫 当前挑战

在企业层面，风险和复杂性要高得多。企业的业务运行在存储于云仓库、关系数据库和安全文件系统中的结构化数据上。从 BI 仪表板到 CRM 更新和合规工作流，AI 不仅需要执行命令，还必须**准确理解并检索正确的数据，并具有上下文**。

虽然许多社区和官方的 MCP 服务器已经支持连接到 PostgreSQL、MySQL、SQL Server 等主要数据库，但存在一个问题：**仅访问原始数据是不够的**。

企业需要：
- 对其数据模型的准确语义理解
- 报告中可信的计算和聚合
- 明确的业务术语，如"活跃客户"、"净收入"或"流失率"
- 基于用户的权限和访问控制

仅靠自然语言不足以驱动企业数据系统中的复杂工作流。您需要一个层来解释意图，将其映射到正确的数据，准确应用计算，并确保安全性。

## 🎯 我们的使命

<img src="./misc/mcp_wren_engine.webp">

Wren Engine 通过模型上下文协议 (MCP) —— 一种将大语言模型与工具、数据库和企业系统连接的新开放标准，致力于推动 MCP 客户端和 AI Agent 的未来发展。

作为 MCP 生态系统的一部分，Wren Engine 提供了一个**语义引擎**，由下一代语义层驱动，使 AI Agent 能够准确、有上下文和有治理地访问业务数据。

通过将语义层直接构建到 MCP 客户端中，如 Claude、Cline、Cursor 等。Wren Engine 为 AI Agent 提供精确的业务上下文，并确保在各种企业环境中准确的数据交互。

我们相信企业 AI 的未来在于**具有上下文感知的可组合系统**。这就是为什么 Wren Engine 被设计为：

- 🔌 **可嵌入**任何 MCP 客户端或 AI Agent 工作流
- 🔄 **可互操作**与现代数据堆栈 (PostgreSQL、MySQL、Snowflake 等)
- 🧠 **语义优先**，使 AI 能够"理解"您的数据模型和业务逻辑
- 🔐 **治理就绪**，尊重角色、访问控制和定义

通过 Wren Engine，您可以跨团队扩展 AI 应用 —— 不仅通过更好的自动化，而且通过更好的理解。

***查看我们的完整文章***

🤩 [我们的使命 - 推动下一代 AI Agent：为未来 MCP 客户端和企业数据访问构建基础](https://getwren.ai/post/fueling-the-next-wave-of-ai-agents-building-the-foundation-for-future-mcp-clients-and-enterprise-data-access)

## 🚀 MCP 入门
[MCP Server README](mcp-server/README.md)

https://github.com/user-attachments/assets/dab9b50f-70d7-4eb3-8fc8-2ab55dc7d2ec

👉 博客教程：[通过模型上下文协议 (MCP) 使用 Wren Engine 和 Zapier 驱动 AI 工作流](https://getwren.ai/post/powering-ai-driven-workflows-with-wren-engine-and-zapier-via-the-model-context-protocol-mcp?utm_campaign=10904457-MCP&utm_content=330804773&utm_medium=social&utm_source=linkedin&hss_channel=lcp-89794921)

## 🤔 概念

- [使用 Apache DataFusion 为 AI Agent 提供语义 SQL 支持](https://getwren.ai/post/powering-semantic-sql-for-ai-agents-with-apache-datafusion)
- [Wren Engine 快速入门](https://docs.getwren.ai/oss/engine/get_started/quickstart)
- [什么是语义？](https://docs.getwren.ai/oss/engine/concept/what_is_semantics)
- [什么是建模定义语言 (MDL)？](https://docs.getwren.ai/oss/engine/concept/what_is_mdl)
- [Wren Engine 与大语言模型的优势](https://docs.getwren.ai/oss/engine/concept/benefits_llm)

## 🚧 项目状态
Wren Engine 目前处于测试版。项目团队正在积极开发中，目标是至少每两周发布一次新版本。

## 🛠️ 开发者指南
项目由 4 个主要模块组成：
1. [ibis-server](./ibis-server/)：由 FastAPI 和 Ibis 驱动的 Wren Engine Web 服务器
2. [wren-core](./wren-core)：由 [Apache DataFusion](https://github.com/apache/datafusion) 驱动的 Rust 编写的语义核心
3. [wren-core-py](./wren-core-py)：wren-core 的 Python 绑定
4. [mcp-server](./mcp-server/)：由 [MCP Python SDK](https://github.com/modelcontextprotocol/python-sdk) 驱动的 Wren Engine MCP 服务器

## ⭐️ 社区

- 欢迎加入我们的 [Discord 服务器](https://discord.gg/5DvshJqG8Z) 提供反馈！
- 如有任何问题，请访问 [Github Issues](https://github.com/Canner/wren-engine/issues)。
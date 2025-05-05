---
keywords: Experience Platform；查询；查询服务；故障排除；护栏；指南；限制；
title: 查询服务的护栏
description: 本文档提供有关查询服务数据使用限制的信息，以帮助您优化查询使用。
exl-id: 1ad5dcf4-d048-49ff-97e3-07040392b65b
source-git-commit: 23c7a4590b365a49edb066567b6ebe2ac08c67e8
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 2%

---

# 查询服务的护栏

护栏是引导数据和系统使用、性能优化、避免Adobe Experience Platform中出现错误或意外结果的阈值。
本文档提供了查询服务数据的默认使用限制，以帮助您在查询与您的许可权利相关的数据时优化系统性能。

>[!IMPORTANT]
>
>除了此护栏页面外，还检查销售订单中的许可证授权和相应的[产品描述](https://helpx.adobe.com/cn/legal/product-descriptions.html)中的实际使用限制。

## 先决条件

在继续阅读本文档之前，您应该对关键查询服务的定义和功能有深入的了解。 如下所述：

* **临时查询**：用于执行`SELECT`个查询以探索、试验并验证数据，其中查询&#x200B;**的结果未存储在数据湖上**。

* **批处理查询**：用于执行`INSERT TABLE AS SELECT`和`CREATE TABLE AS SELECT`查询以清理、形状、操作和扩充数据。 这些查询的结果&#x200B;**存储在数据湖中**。 用于测量此功能消耗的量度是计算小时数。

* **查询服务用户**：在您当前许可证内提供的Customer Journey Analytics、Adobe Real-Time Customer Data Platform和/或Adobe Journey Optimizer的查询服务用户也可以与Data Distiller一起使用。 查询服务用户在功能之间共享。

* **临时用户**：临时用户是执行临时查询的用户。

* **批处理用户**：批处理用户是执行批处理查询的用户。

* **报表API**：用于执行数据提取调用（内部或外部）的API。 扩展报表数据模型源自Adobe Experience Platform中的本机报表数据模型，如Real-Time CDP功能板数据模型。

## 护栏类型

此文档有两种类型的默认限制：

| 护栏类型 | 描述 |
|----------|---------|
| **性能护栏（软限制）** | 性能护栏是与用例范围相关的使用限制。 当超出性能护栏时，您可能会遇到性能下降和延迟问题。 Adobe不对此类性能下降负责。 始终超过性能护栏的客户可以选择许可额外的容量，以避免性能下降。 |
| **系统强制的护栏（硬限制）** | Real-Time CDP UI或API强制实施系统强制的护栏。 这些限制不得超过，因为UI和API将阻止您这样做或您会返回错误。 |

{style="table-layout:auto"}

>[!NOTE]
>
>本文档中概述的默认限制不断得到改进。 请定期查看以获取最新信息。

## 主要实体性能护栏

下表提供了在使用特定查询模式时用于查询执行的建议护栏限制和描述。

**临时查询**

| 护栏 | 限制 | 限制类型 | 描述 |
|---|---|---|---|
| 最长执行时间 | 10 分钟 | 系统强制的护栏 | 这会定义临时SQL查询的最大输出时间。 超过返回结果的时间限制会引发错误代码53400。 |
| 并发查询服务用户 | <ul><li>在应用程序产品描述中指定。</li><li>+5（每购买一个额外的Ad hoc query用户附加组件包）</li></ul> | 系统强制的护栏 | 这定义了可以为特定组织同时创建会话的用户数量。 如果超过并发限制，用户将收到`Session Limit Reached`错误。 |
| 查询并发 | <ul><li>在应用程序产品描述中指定。</li><li>+1（每购买一个额外的Ad hoc query用户附加SKU包）</li></ul> | 系统强制的护栏 | 这定义可以为特定组织同时执行多少个查询。 如果超过并发限制，查询将排入队列。 |
| 客户端连接器和结果输出限制 | 客户端连接器<ul><li>查询UI（100行）</li><li>第三方客户端(50,000)</li><li>[!DNL PostgresSQL]客户端(50,000)</li></ul> | 系统强制的护栏 | 可通过以下方式接收查询结果：<ul><li>查询服务UI</li><li>第三方客户端</li><li>[!DNL PostgresSQL]客户端</li></ul>注意：对输出计数添加限制可能会更快地返回结果。 例如，`LIMIT 5`、`LIMIT 10`等。 |
| 通过以下方式返回的结果 | 客户端用户界面 | 不适用 | 这会定义如何将结果提供给用户。 |

{style="table-layout:auto"}

**批处理查询**

| **护栏** | **限制** | **限制类型** | **描述** |
|---|---|---|---|
| 最长执行时间 | 24 小时 | 系统强制的护栏 | 这会定义批处理SQL查询的最大执行时间。<br>查询的处理时间取决于要处理的数据量和查询的复杂性。 |
| 未计划批的并发查询服务用户 | <ul><li>在应用程序产品描述中指定。</li><li>+5（每购买一个额外的Ad hoc query用户附加组件包）</li></ul> | 系统强制的护栏 | 对于未计划的批处理查询（例如，在交互模式下的CTAS/ITAS查询），这将定义有多少用户可以同时为特定组织创建会话。 如果超过并发限制，用户将收到`Session Limit Reached`错误。 |
| 计划批的并发查询服务用户 | 无用户限制 | 不适用 | 计划的批处理查询是异步作业，因此没有用户限制。 |
| 批量数据处理所需的计算时间 | 如客户的Adobe Experience Platform Intelligence查询自定义SKU销售订单中所指定 | 性能护栏 | 这定义了客户每年在执行批处理查询以扫描、处理数据并将其写回数据湖时允许的计算时间范围。 |
| 查询并发 | 支持 | 不适用 | 计划的批处理查询是异步作业，因此支持并发查询。 |
| 客户端连接器和结果输出限制 | 客户端连接器<ul><li>查询UI（对行没有上限）</li><li>第三方客户端（行数没有上限）</li><li>[!DNL PostgresSQL]客户端（行数没有上限）</li><li>REST API（行数没有上限）</li></ul> | 系统强制的护栏 | 可以使用以下方法使查询结果可用：<ul><li>可以存储为派生数据集</li><li>可以插入到现有的派生数据集中</li></ul>注：查询结果的记录计数没有上限。 |
| 通过以下方式返回的结果 | 数据集 | 不适用 | 这会定义如何将结果提供给用户。 |

{style="table-layout:auto"}

## 查询加速存储 {#query-accelerated-store}

下表提供了推荐的护栏限制以及查询加速存储的说明。

| 护栏 | 限制 | 限制类型 | 描述 |
|---|---|---|---|
| 查询并发 | 4 | 系统强制的护栏 | 为确保通过报表API对聚合数据进行查询(包括增强Real-Time CDP数据模型等数据模型的查询)具有高效执行的资源，报表API通过为每个查询分配并发插槽来跟踪资源利用率。 系统会将查询放入队列并等待并发插槽可用或从缓存中提供这些查询。 在任意给定时间，最多有4个并发查询插槽可用。<br>如果您通过BI工具访问报表API并且需要更多并发性，则需要BI服务器。 |

{style="table-layout:auto"}

## 后续步骤

阅读本文档后，您应该更好地了解使用可用查询模式执行查询的默认限制。

有关查询服务的更多信息，请参阅以下文档：

* [查询服务API](./api/getting-started.md)
* [查询服务UI](./ui/overview.md)

请参阅Real-Time CDP产品描述文档中的以下文档，了解有关其他Experience Platform服务护栏、端到端延迟信息和许可信息的更多信息：

* [Real-Time CDP护栏](/help/rtcdp/guardrails/overview.md)
* [各种Experience Platform服务的端到端延迟图](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=zh-Hans#end-to-end-latency-diagrams)。
* [Real-Time Customer Data Platform (B2C版本 — Prime和Ultimate包)](https://helpx.adobe.com/cn/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Prime和Ultimate包)](https://helpx.adobe.com/cn/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Prime和Ultimate包)](https://helpx.adobe.com/cn/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)
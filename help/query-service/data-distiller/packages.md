---
title: 查询服务包
description: 以下文档概述了可用于查询服务的功能和产品包，并重点介绍了临时查询和批处理查询之间的差异。
source-git-commit: 2db842c46d7075d77d3fd15c0db2b58b59e4140b
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 3%

---

# 查询服务包

本文档概述了查询服务中可用的不同类型打包和查询执行功能。

Adobe Experience Platform查询服务可以根据可执行的查询模式分为两种功能：

- **临时查询** 是用于探索已摄取数据集以进行验证、验证、实验等的SQL查询。 这些查询不会将数据写回平台数据湖中。
- **批量查询** 是用于对摄取的数据集执行摄取后处理的SQL查询。 这些查询可清理、形状、处理和扩充数据，其结果将写回Platform数据湖。 这些查询可以作为批处理作业进行计划、管理和监控。

查询服务功能与以下产品和加载项一起打包：

- **基于平台的应用程序** (Real-time Customer Data Platform、Customer Journey Analytics和Adobe Journey Optimizer):从一开始就提供用于执行临时查询的查询服务访问权限，其中包含基于平台的应用程序的每个变体和层。
- **[!DNL Data Distiller]** (可与Adobe Real-Time CDP、Customer Journey Analytics和Adobe Journey Optimizer一起购买的附加组件包):提供了用于执行批处理查询的查询服务访问权限 [!DNL Data Distiller].

下表概述了基于查询服务打包方式的关键授权：

| 查询服务授权 | 与基于平台的应用程序打包 | 包装 [!DNL Data Distiller] |
|---|---|---|
| 支持的查询模式 | 仅限Ad Hoc查询 | 批量查询 |
| 支持的用例 | <ul><li>探&#x200B;索</li><li>数据发&#x200B;现</li><li>数据验证</li><li>实验</li></ul> | <ul><li>清洁</li><li>成形</li><li>操纵</li><li>丰富</li></ul> |
| 支持的语义 | <ul><li>选择查询</li></ul> | <ul><li>CTAS和ITAS查询</li></ul> |
| 最大执行时间 | 10 分钟 | 24 小时 |
| 许可证量度 | **查询用户并发**: <ul><li>1个并发用户(Real-time CDP， Adobe Journey Optimizer)&#x200B;</li><li>5个并发用户(Customer Journey Analytics&#x200B;)</li></ul> **查询并发**: <ul><li>1个并发运行查询（所有应用程序）&#x200B;</li></ul> **其他临时查询用户包附加组件** 可购买以增加客户授权的临时查询授权。 <ul><li>每包额外+5个并行用户</li><li>每个包额外+1个并行运行查询</li></ul> | **计算小时数**: <ul><li>变量（范围基于客户的应用程序权限）</li></ul> **计算小时数** 是查询服务引擎在执行批处理查询时读取、处理数据并将数据写回数据湖所花费的时间。 |
| 查询执行界面 | <ul><li>查询服务UI</li><li>第三方客户端UI</li><li>[!DNL PostgresSQL] 客户端UI</li></ul> | <ul><li>查询UI </li><li>第三方客户端UI</li><li>[!DNL PostgresSQL] 客户端UI</li><li>REST API</li></ul> |
| 通过返回的查询结果 | 客户端UI | 数据湖中存储的派生数据集 |
| 结果限制 | <ul><li>查询UI - 100行</li><li>第三方客户 — 50,000</li><li>[!DNL PostgresSQL] 客户端 — 50,000</li></ul> | <ul><li>查询UI（行数没有上限）</li><li>第三方客户端（对行没有上限）</li><li>[!DNL PostgresSQL] 客户端（对行没有上限）</li><li>REST API（行数上限）</li></ul> |
| 读取数据集容量 | 是 | 是 |
| 写入数据集容量 | 否 | 是 |
| 计划容量 | 否 | 是 |
| 监控容量 | 是 | 是 |
| 查询警报设置容量 | 否 | 是 |

{style=&quot;table-layout:auto&quot;}

## 访问控制

Experience Platform的访问控制通过 [Adobe Admin Console](https://adminconsole.adobe.com/) 其中，产品配置文件可将用户与权限和沙箱链接起来。 请参阅 [访问控制概述](../../access-control/home.md) 以了解更多信息。

要使用查询服务， [!DNL Manage Queries] 必须在admin console中启用权限。 此权限允许用户执行临时查询和批处理查询。 有关请求访问产品配置文件的详细说明 [!DNL Manage Queries] 权限在 [管理产品配置文件的权限](../../access-control/ui/permissions.md) 和 [管理产品配置文件的用户](../../access-control/ui/users.md) 文档。

购买 [!DNL Data Distiller] 附加组件， [!DNL Write Dataset] 必须授予权限。 此权限允许 [!DNL Data Distiller] 用户执行批处理查询。

下表概述了 [!DNL Manage Queries] 权限：

| 权限 | 函数 |
|---|---|
| [!DNL Manage Queries] （无写入数据权限） | 提供执行临时查询的访问权限 |
| [!DNL Manage Queries] （具有写数据权限） | 提供执行批处理查询的访问权限 |

{style=&quot;table-layout:auto&quot;}

## 沙盒支持

沙箱是单个Experience Platform实例中的虚拟分区。 每个Platform实例都支持多个生产和非生产沙箱，每个沙箱都维护其自己的Platform资源库。 非生产沙箱允许您测试功能、运行实验和进行自定义配置，而不会影响生产沙箱。 有关沙箱的详细信息，请参阅 [沙箱概述](../../sandboxes/home.md). 所有查询服务权限均在所有沙箱之间共享

## 后续步骤

通过阅读本文档，您应更好地了解查询服务中提供的不同打包类型和查询执行功能。 要进一步了解查询服务（如已知的行业用例），请阅读 [用例文档](../use-cases/abandoned-browse.md). 有关更多常规信息，请访问 [查询服务概述](../home.md).

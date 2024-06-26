---
title: 查询服务打包
description: 以下文档概述了可用于查询服务的功能和产品的打包，并着重说明了临时查询和批量查询之间的差异。
exl-id: ba472d9e-afe6-423d-9abd-13ecea43f04f
source-git-commit: 1e18a60478e2755f49d37d4d3bf4bd3ca6dbf23b
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 2%

---

# 查询服务打包

本文档概述了Query Service中可用的不同类型的打包和查询执行功能。

根据查询模式的不同，Adobe Experience Platform查询服务可以分为两大功能：

- **临时查询** SQL查询是用于探索用于验证、验证、试验等引入的数据集吗？ 这些查询不会将数据写回Platform数据湖。
- **批量查询** 是用于执行摄取的数据集的摄取后处理的SQL查询。 这些查询可清理、形状、操作和扩充数据，其结果会写回Platform数据湖。 这些查询可以作为批处理作业进行计划、管理和监视。

查询服务功能与以下产品和加载项一起打包：

- **基于平台的应用程序** (Adobe Real-time Customer Data Platform、Adobe Customer Journey Analytics和Adobe Journey Optimizer)：从一开始就提供对查询服务的访问权限，以便执行基于平台的应用程序的每个变体和层级。
- **[!DNL Data Distiller]** (可与Adobe Real-Time CDP、Customer Journey Analytics和Adobe Journey Optimizer一起购买的附加组件包)：提供执行批量查询的查询服务访问权限 [!DNL Data Distiller].

## 权利 {#entitlements}

下表概述了基于其打包方式的关键查询服务权限：

| 查询服务权利 | 与基于平台的应用程序打包 | 已打包 [!DNL Data Distiller] |
|---|---|---|
| 支持的查询模式 | 仅临时查询 | 批量查询 |
| 支持的用例 | <ul><li>探索&#x200B;</li><li>数据发现&#x200B;</li><li>数据验证</li><li>试验</li></ul> | <ul><li>清洁</li><li>Shaping</li><li>操作</li><li>丰富</li></ul> |
| 支持的语义 | <ul><li>选择查询</li></ul> | <ul><li>CTA和ITAS查询</li></ul> |
| 最长执行时间 | 10 分钟 | 24 小时 |
| 许可证量度 | **查询用户并发**： <ul><li>1个并发用户(Real-Time CDP、Adobe Journey Optimizer)&#x200B;</li><li>5个并发用户(Customer Journey Analytics)&#x200B;</li></ul> **查询并发**： <ul><li>1个并发运行查询(所有应用程序&#x200B;)</li></ul> **附加的ad hoc query users pack附加组件** 可购买以增加您授权的临时查询权限。 <ul><li>每包5个以上并发用户</li><li>每包+1个额外的并发运行查询</li></ul> | **计算小时数**： <ul><li>变量（根据您的应用程序权利设定范围）</li></ul> **计算小时数** 是测量在执行批量查询时，查询服务引擎读取、处理数据并将其写回数据湖所花费的时间。 <br>使用Data Distiller SKU，您还可以获得附加用户和查询并发，这可用于执行临时查询。  数据Distiller SKU包括：<br><ul><li>另外5个并发用户</li><li>+1个额外的并发运行查询</li></ul> |
| 加快查询和报告使用 | 否 | 是 — 通过并发加速查询，您可以从加速存储中读取数据，并在功能板中显示。 还提供了用于在加速存储中存储报告模型和数据集的专用权限。 |
| 数据湖存储容量 | 您的总存储权利取决于您的基于平台的应用程序许可证。 例如，Real-Time CDP、AJO、CJA等。 | 是 — 提供了额外的存储权利，以便在七天数据到期日期之后保留数据Distiller用例的原始数据集和派生数据集。<br>您的数据湖存储容量以TB为单位，具体取决于您购买的计算小时数。 查看产品描述以了解更多详细信息。 |
| 允许数据导出 | 您的总导出权利取决于您的基于平台的应用程序许可证。 例如，Real-Time CDP、AJO、CJA等。 | 是 — 提供了额外的导出授权，以允许导出使用数据Distiller创建的派生数据集。<br>您每年允许的数据导出以TB为单位，具体取决于您购买的计算小时数。 请查看产品描述以了解更多详细信息。 |
| 查询执行界面 | <ul><li>查询服务UI</li><li>第三方客户端用户界面</li><li>[!DNL PostgresSQL] 客户端用户界面</li></ul> | <ul><li>查询服务UI </li><li>第三方客户端用户界面</li><li>[!DNL PostgresSQL] 客户端用户界面</li><li>REST API</li></ul> |
| 通过返回的查询结果 | 客户端用户界面 | 存储在数据湖中的派生数据集 |
| 结果限制 | <ul><li>查询服务UI — 输出行数可以是 [配置了UI设置](./ui/user-guide.md#result-count) 到50-500行。</li><li>第三方客户 — 50,000</li><li>[!DNL PostgresSQL] 客户端 — 50,000</li></ul> | CTAS和ITAS查询仅生成成功消息，因为查询输出存储在派生数据集中。 |
| 读取数据集容量 | 是 | 是 |
| 写入数据集容量 | 否 | 是 |
| 计划产能 | 否 | 是 |
| 监控容量 | 是 | 是 |
| 查询警报设置容量 | 否 | 是 |

{style="table-layout:auto"}

## 访问控制 {#access-control}

Experience Platform的访问控制是通过 [Adobe Admin Console](https://adminconsole.adobe.com/) 其中，产品配置文件将用户与权限和沙盒关联起来。 请参阅 [访问控制概述](../access-control/home.md) 以了解更多信息。

请参阅 [管理产品配置文件的权限](../access-control/ui/permissions.md) 和 [管理产品配置文件的用户](../access-control/ui/users.md) 有关请求访问产品配置文件权限的详细说明，请参阅

### 相关查询服务权限 {#query-service-permissions}

要使用查询服务，请 **[!DNL Manage Queries]** 必须在Admin Console中启用权限。 此权限允许用户执行临时和批量查询。

下表概述了 [!DNL Manage Queries] 权限：

| 权限 | 功能 |
|---|---|
| [!DNL Manage Queries] （没有写入数据权限） | 提供执行特定查询的访问权限 |
| [!DNL Manage Queries] （具有写入数据权限） | 提供执行批处理查询的访问权限 |

{style="table-layout:auto"}

### 相关可自定义的分析权限 {#customizable-insights-permissions}

创建数据Distiller [可自定义的分析](./data-distiller/customizable-insights/overview.md) 在功能板中，具有以下权限 **必须** 已在Admin Console中启用。

| 权限 | 功能 |
|---|---|
| [!DNL View Custom Dashboard] | 提供对用户定义仪表板的查看访问权限 |
| [!DNL Manage Custom Dashboard] | 提供用户定义的仪表板的管理访问权限 |

{style="table-layout:auto"}

## 沙盒支持 {#sandbox-support}

沙盒是单个Experience Platform实例中的虚拟分区。 每个Platform实例都支持多个生产沙盒和非生产沙盒，每个沙盒都维护自己的Platform资源库。 非生产沙盒允许您测试功能、运行实验并进行自定义配置，而不会影响您的生产沙盒。 有关沙箱的详细信息，请参阅 [沙盒概述](../sandboxes/home.md). 所有查询服务权利在所有沙盒中共享。

## 后续步骤

通过阅读本文档，您应该更好地了解查询服务中可用的不同打包类型和查询执行功能。 要了解有关查询服务的更多信息（如著名的行业用例），请参阅 [用例文档](./use-cases/abandoned-browse.md). 欲知更多一般信息，请访问 [查询服务概述](./home.md).


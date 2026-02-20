---
title: 查询服务打包
description: 以下文档概述了可用于查询服务的功能和产品的打包，并着重说明了临时查询和批量查询之间的差异。
exl-id: ba472d9e-afe6-423d-9abd-13ecea43f04f
source-git-commit: 33b3534a2c3f9b5da54fa4f3897d1e107f7c1976
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 3%

---

# 查询服务打包

本文档概述了Query Service中可用的不同类型的打包和查询执行功能。

根据查询模式的不同，Adobe Experience Platform查询服务可以分为两大功能：

- **临时查询**&#x200B;是用于浏览摄取的数据集以进行验证、验证、试验等的SQL查询。 这些查询不会将数据写回Experience Platform数据湖。
- **批处理查询**&#x200B;是用于对所摄取的数据集执行摄取后处理的SQL查询。 这些查询可清理、形状、操作和扩充数据，其结果会写回Experience Platform数据湖。 这些查询可以作为批处理作业进行计划、管理和监视。

查询服务功能与以下产品和加载项一起打包：

- **基于Experience Platform的应用程序**(Adobe Real-Time Customer Data Platform、Adobe Customer Journey Analytics和Adobe Journey Optimizer)：从一开始便为基于Experience Platform的应用程序的每个变体和层提供了执行临时查询的查询服务访问权限。
- **[!DNL Data Distiller]** (可与Adobe Real-Time CDP、Customer Journey Analytics和Adobe Journey Optimizer一起购买的附加组件包)： [!DNL Data Distiller]提供执行批处理查询的查询服务访问权限。

## 权利 {#entitlements}

下表概述了基于其打包方式的关键查询服务权限：

| 查询服务权利 | 与基于Experience Platform的应用程序打包 | 已与[!DNL Data Distiller]一起打包 |
|---|---|---|
| 支持的查询模式 | 仅临时查询 | 批量查询 |
| 支持的用例 | <ul><li>探索&#x200B;</li><li>数据发现&#x200B;</li><li>数据验证</li><li>试验</li></ul> | <ul><li>清洁</li><li>Shaping</li><li>操作</li><li>丰富</li></ul> |
| 支持的语义 | <ul><li>选择查询</li></ul> | <ul><li>CTA和ITAS查询</li></ul> |
| 最长执行时间 | 10 分钟 | 24 小时 |
| 许可证量度 | **查询用户并发**： <ul><li>1个并发用户(Real-Time CDP、Adobe Journey Optimizer)&#x200B;</li><li>5个并发用户(Customer Journey Analytics、Adobe Mix Modeler)&#x200B;</li></ul> **查询并发**： <ul><li>1个并发运行查询(所有应用程序&#x200B;)</li></ul> **可以购买附加的即席查询用户包加载项**&#x200B;以增加您的授权即席查询授权。 <ul><li>每包5个以上并发用户</li><li>每包+1个额外的并发运行查询</li></ul> | **计算小时数**： <ul><li>变量（根据您的应用程序权利设定范围）</li></ul> **计算小时数**&#x200B;是查询服务引擎在执行批处理查询时读取、处理数据并将其写回数据湖所花费的时间量。 <br>使用Data Distiller SKU，您还可以获得一个附加用户和查询并发，可用于执行临时查询。  数据Distiller SKU包括：<br><ul><li>另外5个并发用户</li><li>+1个额外的并发运行查询</li></ul> |
| 加快查询和报告使用 | 否 | 是 — 通过并发加速查询，您可以从加速存储中读取数据，并在功能板中显示。 还提供了用于在加速存储中存储报告模型和数据集的专用权限。 |
| 数据湖存储容量 | 您的总存储权利取决于您的基于平台的应用程序许可证。 例如，Real-Time CDP、AJO、CJA等。 | 是 — 提供了额外的存储权利，以便在七天数据到期日期之后保留数据Distiller用例的原始数据集和派生数据集。<br>您的数据湖存储容量以TB为单位，具体取决于您购买的计算小时数。 查看产品描述以了解更多详细信息。 |
| 允许数据导出 | 您的总导出权利取决于您的基于平台的应用程序许可证。 例如，Real-Time CDP、AJO、CJA等。 | 是 — 提供了额外的导出授权，以允许导出使用数据Distiller创建的派生数据集。<br>您每年允许的数据导出量以TB为单位，具体取决于您购买的计算小时数。 请查看产品描述以了解更多详细信息。 |
| 查询执行界面 | <ul><li>查询服务UI</li><li>第三方客户端用户界面</li><li>[!DNL PostgresSQL]客户端用户界面</li></ul> | <ul><li>查询服务UI </li><li>第三方客户端用户界面</li><li>[!DNL PostgresSQL]客户端用户界面</li><li>REST API</li></ul> |
| 通过返回的查询结果 | 客户端用户界面 | 存储在数据湖中的派生数据集 |
| 结果限制 | <ul><li>查询服务UI — 输出行数可以是[使用UI设置](./ui/user-guide.md#result-count)配置为50-500行。</li><li>第三方客户 — 50,000</li><li>[!DNL PostgresSQL]客户端 — 50,000</li></ul> | CTAS和ITAS查询仅生成成功消息，因为查询输出存储在派生数据集中。 |
| 读取数据集容量 | 是 | 是 |
| 写入数据集容量 | 否 | 是 |
| 计划产能 | 否 | 是 |
| 监控容量 | 是 | 是 |
| 查询警报设置容量 | 否 | 是 |

{style="table-layout:auto"}

## 访问控制 {#access-control}

Experience Platform的访问控制通过[Adobe Admin Console](https://adminconsole.adobe.com/)进行管理，其中产品配置文件将用户与权限和沙盒关联起来。 有关详细信息，请参阅[访问控制概述](../access-control/home.md)。

有关请求访问产品配置文件权限的详细说明，请参阅[管理产品配置文件权限](../access-control/ui/permissions.md)和[管理产品配置文件用户](../access-control/ui/users.md)文档

### 相关查询服务权限 {#query-service-permissions}

若要使用查询服务，必须在Admin Console中启用&#x200B;**[!DNL Manage Queries]**&#x200B;权限。 此权限允许用户执行临时和批量查询。

下表概述了[!DNL Manage Queries]权限的影响：

| 权限 | 函数 |
|---|---|
| [!DNL Manage Queries] （没有写入数据权限） | 提供执行特定查询的访问权限 |
| [!DNL Manage Queries] （具有写入数据权限） | 提供执行批处理查询的访问权限 |

{style="table-layout:auto"}

### 相关的SQL分析权限 {#sql-insights-permissions}

要在功能板中创建数据Distiller [SQL Insights](./data-distiller/sql-insights/overview.md)，必须在Admin Console中启用以下权限&#x200B;**&#x200B;**。

| 权限 | 函数 |
|---|---|
| [!DNL View Custom Dashboard] | 提供对用户定义仪表板的查看访问权限 |
| [!DNL Manage Custom Dashboard] | 提供用户定义的仪表板的管理访问权限 |

{style="table-layout:auto"}

## 沙盒支持 {#sandbox-support}

沙盒是单个 Experience Platform 实例内的虚拟分区。每个Experience Platform实例都支持多个生产沙盒和非生产沙盒，每个沙盒都维护自己的Experience Platform资源库。 非生产沙盒允许您测试功能、运行实验并进行自定义配置，而不会影响您的生产沙盒。 有关沙箱的详细信息，请参阅[沙箱概述](../sandboxes/home.md)。 所有查询服务权利在所有沙盒中共享。

## 后续步骤

通过阅读本文档，您应该更好地了解查询服务中可用的不同打包类型和查询执行功能。 若要了解有关查询服务（如已知行业用例）的更多信息，请阅读[用例文档](./use-cases/abandoned-browse.md)。 有关更一般的信息，请访问[查询服务概述](./home.md)。


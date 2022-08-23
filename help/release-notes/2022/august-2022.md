---
title: Adobe Experience Platform发行说明2022年8月
description: 2022年8月版Adobe Experience Platform发行说明。
source-git-commit: 2a507b4fe5b7c9dc523ceb5b2f39becf9e574ed9
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 14%

---

# Adobe Experience Platform 发行说明

**发行日期：2022 年 8 月 24 日**

Adobe Experience Platform 现有功能的更新包括：

- [数据准备](#data-prep)
- [源](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允许数据工程师在体验数据模型(XDM)之间映射、转换和验证数据。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 支持摄取带有警告的记录 | 数据准备现在会将警告（非严重错误）本地化到字段，并允许摄取行的其余部分。 现在，所有映射器转换错误都会报告为警告，部分摄取的行被视为成功，并带有警告。  还支持对包含警告和诊断详细信息的记录进行监控。 部分摄取带有警告的记录当前仅可用于流数据。 查看 [摄取带警告的记录](../../sources/tutorials/ui/monitor-streaming.md) 以了解更多信息。 |

{style=&quot;table-layout:auto&quot;}

详细了解 [!DNL Data Prep]，请参阅 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 跨区域支持Adobe Analytics源 | 您现在可以接收来自任何地区（美国、英国或新加坡）的报告包。 必须将报表包映射到与在其中创建源连接的Experience Platform沙盒实例相同的组织。 有关详细信息，请参阅 [在UI中创建Adobe Analytics源连接](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style=&quot;table-layout:auto&quot;}

要进一步了解源，请参阅 [源概述](../../sources/home.md).

---
title: Adobe Experience Platform 发行说明
description: Adobe Experience Platform的最新发行说明。
source-git-commit: 7145867795bcd8e1093c09df3fefdee518f9578a
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 7%

---

# Adobe Experience Platform 发行说明

**发布日期：2022 年 3 月 30 日**

Adobe Experience Platform的新增功能：

- [[!DNL Audit Logs]](#audit-logs)

Adobe Experience Platform 现有功能的更新包括：

- [警报](#alerts)
- [源](#sources)

## [!DNL Audit Logs] {#audit-logs}

Experience Platform允许您审核用户活动以获取各种服务和功能。 审核日志提供有关谁执行了操作以及何时执行的信息。

**新增功能**

| 功能 | 描述 |
| --- | --- |
| 数据集、架构、类、字段组、数据类型、沙盒、目标、区段、合并策略、计算属性、产品配置文件和帐户的审核日志(Adobe) | 这些是审核日志记录的资源。 如果启用了该功能，则会在活动发生时自动收集审核日志。 您无需手动启用日志收集。 |
| 导出审核日志 | 审核日志可下载为 `CSV` 或 `JSON` 文件。 生成的文件将直接保存到您的计算机。 |

有关Platform中审核日志的更多信息，请参阅 [审核日志概述](../../landing/governance-privacy-security/audit-logs/overview.md).

## 警报 {#alerts}

Experience Platform允许您订阅各种平台活动的基于事件的警报。 您可以通过 [!UICONTROL 警报] 选项卡，可以选择通过UI本身或电子邮件通知接收警报消息。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 新警报规则 | 两个新的警报规则现在可用于与数据摄取相关的源。 请参阅 [警报规则](../../observability/alerts/rules.md) ，以了解更新的警报类型列表。 |

有关平台中警报的更多信息，请参阅 [警报概述](../../observability/alerts/overview.md).

## 源 {#sources}

Adobe Experience Platform可以从外部源摄取数据，同时允许您使用Platform服务来构建、标记和增强该数据。 您可以从各种来源摄取数据，如Adobe应用程序、基于云的存储、第三方软件和您的CRM系统。

Experience Platform提供了RESTful API和交互式UI，让您可以轻松地为各种数据提供程序设置源连接。 这些源连接允许您验证并连接到外部存储系统和CRM服务，设置摄取运行的时间，以及管理数据摄取吞吐量。

**更新功能**

| 功能 | 描述 |
| --- | --- |
| 现在有新的源可用于B2B使用 | 现在，您可以在Platform上为B2B用例使用所有可用源。 请参阅 [源目录](../../sources/home.md) 以获取可用源的完整列表。 |
| 全面提供新 [!DNL Oracle Eloqua] 来源 | 您现在可以使用 [!DNL Oracle Eloqua] 源：无缝地从 [!DNL Oracle Eloqua] 实例（帐户、营销活动、联系人）到平台。 请参阅 [创建 [!DNL Oracle Eloqua] 源连接](../../sources/connectors/oracle-eloqua.md) 以了解更多信息。 |
| 的API增强功能 [!DNL Data Landing Zone] | 的 [!DNL Data Landing Zone] 现在，源支持在使用 [!DNL Flow Service] API。 请参阅 [创建 [!DNL Data Landing Zone] 源连接](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) 以了解更多信息。 |

要进一步了解源，请参阅 [源概述](../../sources/home.md).

---
title: Adobe Experience Platform 发行说明（2026 年 2 月）
description: Adobe Experience Platform 的 2026 年 2 月发行说明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 7cb35f5b35878b655dc668c0b26e22a41d675161
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 46%

---

# Adobe Experience Platform 发行说明

>[!TIP]
>
>有关其他 Adobe Experience Platform 应用程序的发行说明，请参阅以下文档：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hans/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/releases/latest)
>- [联合受众构成](https://experienceleague.adobe.com/zh-hans/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hans/docs/real-time-cdp-collaboration/using/latest)

**发行日期： 2026年2月17日**

Adobe Experience Platform 中新功能和现有功能的更新：

- [警报](#alerts)
- [目标](#destinations)
- [源](#sources)

## 警报 {#alerts}

Experience Platform 允许您订阅各种 Experience Platform 活动的基于事件的警报。您可以通过Experience Platform用户界面的[!UICONTROL Alerts]选项卡订阅各种警报规则，并且可以选择在UI中或通过电子邮件通知接收警报消息。

**新增功能或更新后的功能**

| 功能 | 描述 |
| --- | --- |
| 面向客户的警报[!DNL Slack]集成 | 您现在可以向[!DNL Slack]提供面向客户的警报。 按照[分步教程](../../observability/alerts/slack-integration.md)操作，设置[!DNL Slack]集成并直接在[!DNL Slack]工作区中接收警报通知。 |

{style="table-layout:auto"}

有关详细信息，请参阅 [[!DNL Observability Insights]  概述](../../observability/home.md)。

## 目标 {#destinations}

[!DNL Destinations] 是预建的与目标平台的集成，可实现从 Experience Platform 无缝激活数据。您可以使用目标激活已知和未知的数据，用于跨渠道营销活动、电子邮件营销活动、定向广告和许多其他用例。

**新增或更新目标**

| 目标 | 描述 |
| --- | --- |
| [[!DNL Snowflake] 批次](../../destinations/catalog/warehouses/snowflake-batch.md)一般可用 | [!DNL Snowflake]批次目标现已正式可用。 现在，世界各地的Real-Time CDP客户都可使用此连接器将数据激活到其Snowflake帐户，而无需实际复制数据。 有限版本的所有限制均已解除（仅适用于美国客户，仅支持属于默认合并策略的受众）。 |

{style="table-layout:auto"}

**修复和改进**

| 修复 | 描述 |
| --- | --- |
| 激活失败率超出警报 | 激活失败率超过目标警报现在可正确使用您在评估和发送警报时配置的阈值。 以前，无论您配置的百分比如何，警报都会以1%的失败率触发。 有关此警报的详细信息，请参阅[标准警报规则](../../observability/alerts/rules.md#destinations)。 |
| Google Customer Match排除的标识报表 | 修复了跳过的记录计数逻辑中的错误，该错误会导致Google客户匹配目标显示夸大的排除配置文件计数。 激活和导出行为不受影响；只有报告的数字不正确。 |

{style="table-layout:auto"}

有关更多信息，请阅读[目标概述](../../destinations/home.md)。

## 源 {#sources}

Experience Platform 提供 RESTful API 和交互式 UI，可让您轻松为各种数据提供者设置源连接。这些源连接允许您验证并连接到外部存储系统和 CRM 服务、设置运行摄取操作的时间以及管理数据摄取吞吐量。

**新源或已更新的源**

| 来源 | 描述 |
| --- | --- |
| [!DNL Databricks]源连接器中的Unity Catalog支持 | [!DNL Databricks]源连接器现在支持Unity目录。 阅读更新的[[!DNL Databricks]](../../sources/connectors/databases/databricks.md)文档，了解如何在配置源连接时使用Unity Catalog。 |

{style="table-layout:auto"}

有关更多信息，请阅读[源概述](../../sources/home.md)。
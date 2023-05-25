---
title: 用于报表包数据的Adobe Analytics Source Connector
description: 本文档概述了Analytics并描述了Analytics数据的用例。
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: 83ce7d46e4e64fbe961c964ed5a17ec12a7ec15f
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 7%

---

# 报告包数据的 Adobe Analytics Source Connector

Adobe Experience Platform允许您通过Analytics Source Connector摄取Adobe Analytics数据。 此 [!DNL Analytics] 源连接器流式传输由收集的数据 [!DNL Analytics] 实时转换到Platform，转换SCDS格式 [!DNL Analytics] 数据进入 [!DNL Experience Data Model] (XDM)供平台使用的字段。

本文档提供了以下内容的概述 [!DNL Analytics] 和介绍了的用例 [!DNL Analytics] 数据。

## Adobe Analytics和Analytics数据

[!DNL Analytics] 是一个功能强大的引擎，可帮助您了解有关客户的更多信息，了解他们如何与您的Web资产进行交互，了解您的数字营销支出在何处有效，并确定需要改进的方面。 [!DNL Analytics] 每年处理数万亿次的Web交易，并且 [!DNL Analytics] source connector允许您轻松利用这种丰富的行为数据并扩充 [!DNL Real-Time Customer Profile] 几分钟内。

![一个图形，用于说明来自各种Adobe应用程序(包括Adobe Analytics)的数据的历程。](./images/analytics-data-experience-platform.png)

从高层次上说， [!DNL Analytics] 从世界各地的各种数字渠道和多个数据中心收集数据。 收集数据后，会应用访客识别、分段和转换架构(VISTA)规则和处理规则来塑造传入数据。 原始数据经过此轻量级处理后，即可由以下人员使用 [!DNL Real-Time Customer Profile]. 在与上述过程平行的一个过程中，将相同的处理过的数据进行微批次处理，并将其摄取到Platform数据集中，以供以下人员使用 [!DNL Data Science Workspace]， [!DNL Query Service]和其他数据发现应用程序。

请参阅 [处理规则概述](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html?lang=zh-Hans) 以了解有关处理规则的更多信息。

## 体验数据模型(XDM)

XDM是一个公开记录的规范，为应用程序提供了通用结构和定义，以用于Experience Platform上与服务进行通信。

遵守XDM标准允许统一合并数据，使提交数据和收集信息更容易。

要了解有关XDM的更多信息，请参阅 [XDM系统概述](../../../xdm/home.md).

## 字段如何从Adobe Analytics映射到XDM？

>[!IMPORTANT]
>
>数据准备转换可能会增加整个数据流的延迟。 附加的延迟根据转换逻辑的复杂性而有所不同。

建立源连接以引入 [!DNL Analytics] 数据通过Platform用户界面进入Experience Platform，数据字段自动映射并引入 [!DNL Real-Time Customer Profile] 几分钟内。 有关创建源连接的说明 [!DNL Analytics] 使用Platform UI，请参阅 [Analytics源连接器教程](../../tutorials/ui/create/adobe-applications/analytics.md).

有关以下时间之间发生的字段映射的详细信息： [!DNL Analytics] 和Experience Platform，请参见 [Adobe Analytics字段映射](./mapping/analytics.md) 指南。

## Platform上Analytics数据的预期滞后时间是多少？

下表列出了Platform上Analytics数据的预期延迟。 滞后时间因客户配置、数据量和客户应用程序而异。 例如，如果将Analytics实施配置为 `A4T` 管道的延迟将增加到5-10分钟。

| Analytics 数据 | 预期延迟 |
| -------------- | ---------------- |
| 新数据到 [!DNL Real-Time Customer Profile] (A4T **非** enabled) | &lt; 2 分钟 |
| 新数据到 [!DNL Real-Time Customer Profile] (A4T **是** enabled) | 长达30分钟 |
| 数据湖的新数据 | &lt; 90 分钟 |
| 少于100亿个事件的回填 | &lt; 4 周 |

生产沙盒的Analytics回填默认为13个月。 对于非生产沙盒中的Analytics数据，回填将设置为3个月。 上表中提到的100亿个事件的限制严格地限于预期延迟。

在生产沙盒中创建Analytics源数据流时，将创建两个数据流：

* 一个数据流，可将历史报表包数据回填13个月到数据湖。 此数据流在回填完成后结束。
* 将实时数据发送到数据湖和的数据流 [!DNL Real-Time Customer Profile]. 此数据流持续运行。

>[!NOTE]
>
>Analytics回填数据未引入 [!DNL Profile] 因此，许可证配置文件中不会计入此项。

## 中的主要标识符 [!DNL Analytics] 数据

每次点击 [!DNL Analytics] source connector包含一个主要标识符，该主要标识符取决于ECID或AAID是否存在。 如果存在ECID，则ECID被指定为主要标识符。 如果存在AAID，则将AAID指定为主要的。

下表提供有关中标识字段的更多信息 [!DNL Analytics] 数据。

| 标识字段 | 描述 |
| --- | --- |
| AAID | AAID是Adobe Analytics中的主要设备标识符，并且必定存在于通过 [!DNL Analytics] 源。 AAID有时称为 *旧版Analytics ID* 或作为 `s_vi` Cookie ID。 尽管如此，即使 `s_vi` Cookie不存在。 AAID由 `post_visid_high` 和 `post_visid_low` 中的列 [[!DNL Analytics] 数据馈送](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). 对于任何给定事件，AAID字段都包含单个标识，它可能是 [操作顺序 [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **注释**：在整个报表包中，AAID可能包含跨事件的多种类型。 |
| ECID | ECID(Experience CloudID)是一个单独的设备标识符字段，在以下情况下会在Adobe Analytics中填充该字段： [!DNL Analytics] 是使用Experience CloudIdentity服务实现的。 ECID有时也称为MCID(Marketing CloudID)。 如果事件中存在ECID，则AAID可能基于ECID，具体取决于Analytics [宽限期](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) 已配置。 ECID由 `mcvisid` Analytics数据馈送中的。 有关ECID的更多信息，请参见 [ECID概述](../../../identity-service/ecid.md). 有关ECID如何与配合使用的信息 [!DNL Analytics]，请参阅文档 [Analytics和Experience CloudID请求](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html?lang=zh-Hans). |
| AACUSTOMID | Adobe Analytics AACUSTOMID是一个单独的标识符字段，根据对 `s.VisitorID` 中的变量 [!DNL Analytics] 实现。 AACUSTOMID由 `cust_visid` 中的列 [[!DNL Analytics] 数据馈送](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). 如果AACUSTOMID存在，则AAID将基于AACUSTOMID，因为AACUSTOMID比 [操作顺序 [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### 如何 [!DNL Analytics] 源处理身份

此 [!DNL Analytics] 源将这些标识以XDM形式传递给Experience Platform，如下所示：

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

这些字段未标记为标识。相反，相同的身份将复制到XDM的 `identityMap` 作为键值对：

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

在身份映射中，如果存在ECID，则将其标记为事件的主要身份。 在这种情况下，AAID可能基于ECID，这是由于 [Identity服务宽限期](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). 否则，会将 AAID 标记为事件的主标识。绝不会将 AACUSTOMID 标记为事件的主 ID。但是，如果存在AACUSTOMID，则由于操作顺序的Experience Cloud，AAID将基于AACUSTOMID。

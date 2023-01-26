---
title: Adobe Analytics报表包数据的源连接器
description: 本文档概述了Analytics，并介绍了Analytics数据的用例。
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: 486f5bdd834808c6262f41c0b0187721fc9b0799
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 7%

---

# 报告包数据的 Adobe Analytics Source Connector

Adobe Experience Platform允许您通过Analytics源连接器摄取Adobe Analytics数据。 的 [!DNL Analytics] 源连接器流收集的数据 [!DNL Analytics] 实时转换到平台，转换SCDS格式 [!DNL Analytics] 数据输入 [!DNL Experience Data Model] (XDM)字段供Platform使用。

本文档提供了 [!DNL Analytics] 和描述 [!DNL Analytics] 数据。

## Adobe Analytics和Analytics数据

[!DNL Analytics] 是一个功能强大的引擎，可帮助您进一步了解客户、客户如何与您的Web资产进行交互、了解您的数字营销支出在何处是有效的，以及确定需要改进的方面。 [!DNL Analytics] 每年处理数万亿次Web交易， [!DNL Analytics] 源连接器允许您轻松地利用此丰富的行为数据并丰富 [!DNL Real-Time Customer Profile] 几分钟后。

![一个图形，用于说明来自不同Adobe应用程序(包括Adobe Analytics)的数据历程。](./images/analytics-data-experience-platform.png)

在高层， [!DNL Analytics] 收集来自世界各地各种数字渠道和多个数据中心的数据。 收集数据后，将应用访客识别、分段和转换架构(VISTA)规则和处理规则来形成传入数据。 在原始数据经过这种轻量级的处理后，会认为它已准备好供使用 [!DNL Real-Time Customer Profile]. 在与上述过程平行的过程中，相同的处理数据被微批处理并摄取到Platform数据集中，以供 [!DNL Data Science Workspace], [!DNL Query Service]，以及其他数据发现应用程序。

请参阅 [处理规则概述](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html?lang=zh-Hans) 以了解有关处理规则的详细信息。

## 体验数据模型(XDM)

XDM是一项公开记录的规范，它为应用程序在Experience Platform时用于与服务通信的通用结构和定义。

遵循XDM标准可以统一纳入数据，从而更便于提供数据和收集信息。

要进一步了解XDM，请参阅 [XDM系统概述](../../../xdm/home.md).

## 如何将字段从Adobe Analytics映射到XDM?

>[!IMPORTANT]
>
>数据准备转换可能会为整个数据流添加延迟。 添加的额外延迟因转换逻辑的复杂性而异。

建立源连接以将 [!DNL Analytics] 数据通过Platform用户界面Experience Platform，数据字段会自动映射和引入到 [!DNL Real-Time Customer Profile] 几分钟内。 有关创建源连接的说明 [!DNL Analytics] 使用平台UI，查看 [Analytics源连接器教程](../../tutorials/ui/create/adobe-applications/analytics.md).

有关在 [!DNL Analytics] 和Experience Platform，请参阅 [Adobe Analytics字段映射](./mapping/analytics.md) 的双曲余切值。

## 平台上Analytics数据的预期滞后时间是多少？

下表概述了平台上Analytics数据的预期滞后。 滞后时间会因客户配置、数据量和客户应用程序而异。 例如，如果Analytics实施配置了 `A4T` 管道的延迟将增加到5到10分钟。

| Analytics 数据 | 预期滞后 |
| -------------- | ---------------- |
| 新数据 [!DNL Real-Time Customer Profile] (A4T) **not** enabled) | &lt; 2 分钟 |
| 新数据 [!DNL Real-Time Customer Profile] (A4T) **is** enabled) | &lt; 15 分钟 |
| 数据湖的新数据 | &lt; 90 分钟 |
| 回填不到100亿个事件 | &lt; 4 周 |

Analytics回填默认为13个月。 上表所列的100亿件事件的限制严格限于预期滞后。

>[!NOTE]
>
>不会将Analytics回填数据摄取到 [!DNL Profile] 因此，许可证配置文件中不会计入此类事件。

## 中的主要标识符 [!DNL Analytics] 数据

从 [!DNL Analytics] 源连接器包含主要标识符，该标识符取决于ECID还是AAID存在。 如果存在ECID，则会将ECID指定为主标识符。 如果存在AAID，则将AAID指定为主AAID。

下表提供了有关 [!DNL Analytics] 数据。

| 标识字段 | 描述 |
| --- | --- |
| AAID | AAID是Adobe Analytics中的主设备标识符，它保证存在于通过 [!DNL Analytics] 来源。 AAID有时称为 *旧版Analytics ID* 或作为 `s_vi` cookie ID。 尽管如此，即使在 `s_vi` cookie不存在。 AAID由 `post_visid_high` 和 `post_visid_low` 列 [[!DNL Analytics] 数据馈送](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). 在任何给定事件上，AAID字段都包含单个标识，该标识可能是 [操作顺序 [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **注意**:在整个报表包中，AAID可能包含各种事件的各种类型。 |
| ECID | ECID(Experience CloudID)是一个单独的设备标识符字段，在 [!DNL Analytics] 使用Experience Cloud标识服务实施。 ECID有时也称为MCID(Marketing CloudID)。 如果事件中存在ECID，则AAID可能基于ECID，具体取决于Analytics [宽限期](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) 已配置。 ECID由 `mcvisid` （在Analytics数据馈送中）。 有关ECID的更多信息，请参阅 [ECID概述](../../../identity-service/ecid.md). 有关ECID如何与 [!DNL Analytics]，请参阅 [Analytics和Experience CloudID请求](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html?lang=zh-Hans). |
| AACUSTOMID | AACUSTOMID是一个单独的标识符字段，该字段会根据使用 `s.VisitorID` 变量 [!DNL Analytics] 实施。 AACUSTOMID由 `cust_visid` 列 [[!DNL Analytics] 数据馈送](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html). 如果存在AACUSTOMID，则AAID将基于AACUSTOMID，因为AACUSTOMID会覆盖由 [操作顺序 [!DNL Analytics] ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### 如何 [!DNL Analytics] 源代码标识

的 [!DNL Analytics] 源将这些身份以XDM形式传递到Experience Platform，如下所示：

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

这些字段未标记为标识。相同的身份将会复制到XDM的 `identityMap` 作为键值对：

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

在身份映射中，如果ECID存在，则会将其标记为事件的主标识。 在这种情况下，AAID可能基于ECID，因为 [Identity服务宽限期](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). 否则，会将 AAID 标记为事件的主标识。绝不会将 AACUSTOMID 标记为事件的主 ID。但是，如果存在AACUSTOMID，则由于操作的Experience Cloud顺序，AAID基于AACUSTOMID。
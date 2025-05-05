---
title: 报告包数据的Adobe Analytics Source Connector
description: 本文档概述了Analytics，并描述了Analytics数据的用例。
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1196'
ht-degree: 0%

---

# 报告包数据的Adobe Analytics source connector

Adobe Experience Platform允许您通过Analytics Source Connector摄取Adobe Analytics数据。 [!DNL Analytics]源连接器将[!DNL Analytics]收集的数据实时流式传输到Experience Platform，并将SCD格式的[!DNL Analytics]数据转换为[!DNL Experience Data Model] (XDM)字段以供Experience Platform使用。

本文档提供了[!DNL Analytics]的概述并描述了[!DNL Analytics]数据的用例。

## Adobe Analytics和Analytics数据

[!DNL Analytics]是一个功能强大的引擎，可帮助您了解有关客户的更多信息，了解他们如何与您的Web资产进行交互，了解您的数字营销支出在哪些方面有效，并确定需要改进的方面。 [!DNL Analytics]每年处理数万亿个Web事务，而[!DNL Analytics]源连接器允许您轻松地挖掘此丰富的行为数据，并在几分钟内扩充[!DNL Real-Time Customer Profile]。

![一个图形，说明来自包括Adobe Analytics在内的不同Adobe应用程序的数据之旅。](./images/analytics-data-experience-platform.png)

从较高层面来看，[!DNL Analytics]从世界各地的各种数字渠道和多个数据中心收集数据。 收集数据后，将应用访客识别、分段和转换架构(VISTA)规则和处理规则来塑造传入的数据。 原始数据经过此轻量级处理后，会被[!DNL Real-Time Customer Profile]视为准备就绪，可供使用。 在与上述过程平行的过程中，相同的已处理数据会被微批次并摄取到Experience Platform数据集中，以供[!DNL Query Service]和其他数据发现应用程序使用。

有关处理规则的更多信息，请参阅[处理规则概述](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html?lang=zh-Hans)。

## Experience Data Model (XDM)

XDM是一个公开记录的规范，为应用程序提供了通用结构和定义，以便用于与Experience Platform上的服务进行通信。

遵守XDM标准允许统一合并数据，使得提交数据和收集信息更加容易。

要了解有关XDM的更多信息，请参阅[XDM系统概述](../../../xdm/home.md)。

## 字段如何从Adobe Analytics映射到XDM？

>[!IMPORTANT]
>
>数据准备转换可能会增加整个数据流的延迟。 附加的延迟因转换逻辑的复杂性而异。

为使用Experience Platform用户界面将[!DNL Analytics]数据引入Experience Platform而建立了源连接后，数据字段会在几分钟内自动映射并引入到[!DNL Real-Time Customer Profile]中。 有关使用Experience Platform UI创建与[!DNL Analytics]的源连接的说明，请参阅[Analytics源连接器教程](../../tutorials/ui/create/adobe-applications/analytics.md)。

有关[!DNL Analytics]与Experience Platform之间发生的字段映射的详细信息，请参阅[Adobe Analytics字段映射](./mapping/analytics.md)指南。

## Experience Platform上Analytics数据的预期滞后时间是多少？

下表概述了Experience Platform上Analytics数据的预期延迟。 滞后时间因客户配置、数据卷和使用者应用程序而异。 例如，如果Analytics实施配置了`A4T`，则管道延迟将增加到5-10分钟。

| Analytics数据 | 预期延迟 |
| -------------- | ---------------- |
| [!DNL Real-Time Customer Profile]的新数据（A4T **未**&#x200B;启用） | &lt; 2分钟 |
| [!DNL Real-Time Customer Profile]的新数据（A4T **已启用**） | 长达30分钟 |
| 数据湖的新数据 | &lt; 2.25小时 |
| 未拼合[的新数据到Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/stitching/overview.html?lang=en) | &lt; 3.75小时 |
| 通过拼合向Customer Journey Analytics提供新数据 | &lt; 7小时 |
| 少于100亿个事件的回填 | &lt; 4周 |

有关Customer Journey Analytics延迟的详细信息，请参阅：[Customer Journey Analytics护栏](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html?lang=en)。

生产沙盒的Analytics回填默认为13个月。 对于非生产沙盒中的Analytics数据，回填将设置为三个月。 上表中提到的100亿个事件的限制严格与预期延迟有关。

在生产沙盒中创建Analytics源数据流时，将创建两个数据流：

* 一个数据流，将历史报表包数据回填到13个月的数据湖。 此数据流在回填完成后结束。
* 将实时数据发送到数据湖和[!DNL Real-Time Customer Profile]的数据流流。 此数据流持续运行。

>[!NOTE]
>
>Analytics回填数据未摄取到[!DNL Profile]，因此许可证配置文件中未考虑这些数据。

## [!DNL Analytics]数据中的主标识符

来自[!DNL Analytics]源连接器的每次点击都包含一个主要标识符，该标识符取决于ECID或AAID是否存在。 如果存在ECID，则ECID被指定为主要标识符。 如果存在AAID，则将AAID指定为主要的。

下表提供了有关[!DNL Analytics]数据中标识字段的更多信息。

| 标识字段 | 描述 |
| --- | --- |
| AAID | AAID是Adobe Analytics中的主要设备标识符，并且必定存在于通过[!DNL Analytics]源传递的每个事件中。 AAID有时称为&#x200B;*旧版Analytics ID*&#x200B;或`s_vi` Cookie ID。 尽管如此，即使不存在`s_vi` Cookie，也会创建AAID。 AAID由[[!DNL Analytics] 数据馈送](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html)中的`post_visid_high`和`post_visid_low`列表示。 在任何给定事件上，AAID字段都包含单个标识，该标识可能是 [!DNL Analytics] ID[&#128279;](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html)的操作顺序中描述的几种不同类型之一。 **注意**：在整个报表包中，AAID可能包含跨事件的多种类型。 |
| ECID | ECID (Experience Cloud ID)是一个单独的设备标识符字段，当使用Adobe Analytics Identity Service实现[!DNL Analytics]时，将在Experience Cloud中填充该字段。 ECID有时也称为MCID (Marketing Cloud ID)。 如果事件中存在ECID，则AAID可能基于ECID，具体取决于是否配置了Analytics [宽限期](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html)。 在Analytics数据馈送中，ECID由`mcvisid`表示。 有关ECID的详细信息，请参阅[ECID概述](../../../identity-service/features/ecid.md)。 有关ECID如何与[!DNL Analytics]配合使用的信息，请参阅有关[Analytics和Experience Cloud ID请求](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html)的文档。 |
| AACUSTOMID | AACUSTOMID是一个单独的标识符字段，将根据[!DNL Analytics]实现中`s.VisitorID`变量的使用情况在Adobe Analytics中填充该字段。 在[[!DNL Analytics] 数据馈送](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html)中，AACUSTOMID由`cust_visid`列表示。 如果AACUSTOMID存在，则AAID将基于AACUSTOMID，因为AACUSTOMID优于 [!DNL Analytics] ID[&#128279;](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html)的操作顺序所定义的所有其他标识符。 |

### [!DNL Analytics]源如何处理标识

[!DNL Analytics]源将这些标识以XDM形式传递给Experience Platform，如下所示：

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

这些字段未标记为标识。 相反，相同的标识（如果存在于事件中）将作为键值对复制到XDM的`identityMap`中：

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

将一个或多个身份复制到`identityMap`时，`endUserIDs._experience.mcid.namespace.code`也设置在同一事件上：

* 如果存在AAID，则`endUserIDs._experience.aaid.namespace.code`设置为“AAID”。
* 如果存在ECID，则`endUserIDs._experience.mcid.namespace.code`设置为“ECID”。
* 如果存在AACUSTOMID，则`endUserIDs._experience.aacustomid.namespace.code`设置为“AACUSTOMID”。

在身份映射中，如果存在ECID，则将其标记为事件的主身份。 在这种情况下，由于[Identity服务宽限期](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html)，AAID可能基于ECID。 否则，AAID将标记为事件的主标识。 绝不会将AACUSTOMID标记为事件的主ID。 但是，如果存在AACUSTOMID，则由于Experience Cloud操作顺序，AAID将基于AACUSTOMID。

>[!NOTE]
>
>您可以使用数据准备过滤掉来自Analytics的次要身份，例如AAID和AACUSTOMID。 如果过滤掉这些标识，它们将不会被摄取到配置文件中，前提是它们在传入的Analytics数据中可用。 未过滤的数据将继续加载到数据湖中。

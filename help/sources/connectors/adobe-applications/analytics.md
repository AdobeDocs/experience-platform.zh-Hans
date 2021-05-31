---
keywords: Experience Platform；主页；热门主题；Analytics源连接器；分析；Analytics
solution: Experience Platform
title: Adobe Analytics报表包数据的源连接器
topic-legacy: overview
description: 本文档概述了Analytics，并介绍了Analytics数据的用例。
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 1%

---

# Adobe Analytics报表包数据的源连接器

Adobe Experience Platform允许您通过Analytics源连接器摄取Adobe Analytics数据。 [!DNL Analytics]源连接器将[!DNL Analytics]收集的数据实时流式传输到Platform，并将SCDS格式的[!DNL Analytics]数据转换为[!DNL Experience Data Model](XDM)字段供Platform使用。

本文档概述了[!DNL Analytics]，并介绍了[!DNL Analytics]数据的用例。

## Adobe Analytics和Analytics数据

[!DNL Analytics] 是一个功能强大的引擎，可帮助您进一步了解客户、客户如何与您的Web资产进行交互、了解您的数字营销支出在何处是有效的，以及确定需要改进的方面。[!DNL Analytics] 每年处理数万亿次web交易，而 [!DNL Analytics] 源连接器让您能够轻松地利用此丰富的行为数据，并在几分钟 [!DNL Real-time Customer Profile] 内丰富这些数据。

![](./images/analytics-data-experience-platform.png)

在高级别，[!DNL Analytics]从世界各地的各种数字渠道和多个数据中心收集数据。 收集数据后，将应用访客识别、分段和转换架构(VISTA)规则和处理规则来形成传入数据。 原始数据经过此轻量级处理后，会被视为已准备好供[!DNL Real-time Customer Profile]使用。 在与上述过程平行的过程中，相同的处理数据被微批处理并摄取到Platform数据集中，以供[!DNL Data Science Workspace]、[!DNL Query Service]和其他数据发现应用程序使用。

有关处理规则的更多信息，请参阅[处理规则概述](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html) 。

## 体验数据模型(XDM)

XDM是一项公开记录的规范，它为应用程序在Experience Platform时用于与服务通信的通用结构和定义。

遵循XDM标准可以统一纳入数据，从而更便于提供数据和收集信息。

要了解有关XDM的更多信息，请参阅[XDM系统概述](../../../xdm/home.md)。

## 如何将字段从Adobe Analytics映射到XDM?

当建立源连接以使用Platform用户界面将[!DNL Analytics]数据Experience Platform到中时，数据字段会在几分钟内自动映射并摄取到[!DNL Real-time Customer Profile]中。 有关使用Platform UI创建与[!DNL Analytics]的源连接的说明，请参阅[Analytics源连接器教程](../../tutorials/ui/create/adobe-applications/analytics.md)。

有关[!DNL Analytics]和Experience Platform之间的字段映射的详细信息，请参阅[Adobe Analytics字段映射](./mapping/analytics.md)指南。

## 平台上Analytics数据的预期滞后时间是多少？

| Analytics 数据 | 预期滞后 |
| -------------- | ---------------- |
| 新数据到[!DNL Real-time Customer Profile]（已启用A4T **未**） | &lt; 2 分钟 |
| [!DNL Real-time Customer Profile]的新数据（A4T **已启用**） | &lt; 15 分钟 |
| 数据湖的新数据 | &lt; 90 分钟 |
| 回填数据（13个月的数据或100亿个事件，以较低者为准） | &lt; 4 周 |

>[!NOTE]
>
>滞后时间会因客户配置、数据量和客户应用程序而异。 例如，如果[!DNL Analytics]实施配置了`A4T` ，则到管道的延迟将增加到5到10分钟。

## [!DNL Analytics]数据中的主标识符

[!DNL Analytics]源连接器的每次点击都包含一个主要标识符，该标识符取决于ECID还是AAID存在。 如果存在ECID，则会将ECID指定为主标识符。 如果存在AAID，则将AAID指定为主AAID。

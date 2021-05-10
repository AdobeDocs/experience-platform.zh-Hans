---
keywords: Experience Platform；主页；热门主题；分析源连接器；分析；分析
solution: Experience Platform
title: Adobe Analytics Source Connector for Report-Suite Data
topic-legacy: overview
description: 本文档概述了Analytics，并描述了Analytics数据的用例。
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
translation-type: tm+mt
source-git-commit: af5ad975bbfd6a67fe66c90e33da1365d49c8899
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 3%

---

# Adobe Analytics源连接器用于报表包数据

Adobe Experience Platform允许您通过Analytics源连接器收录Adobe Analytics数据。 [!DNL Analytics]源连接器将由[!DNL Analytics]收集的数据实时流化到平台，将SCDS格式的[!DNL Analytics]数据转换为[!DNL Experience Data Model](XDM)字段，供平台使用。

本文档概述[!DNL Analytics]并描述[!DNL Analytics]数据的用例。

## Adobe Analytics和Analytics数据

[!DNL Analytics] 是一款强大的引擎，可帮助您了解关于客户的更多信息、客户如何与您的网络资产互动、了解您的数字营销支出的成效以及确定改进领域。[!DNL Analytics] 每年处理数万亿个web事务，而 [!DNL Analytics] 源连接器使您能轻松利用这一丰富的行为数据，并在几 [!DNL Real-time Customer Profile] 分钟内丰富数据。

![](./images/analytics-data-experience-platform.png)

在高层面上，[!DNL Analytics]可收集来自世界各地各种数字渠道和多个数据中心的数据。 收集数据后，将应用访客识别、分段和转换架构(VISTA)规则和处理规则来改变传入数据的形状。 在原始数据经过此轻量处理后，会认为它可供[!DNL Real-time Customer Profile]使用。 在与上述过程平行的过程中，将相同的处理数据进行微批处理并摄取到平台数据集中，供[!DNL Data Science Workspace]、[!DNL Query Service]和其它数据发现应用使用。

有关处理规则的详细信息，请参阅[处理规则概述](https://docs.adobe.com/content/help/zh-Hans/analytics/admin/admin-tools/processing-rules/processing-rules.html)。

## 体验数据模型(XDM)

XDM是一个公开的文档规范，它为应用程序提供了通用结构和定义，以用于与Experience Platform上的服务通信。

遵循XDM标准可以统一整合数据，从而更轻松地交付数据和收集信息。

要了解有关XDM的更多信息，请参阅[XDM系统概述](../../../xdm/home.md)。

## 如何将字段从Adobe Analytics映射到XDM?

当建立源连接以使用平台用户界面将[!DNL Analytics]数据引入Experience Platform时，数据字段将在几分钟内自动映射并引入到[!DNL Real-time Customer Profile]中。 有关使用平台UI创建与[!DNL Analytics]的源连接的说明，请参阅[分析源连接器教程](../../tutorials/ui/create/adobe-applications/analytics.md)。

有关[!DNL Analytics]和Experience Platform之间发生的字段映射的详细信息，请参阅[Adobe Analytics字段映射](./mapping/analytics.md)指南。

## 平台上的Analytics数据预期的延迟是什么？

| Analytics 数据 | 预期延迟 |
| -------------- | ---------------- |
| [!DNL Real-time Customer Profile]的新数据（A4T **未**&#x200B;启用） | &lt; 2 分钟 |
| [!DNL Real-time Customer Profile]的新数据（A4T **已启用**） | &lt; 15 分钟 |
| 数据湖的新数据 | &lt; 90 分钟 |
| 回填数据(13个月的数据或100亿事件，以较低者为准) | &lt; 4 周 |

>[!NOTE]
>
>延迟会因客户配置、数据量和消费者应用程序而异。 例如，如果[!DNL Analytics]实现配置了`A4T` ，则到Pipeline的延迟将增加到5-10分钟。

## [!DNL Analytics]数据中的主标识符

[!DNL Analytics]源连接器的每次点击都包含一个主标识符，该标识符取决于ECID还是AAID存在。 如果有ECID，则将ECID指定为主标识符。 如果存在AAID，则将AAID指定为主AAID。

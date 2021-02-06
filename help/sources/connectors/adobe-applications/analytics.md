---
keywords: Experience Platform；主页；热门主题；Analytics Data Connector；分析；分析
solution: Experience Platform
title: Adobe Analytics报表包数据源连接器
topic: overview
description: 此文档概述了Analytics并描述了Analytics数据的用例。
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 3%

---


# Adobe Analytics报表包数据连接器

Adobe Experience Platform允许您通过Analytics Data Connector(ADC)获取Adobe Analytics数据。 ADC将由[!DNL Analytics]收集的数据实时流化到[!DNL Platform]，将SCDS格式的[!DNL Analytics]数据转换为[!DNL Experience Data Model](XDM)字段，供[!DNL Platform]使用。

此文档概述[!DNL Analytics]并描述[!DNL Analytics]数据的用例。

## Adobe Analytics与分析数据

[!DNL Analytics] 是一款强大的引擎，可帮助您了解关于客户的更多信息、客户如何与您的网络资产互动、了解数字营销支出的有效位置以及确定改进领域。[!DNL Analytics] 每年处理数万亿次web交易，ADC使您能轻松利用这一丰富的行为数据，并在几分钟 [!DNL Real-time Customer Profile] 内丰富这些数据。

![](./images/analytics-data-experience-platform.png)

从高度上讲，[!DNL Analytics]可收集来自全球各个数字渠道和多个数据中心的数据。 一旦收集了访客，就会应用识别、分段和转换架构(VISTA)规则和处理规则来改变传入数据的形状。 在原始数据经过此轻量处理后，[!DNL Real-time Customer Profile]会将其视为可供使用。 在与上述过程平行的过程中，将相同的处理数据微批处理并引入平台数据集中，供[!DNL Data Science Workspace]、[!DNL Query Service]和其它数据发现应用使用。

有关处理规则的详细信息，请参阅[处理规则概述](https://docs.adobe.com/content/help/zh-Hans/analytics/admin/admin-tools/processing-rules/processing-rules.html)。

## 体验数据模型(XDM)

XDM是一个公开的文档规范，它为用于与[!DNL Experience Platform]上的服务通信的应用程序提供通用结构和定义。

遵循XDM标准，可以统一整合数据，从而更轻松地交付数据和收集信息。

要进一步了解XDM，请参阅[XDM系统概述](../../../xdm/home.md)。

## 如何将字段从Adobe Analytics映射到XDM?

当建立源连接以使用[!DNL Platform]用户界面将[!DNL Analytics]数据引入[!DNL Experience Platform]时，将在几分钟内自动映射数据字段并将其引入[!DNL Real-time Customer Profile]。 有关使用[!DNL Platform] UI创建与[!DNL Analytics]的源连接的说明，请参阅[分析数据连接器教程](../../tutorials/ui/create/adobe-applications/analytics.md)。

有关[!DNL Analytics]和[!DNL Experience Platform]之间的字段映射的详细信息，请访问[Adobe Analytics字段映射指南](./mapping/analytics.md)。

## 平台上的Analytics数据预期的延迟是什么？

| Analytics 数据 | 预期延迟 |
| -------------- | ---------------- |
| [!DNL Real-time Customer Profile]的新数据（A4T **未**&#x200B;启用） | &lt; 2 分钟 |
| [!DNL Real-time Customer Profile]的新数据（A4T **已启用**） | &lt; 15 分钟 |
| 数据湖的新数据 | &lt; 45 分钟 |
| 回填数据(13个月的数据或100亿事件，以较低者为准) | &lt; 4 周 |

>[!NOTE]
>
>延迟因客户配置、数据量和消费者应用程序而异。 例如，如果Analytics实现配置了`A4T` ，则到管道的延迟将增加到5-10分钟。

## 分析数据中的主标识符

Analytics数据连接器的每次点击都包含一个主要标识符，它取决于ECID还是AAID存在。 如果有ECID，则将ECID指定为主标识符。 如果存在AAID，则将AAID指定为主AAID。
---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 分析数据连接器
topic: overview
translation-type: tm+mt
source-git-commit: 662ca170b7416dfb55cfb6b8cbaef640c1f83d31
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 3%

---


# Analytics Data Connector

Adobe Experience Platform允许您通过Analytics Data Connector(ADC)获取Adobe Analytics数据。 ADC将由收集的 [!DNL Analytics] 数据 [!DNL Platform] 实时流化，将SCDS格式化的 [!DNL Analytics] 数据转 [!DNL Experience Data Model] 换为(XDM)字段供 [!DNL Platform]用。

此文档概述 [!DNL Analytics] 了数据的用例 [!DNL Analytics] 。

## Adobe Analytics与分析数据

[!DNL Analytics] 是一款强大的引擎，可帮助您了解关于客户的更多信息、客户如何与您的网络资产互动、了解数字营销支出的有效位置以及确定改进领域。 [!DNL Analytics] 每年处理数万亿次web交易，ADC使您能轻松利用这一丰富的行为数据，并在几分钟 [!DNL Real-time Customer Profile] 内丰富这些数据。

![](./images/analytics-data-experience-platform.png)

从高度上收集 [!DNL Analytics] 来自全球各个数字渠道和多个数据中心的数据。 一旦收集了访客，就会应用识别、分段和转换架构(VISTA)规则和处理规则来改变传入数据的形状。 在原始数据经过这种轻量处理后，它会被视为可供使用 [!DNL Real-time Customer Profile]。 在与上述过程平行的过程中，将相同的处理数据微批处理并引入平台数据集中，供 [!DNL Data Science Workspace]、和 [!DNL Query Service]其他数据发现应用使用。

有关处 [理规则的详细信息](https://docs.adobe.com/content/help/zh-Hans/analytics/admin/admin-tools/processing-rules/processing-rules.html) ，请参阅处理规则概述。

## 体验数据模型(XDM)

XDM是一个公开的文档规范，它为用于与上的服务通信的应用程序提供通用结构和定义 [!DNL Experience Platform]。

遵循XDM标准，可以统一整合数据，从而更轻松地交付数据和收集信息。

要进一步了解XDM，请参阅 [XDM系统概述](../../../xdm/home.md)。

## 如何将字段从Adobe Analytics映射到XDM?

当建立源连接以使用用 [!DNL Analytics] 户界 [!DNL Experience Platform] 面将数 [!DNL Platform] 据引入时，数据字段被自动映射并摄取到几分钟 [!DNL Real-time Customer Profile] 内。 有关使用UI创建源连接 [!DNL Analytics] 的说 [!DNL Platform] 明，请参阅 [Analytics数据连接器教程](../../tutorials/ui/create/adobe-applications/analytics.md)。

有关在和之间进行字段映射的详细 [!DNL Analytics] 信 [!DNL Experience Platform]息，请访问 [Adobe Analytics字段映射指南](./mapping/analytics.md) 。

## 平台上的Analytics数据预期的延迟是什么？

| Analytics 数据 | 预期延迟 |
| -------------- | ---------------- |
| 新数据 [!DNL Real-time Customer Profile] (未启 **用** A4T) | &lt; 2 分钟 |
| 新数据 [!DNL Real-time Customer Profile] (已启用 **A4** T) | &lt; 15 分钟 |
| 数据湖的新数据 | &lt; 45 分钟 |
| 回填数据(13个月的数据或100亿事件，以较低者为准) | &lt; 4 周 |

>[!NOTE] 延迟因客户配置、数据量和消费者应用程序而异。 例如，如果Analytics实施配置了管道 `A4T` 的延迟，则延迟将增加到5-10分钟。

## 分析数据中的主标识符

Analytics数据连接器的每次点击都包含一个主要标识符，它取决于ECID还是AAID存在。 如果有ECID，则将ECID指定为主标识符。 如果存在AAID，则将AAID指定为主AAID。
---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 分析数据连接器
topic: overview
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

---


# Analytics Data Connector

Adobe Experience Platform允许您通过Analytics Data Connector(ADC)获取Adobe Analytics数据。 ADC将Adobe Analytics收集到的数据实时流化到Platform，将SCDS格式的Analytics数据转换为Experience Data Model(XDM)字段，供Platform使用。

本文档概述了Adobe Analytics，并描述了Analytics数据的用例。

## Adobe Analytics和Analytics数据

Adobe Analytics是一款功能强大的引擎，可帮助您了解关于客户的更多信息、客户如何与您的Web资产交互、了解数字营销支出的有效位置并确定改进领域。 Adobe Analytics每年处理数万亿次Web交易，ADC使您能轻松利用这一丰富的行为数据，并在几分钟内丰富实时客户用户档案。

![](./images/analytics-data-experience-platform.png)

Adobe Analytics从高层次上收集来自全球各种数字渠道和多个数据中心的数据。 收集数据后，将应用访客识别、分段和转换架构(VISTA)规则和处理规则来形成传入数据。 在原始数据经过这种轻量级处理后，实时客户用户档案会认为它可供消费。 在与上述过程平行的过程中，相同的处理数据被微批处理并被引入平台数据集中，供数据科学工作区、查询服务和其他数据发现应用使用。

有关VISTA和处理规则的更多信息，请参阅以下文档:
* [VISTA规则概述](https://marketing.adobe.com/resources/help/zh_CN/reference/VISTA.html)
* [处理规则概述](https://docs.adobe.com/content/help/zh-Hans/analytics/admin/admin-tools/processing-rules/processing-rules.html)

## 体验数据模型(XDM)

XDM是一个公开的文档规范，它为应用程序提供了通用的结构和定义，以便用于与Adobe Experience Platform上的服务通信。

遵循XDM标准，可以统一整合数据，从而更轻松地交付数据和收集信息。

要进一步了解XDM，请参阅 [XDM系统概述](../../../xdm/home.md)。

## 如何将字段从Adobe Analytics映射到XDM?

当建立源连接以使用平台用户界面将Analytics数据引入Experience Platform时，数据字段会在几分钟内自动映射并引入实时客户用户档案。 有关使用平台UI创建与Adobe Analytics的源连接的说明，请参阅 [Analytics数据连接器教程](../../tutorials/ui/create/adobe-applications/analytics.md)。

有关Analytics和Experience Platform之间的字段映射的详细信息，请访问 [Adobe Analytics字段映射指南](./analytics-mapping.md) 。

## 平台上的Analytics数据预期的滞后时间是多少？

| Analytics 数据 | 预期延迟 |
| -------------- | ---------------- |
| 实时客户用户档案的新数据(未启 **用** A4T) | &lt; 2 分钟 |
| 实时客户用户档案的新数据(已启用A4T **** ) | &lt; 15 分钟 |
| 数据湖新数据 | &lt; 45 分钟 |
| 回填数据(13个月的数据或100亿事件，以较低者为准) | &lt; 4周 |

>[!NOTE] 延迟因客户配置、数据量和消费者应用程序而异。 例如，如果Analytics实施配置了“管 `A4T` 线”延迟，则延迟将增加到5-10分钟。
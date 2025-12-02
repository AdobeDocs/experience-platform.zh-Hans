---
solution: Experience Platform
title: 数据收集概述
description: 了解如何将数据发送到Adobe Experience Platform。
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 3d51f01d314587510d900d335dc92fedb8ac31e8
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---

# 数据收集概述

Adobe Experience Platform提供了一套方法，可让您从各种来源收集客户体验数据并将这些数据发送到Adobe Experience Platform Edge Network。 然后，可以扩充和转换这些数据，并将其分发到Adobe或非Adobe目标。

Adobe通过用于数据收集的专用库支持以下代码语言：

* **JavaScript**：适用于网站和基于Web的应用程序
* **Kotlin**：用于Android设备
* **Swift**：适用于iOS设备
* **Brightscript**：适用于Roku设备
* **颤动**：对于使用颤动的Android + iOS应用程序
* **React Native**：对于使用React Native的Android + iOS应用程序

Adobe Experience Platform数据收集中的标记UI包括Web SDK和Mobile SDK扩展。

如果上述SDK都不能满足您的项目需求，则可以使用[Adobe Experience Platform Edge Network API](https://developer.adobe.com/data-collection-apis/docs/)将数据直接发送到Adobe。

## 数据收集过程

您可以实施以上某个SDK或标记扩展，以将所有所需数据聚合到单个有效负载中，而不是为每个Adobe产品安装和实施单独的库。 该有效负载被发送到Adobe Experience Platform Edge Network中的[数据流](/help/datastreams/overview.md)。

![数据收集图表](assets/tags-sdks.png)

Adobe Experience Platform Edge Network是一个全球分布式、快速且可靠的服务器网络，能够大规模接收和处理数据。 当数据流接收数据时，它将该数据分发到您配置的各个解决方案。 数据以每个产品都能理解的格式传递。

![Adobe解决方案图表](assets/adobe-solutions.png)

您还可以使用[事件转发](/help/tags/ui/event-forwarding/overview.md)来转换、扩充数据，并将其发送到任何非Adobe目标，且延迟较低，无需任何客户端实现代码。

![事件转发图](assets/event-forwarding.png)

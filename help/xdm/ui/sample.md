---
solution: Experience Platform
title: 在UI中为XDM架构生成示例数据
description: 了解如何根据Adobe Experience Platform用户界面中的现有架构生成示例JSON数据。
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 在UI中生成XDM架构的示例数据

为了将数据摄取到Adobe Experience Platform，数据的格式和结构必须符合现有的Experience Data Model (XDM)架构。 根据特定数据集架构的复杂性，可能很难确定数据集在摄取时预期的数据的确切形状。

对于您在Experience PlatformUI中定义的任何架构，您可以生成符合架构结构的示例JSON对象。 此对象可以用作任何数据的模板，这些数据被摄取到采用相关架构的数据集中。

在Platform UI中，选择 **[!UICONTROL 架构]** 左侧导航栏中。 在 **[!UICONTROL 浏览]** 选项卡，找到要为其生成示例数据的架构。 从列表中选择它，右边栏更新以显示有关架构的详细信息。 从此处选择 **[!UICONTROL 下载样本文件]**.

![](../images/ui/sample/sample-data.png)

浏览器下载了一个JSON示例文件。 现在，您可以将此文件用作参考，以了解在摄取到采用此架构的数据集中时，如何构建数据。

## 后续步骤

本指南介绍了如何从平台UI中的XDM架构生成示例JSON文件。 要了解如何使用架构注册表API生成示例数据，请参阅 [示例数据端点指南](../api/sample-data.md).

准备好开始摄取数据后，请参阅上的教程 [将CSV文件映射到XDM](../../ingestion/tutorials/map-csv/overview.md) 了解如何将平面数据文件（如CSV）映射到XDM架构并将其摄取到Platform。 或者，您可以建立 [源连接](../../sources/home.md) 从外部源引入数据并将其映射到XDM。

欲知关于 [!UICONTROL 架构] 工作区，请参阅 [[!UICONTROL 架构] 工作区概述](./overview.md).

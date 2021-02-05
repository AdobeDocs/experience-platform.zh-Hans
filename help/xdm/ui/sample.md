---
solution: Experience Platform
title: 在UI中为XDM模式生成示例数据
description: 了解如何根据Adobe Experience Platform用户界面中的现有模式生成示例JSON数据。
topic: user guide
translation-type: tm+mt
source-git-commit: 87497ef8a0ebf8de8b6c2dff1650c0b982299e8a
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---


# 在UI中为XDM模式生成示例数据

要将数据引入Adobe Experience Platform，数据的格式和结构必须符合现有的体验数据模型(XDM)模式。 根据特定数据集的模式复杂性，很难确定数据集所期望的数据的确切形状。

对于在模式UI中定义的任何Experience Platform，您都可以生成符合模式结构的示例JSON对象。 此对象可用作任何被引入使用相关模式的数据集中的数据的模板。

在平台UI中，在左侧导航中选择&#x200B;**[!UICONTROL 模式]**。 在&#x200B;**[!UICONTROL 浏览]**&#x200B;选项卡下，找到要为其生成示例模式的。 从列表中选择它，右边栏将更新，显示有关模式的详细信息。 从此处选择&#x200B;**[!UICONTROL 下载示例文件]。**

![](../images/ui/sample/sample-data.png)

浏览器会下载示例JSON文件。 现在，您可以使用此文件作为在引入使用此模式的数据集时如何构建数据的参考。

## 后续步骤

本指南介绍如何在平台UI中从XDM模式生成示例JSON文件。 要了解如何使用模式注册表API生成示例数据，请参阅[示例数据端点指南](../api/sample-data.md)。

准备好开始数据后，请参阅教程[将CSV文件映射到XDM](../../ingestion/tutorials/map-a-csv-file.md)，学习如何将平面数据文件（如CSV）映射到XDM模式并将其引入平台。 或者，您也可以建立[源连接](../../sources/home.md)以从外部源导入数据并将其映射到XDM。

有关UI中[!UICONTROL 模式]工作区功能的详细信息，请参阅[[!UICONTROL 模式]工作区概述](./overview.md)。
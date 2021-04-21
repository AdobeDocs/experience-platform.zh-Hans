---
solution: Experience Platform
title: 在UI中为XDM模式生成示例数据
description: 了解如何根据Adobe Experience Platform用户界面中的现有模式生成示例JSON数据。
topic-legacy: user guide
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# 在UI中为XDM模式生成示例数据

要将数据引入Adobe Experience Platform，数据的格式和结构必须符合现有的体验数据模型(XDM)模式。 根据特定数据集的模式复杂性，可能难以确定数据集需要的数据的确切形状。

对于在Experience PlatformUI中定义的任何模式，您都可以生成一个符合模式结构的示例JSON对象。 此对象可以用作任何数据的模板，这些数据被引入到使用相关模式的数据集中。

在平台UI中，选择左侧导航中的&#x200B;**[!UICONTROL Schemas]**。 在&#x200B;**[!UICONTROL Browse]**&#x200B;选项卡下，找到要为其生成示例模式的位置。 从列表中选择它，右边栏会更新以显示有关模式的详细信息。 从此处选择&#x200B;**[!UICONTROL Download sample file]**。

![](../images/ui/sample/sample-data.png)

浏览器会下载示例JSON文件。 现在，您可以使用此文件作为参考，在引入使用此模式的数据集时，如何构造数据。

## 后续步骤

本指南介绍如何在平台UI中从XDM模式生成示例JSON文件。 要了解如何使用模式 Registry API生成示例数据，请参阅[示例数据终结点指南](../api/sample-data.md)。

准备好开始模式数据后，请参阅教程[将CSV文件映射到XDM](../../ingestion/tutorials/map-a-csv-file.md)，了解如何将平面数据文件（如CSV）映射到XDM并将其引入平台。 或者，您可以建立[源连接](../../sources/home.md)以从外部源导入数据并将其映射到XDM。

有关UI中[!UICONTROL Schemas]工作区功能的详细信息，请参阅[[!UICONTROL Schemas]工作区概述](./overview.md)。

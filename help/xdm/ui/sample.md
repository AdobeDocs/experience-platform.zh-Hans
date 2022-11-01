---
solution: Experience Platform
title: 在UI中为XDM架构生成示例数据
description: 了解如何根据Adobe Experience Platform用户界面中的现有架构生成示例JSON数据。
topic-legacy: user guide
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
source-git-commit: d380b4d2a75efb1c34010a30c619649a7b99643c
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 在UI中为XDM架构生成示例数据

要将数据摄取到Adobe Experience Platform中，数据的格式和结构必须符合现有的体验数据模型(XDM)架构。 根据特定数据集架构的复杂性，可能很难确定数据集在摄取时所需数据的确切形状。

对于您在Experience PlatformUI中定义的任何架构，您可以生成一个符合该架构结构的示例JSON对象。 此对象可用作模板，用于摄取到使用相关架构的数据集中的任何数据。

在平台UI中，选择 **[!UICONTROL 模式]** 中。 在 **[!UICONTROL 浏览]** 选项卡，找到要为其生成示例数据的架构。 从列表中选择该架构，右边栏会更新以显示有关架构的详细信息。 从此处选择 **[!UICONTROL 下载样例文件]**.

![](../images/ui/sample/sample-data.png)

浏览器将下载示例JSON文件。 现在，您可以使用此文件作为参考，以了解在摄取到使用此模式的数据集时如何构建数据。

## 后续步骤

本指南介绍了如何从平台UI中的XDM架构生成示例JSON文件。 要了解如何使用模式注册表API生成示例数据，请参阅 [示例数据端点指南](../api/sample-data.md).

准备好开始摄取数据后，请参阅 [将CSV文件映射到XDM](../../ingestion/tutorials/map-csv/overview.md) 了解如何将平面数据文件（如CSV）映射到XDM架构，并将其摄取到平台中。 或者，您也可以建立 [源连接](../../sources/home.md) 从外部源导入数据并将其映射到XDM。

有关 [!UICONTROL 模式] 工作区中，请参阅 [[!UICONTROL 模式] 工作区概述](./overview.md).

---
title: “网络”选项卡
description: 了解如何使用Adobe Experience Platform Debugger中的“网络”选项卡。
keywords: debugger;experience Platform Debugger 扩展程序;chrome;扩展程序;网络;信息
seo-description: Experience Platform Debugger Network screen
seo-title: Network Tab
uuid: 839686c9-6e4f-4661-acf6-150ea24dc47f
exl-id: ed0579ef-ec26-43df-9453-a395c105038a
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 62%

---

# “网络”选项卡

此 **网络** 选项卡汇总页面上发出的所有Adobe Experience Cloud解决方案调用，并按从左到右的顺序显示它们。 标准参数会自动标示友好名称，并按照相同的角色对常用参数进行分组。

![](images/network.jpg)

这个屏幕可用来比较点击量中的键值对。您可以确认用于集成的参数（例如 Experience Cloud 访客 ID 或补充数据 ID）是否在集成中保持一致。

>[!NOTE]
>
>目前，并非所有在解决方案调用中传递的参数都在“网络”屏幕中可见，例如，Analytics 上下文变量、Target 自定义参数或 Experience Cloud ID 服务客户 ID。

要按解决方案更改信息，请从左侧导航列表中选择要查看的解决方案。以下是经过筛选，仅显示 Analytics 的示例：

![](images/network-analytics.jpg)

要重新显示所有解决方案，请选择 **[!UICONTROL 网络]**

在“网络”视图中选择项目以查看展开视图。 从展开的视图窗口中，可以将显示的信息复制到“剪贴板”。

![](images/network-expand.jpg)

<!--Use the icon at the top of each column to copy the server call URL to your clipboard, where you can paste it into another document for reference or debugging purposes.

![](images/copy.jpg)-->

要清除列表，请选择 **[!UICONTROL 删除事件]**.

要下载包含此屏幕上的信息的Excel文件，请选择 **[!UICONTROL 下载]**.

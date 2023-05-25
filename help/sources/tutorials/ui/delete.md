---
keywords: Experience Platform；主页；热门主题；删除数据流
description: 通过源工作区，您可以删除包含错误或已过时的现有批处理数据流和流式数据流。
solution: Experience Platform
title: 删除UI中的数据流
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 1%

---

# 删除UI中的数据流

此 [!UICONTROL 源] 工作区允许您删除包含错误或已过时的现有批处理数据流和流数据流。

本教程提供了使用删除数据流的步骤。 [!UICONTROL 源] 工作区。

## 快速入门

本教程需要深入了解Adobe Experience Platform的以下组件：

- [源](../../home.md)： [!DNL Experience Platform] 允许从各种源摄取数据，同时让您能够使用以下方式构建、标记和增强传入数据： [!DNL Platform] 服务。
- [沙盒](../../../sandboxes/home.md)： [!DNL Experience Platform] 提供对单个进行分区的虚拟沙盒 [!DNL Platform] 将实例安装到单独的虚拟环境中，以帮助开发和改进数字体验应用程序。

## 删除数据流

在 [EXPERIENCE PLATFORMUI](https://platform.adobe.com)，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区，然后选择 **[!UICONTROL 数据流]** 从顶部标题中。

![目录](../../images/tutorials/delete/catalog.png)

此 **[!UICONTROL 数据流]** 页面。 在此页面上是可查看的数据流列表，包括有关其目标数据集、源、帐户名称和创建日期的信息。

选择过滤器图标(![筛选图标](../../images/tutorials/delete/filter.png))，以启动“排序”面板。

![数据流](../../images/tutorials/delete/dataflows.png)

排序面板提供所有源的列表。 您可以从列表中选择多个源，以访问与所选特定源关联的数据流过滤选择。

选择要使用的源以查看其现有数据流的列表。 标识要删除的数据流后，选择省略号(`...`)。

![数据流 — 过滤器](../../images/tutorials/delete/dataflows-filter.png)

此时会显示一个下拉菜单，为您提供编辑数据流计划、禁用数据流或完全删除数据流的选项。

选择 **[!UICONTROL 删除]** 以删除数据流。

![delete](../../images/tutorials/delete/delete.png)

将出现最终确认对话框。 选择 **[!UICONTROL 删除]** 以完成该过程。

![confirm](../../images/tutorials/delete/confirm.png)

片刻后，屏幕底部会显示一个确认框，用于确认成功删除。

![已确认](../../images/tutorials/delete/confirmed.png)

## 后续步骤

按照本教程中的说明，您已成功使用了 [!UICONTROL 源] 工作区以删除现有数据流。

请参阅上的教程 [使用流服务API删除数据流](../../tutorials/api/delete-dataflows.md) 有关如何使用API调用以编程方式执行这些操作的步骤。

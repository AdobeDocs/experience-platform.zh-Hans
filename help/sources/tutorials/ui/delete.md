---
keywords: Experience Platform；主页；热门主题；删除数据流
description: “源”工作区允许您删除包含错误或已过时的现有批处理和流数据流。
solution: Experience Platform
title: 在UI中删除数据流
topic-legacy: overview
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 1%

---

# 在UI中删除数据流

[!UICONTROL Sources]工作区允许您删除包含错误或已过时的现有批处理和流数据流。

本教程提供了使用[!UICONTROL Sources]工作区删除数据流的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

- [来源](../../home.md): [!DNL Experience Platform] 允许从各种来源摄取数据，同时使您能够使用服务来构建、标记和增强传入数 [!DNL Platform] 据。
- [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供将单个实例分区为单 [!DNL Platform] 独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

## 删除数据流

在[Experience PlatformUI](https://platform.adobe.com)中，从左侧导航中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区，然后从顶部标题中选择&#x200B;**[!UICONTROL Dataflows]**。

![目录](../../images/tutorials/delete/catalog.png)

将显示&#x200B;**[!UICONTROL Dataflows]**&#x200B;页。 本页是可查看目标流的列表，包括有关其数据集、源、帐户名称和创建日期的信息。

选择左上角的过滤器图标(![filter-icon](../../images/tutorials/delete/filter.png))以启动排序面板。

![数据流](../../images/tutorials/delete/dataflows.png)

排序面板提供所有源的列表。 您可以从列表中选择多个源，以访问与所选特定源关联的已过滤数据流的选定内容。

选择要处理的源，以查看其现有数据流的列表。 确定要删除的数据流后，请选择数据流名称旁边的省略号(`...`)。

![数据流 — 过滤器](../../images/tutorials/delete/dataflows-filter.png)

此时会显示一个下拉菜单，其中提供了用于编辑数据流计划、禁用数据流或完全删除数据流的选项。

选择&#x200B;**[!UICONTROL Delete]**&#x200B;以删除数据流。

![删除](../../images/tutorials/delete/delete.png)

此时将显示最终确认对话框。 选择&#x200B;**[!UICONTROL Delete]**&#x200B;以完成该过程。

![confirm](../../images/tutorials/delete/confirm.png)

几分钟后，屏幕底部会出现一个确认框，确认成功删除。

![确认](../../images/tutorials/delete/confirmed.png)

## 后续步骤

通过本教程，您已成功使用[!UICONTROL Sources]工作区删除现有数据流。

有关如何使用API调用以编程方式执行这些操作的步骤，请参见有关使用Flow Service API](../../tutorials/api/delete-dataflows.md)删除数据流的教程。[

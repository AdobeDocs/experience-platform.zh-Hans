---
keywords: 删除目标，如何删除目标，删除目标
title: 删除目标
type: Tutorial
description: 本教程列出了在Adobe Experience Platform UI中删除现有目标的步骤
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: 1ef6430b6661a2b8b5aef196b75cfaf3f6220aab
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# 删除目标 {#delete-destinations}

## 概述 {#overview}

在Adobe Experience Platform用户界面中，您可以删除与目标的现有连接。

删除目标会将任何现有数据流删除到该目标。 在删除数据流之前，激活到您删除的目标的所有区段都未映射。

您可以通过两种方式从 [!DNL Platform] [!DNL UI]. 您可以：

* [从 [!UICONTROL 浏览] 选项卡](#delete-browse-tab)
* [从目标详细信息页面中删除目标](#delete-destination-details-page)

## 从“浏览”选项卡中删除目标{#delete-browse-tab}

按照以下步骤从 [!UICONTROL 浏览] 选项卡。

1. 登录到 [Experience PlatformUI](https://platform.adobe.com/) 选择 **[!UICONTROL 目标]** 中。 要查看现有目标，请选择 **[!UICONTROL 浏览]** 中。

   ![浏览目标](../assets/ui/delete-destinations/browse-destinations.png)

2. 选择过滤器图标 ![过滤器图标](../assets/ui/delete-destinations/filter.png) 来启动排序面板。 排序面板提供了所有目标的列表。 您可以从列表中选择多个目标，以查看与选定目标关联的已过滤数据流选项。

   ![筛选目标](../assets/ui/delete-destinations/filter-destinations.png)

3. 选择 ![“更多”按钮](../assets/ui/delete-destinations/more-icon.png) 按钮，然后选择 ![“删除”按钮](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL 删除]** 删除现有目标连接。
   ![删除目标](../assets/ui/delete-destinations/delete-destinations.png)

4. 选择 **[!UICONTROL 删除]** 确认删除目标连接。

   ![确认删除目标](../assets/ui/delete-destinations/delete-destinations-confirm.png)

## 从目标详细信息页面中删除目标{#delete-destination-details-page}

请按照以下步骤从目标详细信息页面中删除目标。

1. 登录到 [Experience PlatformUI](https://platform.adobe.com/) 选择 **[!UICONTROL 目标]** 中。 要查看现有目标，请选择 **[!UICONTROL 浏览]** 中。

   ![浏览目标](../assets/ui/delete-destinations/browse-destinations.png)

2. 选择过滤器图标 ![过滤器图标](../assets/ui/delete-destinations/filter.png) 来启动排序面板。 排序面板提供了所有目标的列表。 您可以从列表中选择多个目标，以查看与选定目标关联的已过滤数据流选项。

   ![筛选目标](../assets/ui/delete-destinations/filter-destinations.png)

3. 选择要删除的目标名称。

   ![选择目标](../assets/ui/delete-destinations/delete-destination-select.png)

   * 如果目标具有现有数据流，则会将您转到 [!UICONTROL 数据流运行] 选项卡。

      ![“数据流运行”选项卡](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * 如果目标没有现有数据流，您将转到一个空页面，您可以在该页面中开始激活受众。

      ![目标详细信息](../assets/ui/delete-destinations/destination-details-empty.png)

4. 选择 **[!UICONTROL 删除]** 中。

   ![删除目标](../assets/ui/delete-destinations/delete-destinations-button.png)

5. 选择 **[!UICONTROL 删除]** 在确认对话框中，删除目标。

   ![删除目标确认](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >根据服务器负载的不同，可能需要几分钟 [!DNL Platform] 删除目标。

---
keywords: 删除目标
title: 删除目标
type: 教程
description: 本教程列表了在Adobe Experience Platform UI中删除现有目标的步骤
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
translation-type: tm+mt
source-git-commit: 07869d63f395bbab6c49a3976051facdf94d43b7
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 1%

---

# 删除目标{#delete-destinations}

## 概述 {#overview}

在Adobe Experience Platform用户界面中，您可以删除与目标的现有连接。

删除目标将删除到该目标的任何现有数据流。 在删除数据流之前，所有已激活到您删除的目标的区段都将取消映射。

有两种方法可从[!DNL Platform] [!DNL UI]中删除目标。 您可以：

* [从选项卡中删除目 [!UICONTROL Browse] 标](#delete-browse-tab)
* [从“目标详细信息”页中删除目标](#delete-destination-details-page)

## 从“浏览”选项卡{#delete-browse-tab}中删除目标

请按照以下步骤从[!UICONTROL Browse]选项卡中删除目标。

1. 登录到[Experience PlatformUI](https://platform.adobe.com/)并从左侧导航栏中选择&#x200B;**[!UICONTROL Destinations]**。 要视图现有目标，请从顶部标题中选择&#x200B;**[!UICONTROL Browse]**。

   ![浏览目标](../assets/ui/delete-destinations/browse-destinations.png)

2. 选择左上角的过滤器图标![过滤器图标](../assets/ui/delete-destinations/filter.png)以启动排序面板。 排序面板提供所有目标的列表。 您可以从列表中选择多个目标，以查看与所选目标关联的数据流的筛选选择。

   ![筛选目标](../assets/ui/delete-destinations/filter-destinations.png)

3. 在&#x200B;**[!UICONTROL Platform]**&#x200B;列中选择![删除按钮](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL Delete]**按钮以删除现有目标。
   ![删除目标](../assets/ui/delete-destinations/delete-destinations.png)

4. 选择&#x200B;**[!UICONTROL Delete]**&#x200B;以确认删除目标。

   ![确认删除目标](../assets/ui/delete-destinations/delete-destinations-confirm.png)


## 从目标详细信息页面{#delete-destination-details-page}中删除目标

请按照以下步骤从目标详细信息页面中删除目标。

1. 登录到[Experience PlatformUI](https://platform.adobe.com/)并从左侧导航栏中选择&#x200B;**[!UICONTROL Destinations]**。 要视图现有目标，请从顶部标题中选择&#x200B;**[!UICONTROL Browse]**。

   ![浏览目标](../assets/ui/delete-destinations/browse-destinations.png)

2. 选择左上角的过滤器图标![过滤器图标](../assets/ui/delete-destinations/filter.png)以启动排序面板。 排序面板提供所有目标的列表。 您可以从列表中选择多个目标，以查看与所选目标关联的数据流的筛选选择。

   ![筛选目标](../assets/ui/delete-destinations/filter-destinations.png)

3. 选择要删除的目标的名称。

   ![选择目标](../assets/ui/delete-destinations/delete-destination-select.png)

   * 如果目标有现有数据流，则转到[!UICONTROL Dataflow runs]选项卡。

      ![“数据流运行”选项卡](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * 如果目标没有现有受众，您将转到一个空页面，在该页面中可以激活数据。

      ![目标详细信息](../assets/ui/delete-destinations/destination-details-empty.png)


4. 在右边栏中选择&#x200B;**[!UICONTROL Delete]**。

   ![删除目标](../assets/ui/delete-destinations/delete-destinations-button.png)

5. 在确认对话框中选择&#x200B;**[!UICONTROL Delete]**&#x200B;以删除目标。

   ![删除目标确认](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >根据服务器负载，[!DNL Platform]删除目标可能需要几分钟时间。

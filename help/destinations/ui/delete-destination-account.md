---
keywords: 删除目标帐户、目标帐户、如何删除帐户
title: 删除目标帐户
type: Tutorial
description: 本教程列出了在Adobe Experience Platform UI中删除目标帐户的步骤
exl-id: 9b39ba4b-19a4-48a8-a6f1-f860777cdb9e
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 删除目标帐户

## 概述 {#overview}

此 **[!UICONTROL 帐户]** 选项卡显示有关您与各种目标建立的连接的详细信息。 请参阅 [帐户概述](../ui/destinations-workspace.md#accounts) 以获取有关每个目标帐户的所有信息。

本教程介绍了使用Experience PlatformUI删除不再需要的目标帐户的步骤。

![“帐户”选项卡](../assets/ui/update-accounts/destination-accounts.png)

## 删除帐户 {#delete}

>[!TIP]
>
>在删除目标帐户之前，必须首先删除与目标帐户关联的任何现有数据流。 要删除现有目标数据流，请参阅上的教程 [在UI中删除目标数据流](./delete-destinations.md).

按照以下步骤删除现有目标帐户。

1. 登录到 [EXPERIENCE PLATFORMUI](https://platform.adobe.com/) 并选择 **[!UICONTROL 目标]** 左侧导航栏中的。 选择 **[!UICONTROL 帐户]** 查看现有帐户。

   ![“帐户”选项卡](../assets/ui/delete-accounts/accounts-tab.png)

2. 选择过滤器图标 ![筛选图标](../assets/ui/update-accounts/filter.png) 以启动“排序”面板。 排序面板提供所有目标的列表。 您可以从列表中选择多个目标，以查看与所选目标关联的已过滤帐户选择。

   ![筛选目标](../assets/ui/delete-accounts/filter-accounts.png)

3. 选择省略号(`...`)。 此时将显示一个弹出面板，其中提供以下选项 **[!UICONTROL 激活受众]**， **[!UICONTROL 编辑详细信息]**、和 **[!UICONTROL 删除]** 帐户。 选择 ![“删除”按钮](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL 删除]** 按钮以删除所需的帐户。

   ![删除目标帐户](../assets/ui/delete-accounts/delete-accounts.png)

4. 出现最终确认对话框，选择 **[!UICONTROL 删除]** 以完成该过程。

![确认帐户删除](../assets/ui/delete-accounts/confirm-account-deletion.png)

## 后续步骤

通过阅读本教程，您已成功使用目标工作区删除现有帐户。

有关如何使用以编程方式执行这些操作的步骤 [!DNL Flow Service] API，请参考以下教程： [使用流服务API删除连接](../api/delete-destination-account.md)

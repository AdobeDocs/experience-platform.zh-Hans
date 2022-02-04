---
keywords: 删除目标帐户、目标帐户，如何删除帐户
title: 删除目标帐户
type: Tutorial
description: 本教程列出了在Adobe Experience Platform UI中删除目标帐户的步骤
source-git-commit: f31b54622c63f96fb8fa727f80dda295a926e2c7
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 删除目标帐户

## 概述 {#overview}

的 **[!UICONTROL 帐户]** 选项卡会显示有关您已与各种目标建立的连接的详细信息。 请参阅 [帐户概述](../ui/destinations-workspace.md#accounts) 您可以获取每个目标帐户的所有信息。

本教程介绍了使用Experience PlatformUI删除不再需要的目标帐户的步骤。

![“帐户”选项卡](../assets/ui/update-accounts/destination-accounts.png)

## 删除帐户 {#delete}

>[!TIP]
>
>在删除目标帐户之前，必须首先删除与目标帐户关联的任何现有数据流。 要删除现有目标数据流，请参阅 [删除UI中的目标数据流](./delete-destinations.md).

请按照以下步骤删除现有目标帐户。

1. 登录到 [Experience PlatformUI](https://platform.adobe.com/) 选择 **[!UICONTROL 目标]** 中。 选择 **[!UICONTROL 帐户]** 来查看您的现有帐户。

   ![“帐户”选项卡](../assets/ui/delete-accounts/accounts-tab.png)

2. 选择过滤器图标 ![过滤器图标](../assets/ui/update-accounts/filter.png) 来启动排序面板。 排序面板提供了所有目标的列表。 您可以从列表中选择多个目标，以查看与选定目标关联的已筛选帐户选择。

   ![筛选目标](../assets/ui/delete-accounts/filter-accounts.png)

3. 选择省略号(`...`)。 此时会出现一个弹出面板，其中提供了 **[!UICONTROL 激活区段]**, **[!UICONTROL 编辑详细信息]**&#x200B;和 **[!UICONTROL 删除]** 帐户。 选择 ![“删除”按钮](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL 删除]** 按钮以删除所需的帐户。

   ![删除目标帐户](../assets/ui/delete-accounts/delete-accounts.png)

4. 出现最终确认对话框，选择 **[!UICONTROL 删除]** 以完成该过程。

![确认删除帐户](../assets/ui/delete-accounts/confirm-account-deletion.png)

## 后续步骤

通过阅读本教程，您已成功使用目标工作区删除现有帐户。

有关如何使用 [!DNL Flow Service] API，请参阅 [使用流量服务API删除连接](../api/delete-destination-account.md)

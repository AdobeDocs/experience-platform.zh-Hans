---
keywords: 删除目标帐户、目标帐户以及如何删除帐户
title: 删除目标帐户
type: Tutorial
description: 本教程列出了在Adobe Experience Platform UI中删除目标帐户的步骤
exl-id: 9b39ba4b-19a4-48a8-a6f1-f860777cdb9e
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# 删除目标帐户

## 概述 {#overview}

**[!UICONTROL 帐户]**&#x200B;选项卡显示有关您与各种目标建立的连接的详细信息。 请参阅[帐户概述](../ui/destinations-workspace.md#accounts)，以了解有关每个目标帐户的所有信息。

本教程介绍了使用Experience PlatformUI删除不再需要的目标帐户的步骤。

![帐户选项卡](../assets/ui/update-accounts/destination-accounts.png)

## 删除帐户 {#delete}

>[!TIP]
>
>在删除目标帐户之前，必须首先删除与目标帐户关联的任何现有数据流。 要删除现有的目标数据流，请参阅有关在UI[&#128279;](./delete-destinations.md)中删除目标数据流的教程。

请按照以下步骤删除现有目标帐户。

1. 登录到[Experience PlatformUI](https://platform.adobe.com/)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 目标]**。 从顶部标题中选择&#x200B;**[!UICONTROL 帐户]**&#x200B;以查看现有帐户。

   ![帐户选项卡](../assets/ui/delete-accounts/accounts-tab.png)

2. 选择左上角的过滤器图标![过滤器图标](/help/images/icons/filter.png)以启动排序面板。 排序面板提供所有目标的列表。 您可以从列表中选择多个目标，以查看与所选目标关联的已过滤帐户选择。

   ![筛选目标](../assets/ui/delete-accounts/filter-accounts.png)

3. 选择要删除的帐户名称旁边的省略号(`...`)。 此时会显示一个弹出面板，其中提供了&#x200B;**[!UICONTROL 激活受众]**、**[!UICONTROL 编辑详细信息]**&#x200B;和&#x200B;**[!UICONTROL 删除]**&#x200B;帐户的选项。 选择![删除按钮](/help/images/icons/delete.png) **[!UICONTROL 删除]**&#x200B;按钮以删除所需的帐户。

   ![删除目标帐户](../assets/ui/delete-accounts/delete-accounts.png)

4. 出现最终确认对话框，选择&#x200B;**[!UICONTROL 删除]**&#x200B;以完成该过程。

![确认删除帐户](../assets/ui/delete-accounts/confirm-account-deletion.png)

## 后续步骤

通过学习本教程，您已成功使用目标工作区删除现有帐户。

有关如何使用[!DNL Flow Service] API以编程方式执行这些操作的步骤，请参阅有关使用流服务API [删除连接的教程](../api/delete-destination-account.md)

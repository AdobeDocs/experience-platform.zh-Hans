---
keywords: Experience Platform；主页；热门主题；更新帐户
description: 在某些情况下，可能需要更新现有源帐户的详细信息。 通过源工作区，您可以添加、编辑和删除现有批处理或流连接的详细信息，包括其名称、描述和凭据。
solution: Experience Platform
title: 在UI中更新Source连接帐户详细信息
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 1%

---

# 在UI中更新帐户详细信息

在某些情况下，可能需要更新现有源帐户的详细信息。 [!UICONTROL 源]工作区允许您添加、编辑和删除现有批次或流连接的详细信息，包括其名称、描述和凭据。

本教程提供了从[!UICONTROL 源]工作区更新现有帐户的详细信息和凭据的步骤。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

- [源](../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
- [沙盒](../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 更新帐户

登录到[Experience Platform UI](https://platform.adobe.com)，然后从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 从顶部标题中选择&#x200B;**[!UICONTROL 帐户]**&#x200B;以查看现有帐户。

![目录](../../images/tutorials/update/catalog.png)

此时会显示&#x200B;**[!UICONTROL 帐户]**&#x200B;页面。 本页是可查看帐户的列表，包括有关其源、用户名、数据流数量和创建日期的信息。

选择左上角的过滤器图标![过滤器](/help/images/icons/filter.png)以启动排序面板。

![帐户列表](../../images/tutorials/update/accounts-list.png)

排序面板提供所有源的列表。 您可以从列表中选择多个源，以访问与不同源关联的已过滤的帐户选择。

选择要使用的源以查看其现有帐户的列表。 标识要更新的帐户后，选择帐户名称旁边的省略号(`...`)。

![帐户排序](../../images/tutorials/update/accounts-sort.png)

出现下拉菜单，为您提供&#x200B;**[!UICONTROL 添加数据]**、**[!UICONTROL 编辑详细信息]**&#x200B;和&#x200B;**[!UICONTROL 删除]**&#x200B;的选项。 从菜单中选择&#x200B;**[!UICONTROL 编辑详细信息]**&#x200B;以更新您的帐户。

![更新](../../images/tutorials/update/update.png)

通过&#x200B;**[!UICONTROL 编辑帐户详细信息]**&#x200B;对话框，您可以更新帐户的名称、描述和身份验证凭据。 更新所需信息后，选择&#x200B;**[!UICONTROL 保存]**。

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

片刻后，屏幕底部会显示一个确认框，用于确认更新是否成功。

![更新已确认](../../images/tutorials/update/update-confirmed.png)

## 后续步骤

通过完成本教程，您已成功使用[!UICONTROL 源]工作区来更新现有源帐户的信息。

有关如何使用[!DNL Flow Service] API以编程方式执行这些操作的步骤，请参阅有关[使用流服务API更新连接信息的教程](../../tutorials/api/update.md)。

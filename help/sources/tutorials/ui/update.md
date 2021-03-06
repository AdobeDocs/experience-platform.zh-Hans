---
keywords: Experience Platform；主页；热门主题；更新帐户
description: 在某些情况下，可能需要更新现有源帐户的详细信息。 “源”工作区允许您添加、编辑和删除现有批处理或流连接的详细信息，包括其名称、说明和凭据。
solution: Experience Platform
title: 在UI中更新源连接帐户详细信息
topic-legacy: overview
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# 在UI中更新帐户详细信息

在某些情况下，可能需要更新现有源帐户的详细信息。 [!UICONTROL Sources]工作区允许您添加、编辑和删除现有批处理或流连接的详细信息，包括其名称、说明和凭据。

本教程提供了从[!UICONTROL Sources]工作区更新现有帐户的详细信息和凭据的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

- [来源](../../home.md):Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
- [沙箱](../../../sandboxes/home.md):Experience Platform提供将单个平台实例分为单独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

## 更新帐户

登录到[Experience PlatformUI](https://platform.adobe.com)，然后从左侧导航中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区。 从顶部标题中选择&#x200B;**[!UICONTROL Accounts]**&#x200B;以视图现有帐户。

![目录](../../images/tutorials/update/catalog.png)

将显示&#x200B;**[!UICONTROL Accounts]**&#x200B;页。 本页是可查看帐户的列表，包括有关其源、用户名、数据流数和创建日期的信息。

选择左上角的过滤器图标![过滤器](../../images/tutorials/update/filter.png)以启动排序面板。

![帐户列表](../../images/tutorials/update/accounts-list.png)

排序面板提供所有源的列表。 您可以从列表中选择多个源，以访问与不同源关联的筛选帐户选择。

选择要处理的源，以查看其现有帐户的列表。 确定要更新的帐户后，请选择帐户名称旁边的省略号(`...`)。

![accounts-sort](../../images/tutorials/update/accounts-sort.png)

此时将显示一个下拉菜单，其中提供了&#x200B;**[!UICONTROL Add data]**、**[!UICONTROL Edit details]**&#x200B;和&#x200B;**[!UICONTROL Delete]**&#x200B;的选项。 从菜单中选择&#x200B;**[!UICONTROL Edit details]**&#x200B;以更新您的帐户。

![更新](../../images/tutorials/update/update.png)

**[!UICONTROL Edit account details]**&#x200B;对话框允许您更新帐户的名称、说明和身份验证凭据。 更新所需信息后，选择&#x200B;**[!UICONTROL Save]**。

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

稍后，屏幕底部会显示一个确认框，确认更新成功。

![update-confirmed](../../images/tutorials/update/update-confirmed.png)

## 后续步骤

通过本教程，您已成功使用[!UICONTROL Sources]工作区更新现有源帐户的信息。

有关如何使用[!DNL Flow Service] API以编程方式执行这些操作的步骤，请参阅有关使用流服务API](../../tutorials/api/update.md)更新连接信息的教程。[

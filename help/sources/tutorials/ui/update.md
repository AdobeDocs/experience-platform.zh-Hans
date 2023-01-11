---
keywords: Experience Platform；主页；热门主题；更新帐户
description: 在某些情况下，可能需要更新现有来源帐户的详细信息。 “源”工作区允许您添加、编辑和删除现有批处理或流连接的详细信息，包括其名称、描述和凭据。
solution: Experience Platform
title: 在UI中更新源连接帐户详细信息
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# 在UI中更新帐户详细信息

在某些情况下，可能需要更新现有来源帐户的详细信息。 的 [!UICONTROL 源] 工作区允许您添加、编辑和删除现有批处理连接或流连接的详细信息，包括其名称、描述和凭据。

本教程提供了从 [!UICONTROL 源] 工作区。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

- [源](../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
- [沙箱](../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

## 更新帐户

登录到 [Experience PlatformUI](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 选择 **[!UICONTROL 帐户]** 查看现有帐户。

![目录](../../images/tutorials/update/catalog.png)

的 **[!UICONTROL 帐户]** 页面。 本页列出了可查看帐户，包括有关其来源、用户名、数据流数和创建日期的信息。

选择过滤器图标 ![过滤器](../../images/tutorials/update/filter.png) 来启动排序面板。

![accounts-list](../../images/tutorials/update/accounts-list.png)

排序面板提供所有源的列表。 您可以从列表中选择多个源，以访问与不同源关联的已过滤帐户选择。

选择您要使用的来源，以查看其现有帐户的列表。 确定要更新的帐户后，选择省略号(`...`)。

![accounts-sort](../../images/tutorials/update/accounts-sort.png)

此时会出现一个下拉菜单，为您提供 **[!UICONTROL 添加数据]**, **[!UICONTROL 编辑详细信息]**&#x200B;和 **[!UICONTROL 删除]**. 选择 **[!UICONTROL 编辑详细信息]** 来更新您的帐户。

![更新](../../images/tutorials/update/update.png)

的 **[!UICONTROL 编辑帐户详细信息]** 对话框允许您更新帐户的名称、说明和身份验证凭据。 更新所需信息后，选择 **[!UICONTROL 保存]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

片刻后，屏幕底部会显示一个确认框，确认更新成功。

![更新 — 确认](../../images/tutorials/update/update-confirmed.png)

## 后续步骤

通过阅读本教程，您已成功使用 [!UICONTROL 源] 工作区以更新现有源帐户的信息。

有关如何使用 [!DNL Flow Service] API，请参阅 [使用流服务API更新连接信息](../../tutorials/api/update.md).

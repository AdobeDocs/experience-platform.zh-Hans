---
keywords: Experience Platform;home;popular topics;update accounts;
description: null
solution: Experience Platform
title: 在UI中更新帐户详细信息
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 413687a0d9e790ea3f61a858002e9510216d7c34
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---


# 在UI中更新帐户详细信息

在某些情况下，可能需要更新现有源帐户的详细信息。 Sources [!UICONTROL 工作区] 可让您编辑、添加和删除帐户的详细信息，包括帐户名称、说明和身份验证凭据的值。

本教程提供了从“源”工作区更新现有帐户的详细信息和凭 [!UICONTROL 据的步] 骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   - [模式合成基础](../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL Real-time Customer Profile]](../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

## 更新帐户

登录以登录到Experience Platform [UI](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航]** 中选择 [!UICONTROL “源] ”以访问“源”工作区。 从顶 **[!UICONTROL 部标题]** 中选择帐户以视图现有帐户。

![目录](../../images/tutorials/update/catalog.png)

将显 **[!UICONTROL 示]** “帐户”页。 本页是可查看帐户的列表，包括有关其源、用户名、数据流数和创建日期的信息。

选择左上角 ![的筛选](../../images/tutorials/update/filter.png) 器图标筛选器以启动排序面板。

![帐户列表](../../images/tutorials/update/accounts-list.png)

排序面板提供所有源的列表。 您可以从列表中选择多个源，以访问与不同源关联的筛选帐户的选择。

选择要处理的源，以查看其现有帐户的列表。 确定要更新的帐户后，请选择帐户名称旁`...`的省略号()。

![accounts-sort](../../images/tutorials/update/accounts-sort.png)

此时会显示一个下拉菜单，其中提供 **[!UICONTROL 了添加数据]**、 **[!UICONTROL 编辑详细信]****[!UICONTROL 息和删]**&#x200B;除选项。 从菜 **[!UICONTROL 单中选择]** “编辑详细信息”以更新您的帐户。

![更新](../../images/tutorials/update/update.png)

在“ **[!UICONTROL 编辑帐户详细信息]** ”对话框中，可以更新帐户的名称、说明和身份验证凭据。 更新所需信息后，选择“保 **[!UICONTROL 存]**”。

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

片刻后，屏幕底部将显示一个绿色确认框，确认成功更新。

![更新确认](../../images/tutorials/update/update-confirmed.png)

## 后续步骤

通过遵循本教程，您成功地使用 [!UICONTROL 了Sources] 工作区更新帐户信息。

有关如何使用API以编程方式执行这些操 [!DNL Flow Service] 作的步骤，请参阅有关使用 [Flow Service API更新连接信息的教程](../../tutorials/api/update.md)。
---
keywords: Experience Platform；主页；热门主题；删除帐户
description: Adobe Experience Platform中的源连接器提供了按计划摄取外部源数据的功能。 本教程提供了从“源”工作区中删除帐户的步骤。
solution: Experience Platform
title: 在UI中删除源连接帐户
topic-legacy: overview
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# 删除源连接帐户

Adobe Experience Platform中的源连接器提供了按计划摄取外部源数据的功能。 本教程提供了从 **[!UICONTROL 源]** 工作区。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../xdm/home.md):标准化框架， [!DNL Experience Platform] 组织客户体验数据。
   - [架构组合的基础知识](../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   - [模式编辑器教程](../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

## 使用UI删除帐户

>[!TIP]
>
>在删除源帐户之前，必须首先删除与源帐户关联的任何现有数据流。 要删除现有数据流，请参阅 [删除UI中的源数据流](./delete.md).

登录到 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 从左侧导航栏访问 **[!UICONTROL 源]** 工作区。 的 **[!UICONTROL 目录]** 屏幕显示了各种源，您可以使用这些源创建帐户和数据流。 每个源都显示与其关联的现有帐户和数据流的数量。

选择 **[!UICONTROL 帐户]** 访问 **[!UICONTROL 帐户]** 页面。

![catalog-accounts](../../images/tutorials/delete-accounts/catalog.png)

此时会显示现有帐户的列表。 本页列出了现有帐户的可排序信息，如源、用户名、关联的数据流和创建日期。 选择 **漏斗图标** 排序。

![数据流列表](../../images/tutorials/delete-accounts/accounts.png)

排序面板将显示在屏幕的左侧，其中包含可用源的列表。 您可以使用排序函数选择多个源。

选择要访问的源，并从主界面的帐户列表中找到要删除的帐户。 在示例中，所选的源为 **[!DNL Azure Blob Storage]** 帐户名称为 **[!UICONTROL blobTestConnector]**. 从排序面板中选择多个源时，最近创建的帐户将首先显示，因为列表按创建日期排序。

选择要删除的帐户。

![数据流排序](../../images/tutorials/delete-accounts/sort.png)

的 **[!UICONTROL 属性]** 面板显示在屏幕的右侧，其中包含有关所选帐户的信息。

选择省略号(`...`)。 此时会出现一个弹出面板，其中提供了 **[!UICONTROL 添加数据]**, **[!UICONTROL 编辑详细信息]**&#x200B;和 **[!UICONTROL 删除]**. 选择 **[!UICONTROL 删除]** 删除帐户。

![数据流排序](../../images/tutorials/delete-accounts/delete.png)

出现最终确认对话框，选择 **[!UICONTROL 删除]** 以完成该过程。

![删除](../../images/tutorials/delete-accounts/confirm.png)

## 后续步骤

通过阅读本教程，您已成功使用 **[!UICONTROL 源]** 工作区以删除现有帐户。

有关如何使用 [!DNL Flow Service] API，请参阅 [使用流量服务API删除连接](../../tutorials/api/delete.md)

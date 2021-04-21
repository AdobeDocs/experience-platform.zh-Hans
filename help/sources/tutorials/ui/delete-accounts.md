---
keywords: Experience Platform；主页；热门主题；删除帐户
description: Adobe Experience Platform中的源连接器提供按计划收集外部源数据的能力。 本教程提供了从“源”工作区删除帐户的步骤。
solution: Experience Platform
title: 在UI中删除源连接帐户
topic-legacy: overview
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# 删除源连接帐户

Adobe Experience Platform中的源连接器提供按计划收集外部源数据的能力。 本教程提供了从&#x200B;**[!UICONTROL Sources]**&#x200B;工作区中删除帐户的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   - [模式合成的基础](../../../xdm/schema/composition.md):了解XDM模式的基本构建基块，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL Real-time Customer Profile]](../../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。

## 使用UI删除帐户

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问&#x200B;**[!UICONTROL Sources]**&#x200B;工作区。 **[!UICONTROL Catalog]**&#x200B;屏幕显示了各种源，您可以为这些源创建帐户和数据流。 每个源显示与它们关联的现有帐户和数据流的数量。

选择&#x200B;**[!UICONTROL Accounts]**&#x200B;以访问&#x200B;**[!UICONTROL Accounts]**&#x200B;页面。

![catalog-accounts](../../images/tutorials/delete-accounts/catalog.png)

将显示现有帐户的列表。 在此页上是现有帐户的可排序信息列表，如源、用户名、关联数据流和创建日期。 选择左上角的&#x200B;**漏斗图标**&#x200B;进行排序。

![数据流 — 列表](../../images/tutorials/delete-accounts/accounts.png)

排序面板显示在屏幕左侧，包含可用源的列表。 您可以使用排序功能选择多个源。

选择要访问的源，并从主界面中的帐户列表中找到要删除的帐户。 在示例中，所选的源为&#x200B;**[!DNL Azure Blob Storage]**，帐户名为&#x200B;**[!UICONTROL blobTestConnector]**。 从“排序”面板中选择多个源时，最近创建的帐户将首先显示，因为列表按创建日期排序。

选择要删除的帐户。

![数据流排序](../../images/tutorials/delete-accounts/sort.png)

屏幕右侧将显示&#x200B;**[!UICONTROL Properties]**&#x200B;面板，其中包含有关选定帐户的信息。

选择要删除的帐户名称旁边的省略号(`...`)。 出现一个弹出面板，为&#x200B;**[!UICONTROL Add data]**、**[!UICONTROL Edit details]**&#x200B;和&#x200B;**[!UICONTROL Delete]**&#x200B;提供选项。 选择&#x200B;**[!UICONTROL Delete]**&#x200B;以删除帐户。

![数据流排序](../../images/tutorials/delete-accounts/delete.png)

随后将显示最终确认对话框，选择&#x200B;**[!UICONTROL Delete]**&#x200B;以完成该过程。

![删除](../../images/tutorials/delete-accounts/confirm.png)

## 后续步骤

通过本教程，您已成功使用&#x200B;**[!UICONTROL Sources]**&#x200B;工作区删除现有帐户。

有关如何使用[!DNL Flow Service] API以编程方式执行这些操作的步骤，请参阅有关使用流服务API](../../tutorials/api/delete.md)删除连接的教程[

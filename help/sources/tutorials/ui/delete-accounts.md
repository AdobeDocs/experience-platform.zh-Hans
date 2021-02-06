---
keywords: Experience Platform；主页；热门主题；删除帐户
description: Adobe Experience Platform的源连接器提供按计划接收外部源数据的能力。 本教程提供了从“源”工作区删除帐户的步骤。
solution: Experience Platform
title: 在UI中删除源连接帐户
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---


# 删除源连接帐户

Adobe Experience Platform的源连接器提供按计划接收外部源数据的能力。 本教程提供了从&#x200B;**[!UICONTROL Sources]**&#x200B;工作区中删除帐户的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   - [模式合成基础](../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL Real-time Customer Profile]](../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

## 使用UI删除帐户

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;**[!UICONTROL 源]**&#x200B;工作区。 **[!UICONTROL 目录]**&#x200B;屏幕显示各种源，您可以为其创建帐户和数据流。 每个源显示与它们关联的现有帐户和数据流的数量。

选择&#x200B;**[!UICONTROL 帐户]**&#x200B;以访问&#x200B;**[!UICONTROL 帐户]**&#x200B;页。

![catalog-accounts](../../images/tutorials/delete-accounts/catalog.png)

将显示一列表现有帐户。 此页上是现有帐户的可排序信息列表，如源、用户名、关联数据流和创建日期。 选择左上角的&#x200B;**漏斗图标**&#x200B;进行排序。

![dataflows-列表](../../images/tutorials/delete-accounts/accounts.png)

排序面板显示在屏幕的左侧，其中包含可用源的列表。 您可以使用排序功能选择多个源。

选择要访问的源，并从主界面中的帐户列表中找到要删除的帐户。 在示例中，所选的源为&#x200B;**[!DNL Azure Blob Storage]**，帐户名为&#x200B;**[!UICONTROL blobTestConnector]**。 从排序面板中选择多个源时，最近创建的帐户将首先显示，因为列表按创建日期排序。

选择要删除的帐户。

![dataflows sort](../../images/tutorials/delete-accounts/sort.png)

屏幕右侧将显示&#x200B;**[!UICONTROL 属性]**&#x200B;面板，其中包含有关选定帐户的信息。

选择要删除的帐户名称旁的省略号(`...`)。 出现一个弹出面板，其中提供了&#x200B;**[!UICONTROL 添加数据]**、**[!UICONTROL 编辑详细信息]**&#x200B;和&#x200B;**[!UICONTROL 删除]**&#x200B;的选项。 选择&#x200B;**[!UICONTROL 删除]**&#x200B;以删除帐户。

![dataflows sort](../../images/tutorials/delete-accounts/delete.png)

出现最终确认对话框，选择&#x200B;**[!UICONTROL 删除]**&#x200B;以完成该过程。

![删除](../../images/tutorials/delete-accounts/confirm.png)

## 后续步骤

通过遵循本教程，您已成功使用&#x200B;**[!UICONTROL 源]**&#x200B;工作区删除现有帐户。

有关如何使用[!DNL Flow Service] API以编程方式执行这些操作的步骤，请参阅有关使用流服务API](../../tutorials/api/delete.md)删除连接的教程。[
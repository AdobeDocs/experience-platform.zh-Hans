---
keywords: Experience Platform；主页；热门主题；Veeva CRM;Veeva
solution: Experience Platform
title: 在UI中创建Veeva CRM源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Veeva CRM源连接。
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: 076e0880c9efd1fe1cbfb4c610c5e15093adf460
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 1%

---

# 在UI中创建[!DNL Veeva CRM]源连接

Adobe Experience Platform中的源连接器提供了按计划摄取外部源CRM数据的功能。 本教程提供了使用[!DNL Platform]用户界面创建[!DNL Veeva CRM]源连接器的步骤。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):用于组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果您已经拥有有效的[!DNL Veeva CRM]帐户，则可以跳过本文档的其余部分，并继续阅读有关[配置数据流](../../dataflow/crm.md)的教程。

### 收集所需的凭据

| 凭据 | 描述 |
| ---------- | ----------- |
| `environmentUrl` | [!DNL Veeva CRM]源实例的URL。 |
| `username` | [!DNL Veeva CRM]用户帐户的用户名。 |
| `password` | [!DNL Veeva CRM]用户帐户的密码。 |
| `securityToken` | [!DNL Veeva CRM]用户帐户的安全令牌。 |

有关入门的更多信息，请参阅[此Veeva CRM文档]

## 连接[!DNL Veeva CRM]帐户

收集所需凭据后，可以按照以下步骤将[!DNL Veeva CRM]帐户关联到[!DNL Platform]。

在平台UI中，从左侧导航栏中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区。 [!UICONTROL Catalog]屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在[!UICONTROL CRM]类别下，选择&#x200B;**[!UICONTROL Veva CRM]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![目录](../../../../images/tutorials/create/veeva/catalog.png)

出现&#x200B;**[!UICONTROL 连接Veeva CRM帐户]**&#x200B;页面。 在此页面上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择要使用创建新数据流的[!DNL Veeva CRM]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/veeva/existing.png)

### 新帐户

如果要创建新帐户，请选择&#x200B;**[!UICONTROL 新建帐户]**，然后提供名称、可选描述和您的[!DNL Veeva CRM]凭据。 完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后允许一些时间建立新连接。

![新建](../../../../images/tutorials/create/veeva/new.png)

## 后续步骤

在本教程中，您已建立与[!DNL Veeva CRM]帐户的连接。 您现在可以继续阅读下一个教程，并[配置数据流以将数据导入Platform](../../dataflow/crm.md)。

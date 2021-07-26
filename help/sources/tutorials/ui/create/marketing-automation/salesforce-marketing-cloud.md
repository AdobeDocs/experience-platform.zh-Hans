---
keywords: Experience Platform；主页；热门主题；Salesforce Marketing Cloud;Salesforce Marketing Cloud
solution: Experience Platform
title: 在UI中创建SalesforceMarketing Cloud源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建SalesforceMarketing Cloud源连接。
source-git-commit: f196da32f67578ad1d73f3200f6050a7ddab0d88
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# 在UI中创建[!DNL Salesforce Marketing Cloud]源连接

>[!NOTE]
>
> [!DNL Salesforce Marketing Cloud]源位于测试版中。 有关使用测试版标记的源的详细信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

Adobe Experience Platform中的源连接器提供了按计划摄取外部源数据的功能。 本教程提供了使用Platform用户界面创建[!DNL Salesforce Marketing Cloud]源连接器的步骤。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):用于组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建块，包括模式组合中的关键原则和最佳实践。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一的实时客户资料。

如果已经具有[!DNL Salesforce Marketing Cloud]连接，则可以跳过本文档的其余部分，并继续阅读有关[配置数据流](../../dataflow/marketing-automation.md)的教程。

### 收集所需的凭据

要在Platform上访问您的[!DNL Salesforce Marketing Cloud]帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 应用程序的主机服务器。 这通常是您的子域。 |
| `clientId` | 与[!DNL Salesforce Marketing Cloud]应用程序关联的客户端ID。 |
| `clientSecret` | 与[!DNL Salesforce Marketing Cloud]应用程序关联的客户端密钥。 |

有关入门的更多信息，请参阅此[[!DNL Salesforce Marketing Cloud] 文档](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm)。

## 连接[!DNL Salesforce Marketing Cloud]帐户

收集所需凭据后，可以按照以下步骤将[!DNL Salesforce Marketing Cloud]帐户关联到Platform。

在平台UI中，从左侧导航中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区。 [!UICONTROL Catalog]屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 您还可以使用搜索栏缩小显示的连接器。

在[!UICONTROL 营销自动化]类别下，选择&#x200B;**[!UICONTROL SalesforceMarketing Cloud]**，然后选择&#x200B;**[!UICONTROL 设置]**。

![目录](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

出现&#x200B;**[!UICONTROL 连接到SalesforceMarketing Cloud]**&#x200B;页面。 在此页面上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用的是新凭据，请选择&#x200B;**[!UICONTROL 新帐户]**。 在显示的输入窗体中，提供名称、可选描述和您的[!DNL Salesforce Marketing Cloud]凭据。 完成后，选择&#x200B;**[!UICONTROL 连接]**，然后允许一些时间建立新连接。

![新建](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的[!DNL Salesforce Marketing Cloud]帐户，然后选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## 后续步骤

在本教程中，您已建立与[!DNL Salesforce Marketing Cloud]帐户的连接。 您现在可以继续阅读下一个教程并[配置数据流，以将营销自动化系统数据导入Platform](../../dataflow/marketing-automation.md)。

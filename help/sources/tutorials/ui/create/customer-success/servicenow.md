---
keywords: Experience Platform；主页；热门主题；ServiceNow；servicenow
solution: Experience Platform
title: 在UI中创建ServiceNow Source连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建ServiceNow源连接。
exl-id: 66c12f4d-8b0c-4bb2-910d-9e09fa364c94
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 2%

---

# 在用户界面中创建[!DNL ServiceNow]源连接

Adobe Experience Platform中的Source连接器提供了按计划摄取外部来源数据的功能。 本教程提供了使用[!DNL Experience Platform]用户界面创建[!DNL ServiceNow]源连接器的步骤。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有有效的[!DNL ServiceNow]连接，则可以跳过本文档的其余部分，并转到有关[配置数据流](../../dataflow/customer-success.md)的教程

### 收集所需的凭据

要在[!DNL Experience Platform]上访问您的[!DNL ServiceNow]帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `endpoint` | [!DNL ServiceNow]服务器的终结点。 |
| `username` | 用于连接到[!DNL ServiceNow]服务器进行身份验证的用户名。 |
| `password` | 用于连接到[!DNL ServiceNow]服务器以进行身份验证的密码。 |

有关入门的详细信息，请参阅[此 [!DNL ServiceNow] 文档](https://developer.servicenow.com/app.do#!/rest_api_doc？v=newyork&amp;id=r_TableAPI-GET)。

## 连接您的[!DNL ServiceNow]帐户

收集所需的凭据后，您可以按照以下步骤将您的[!DNL ServiceNow]帐户关联到[!DNL Experience Platform]。

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;**[!UICONTROL 源]**&#x200B;工作区。 **[!UICONTROL Catalog]**&#x200B;屏幕显示您可以为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在&#x200B;**[!UICONTROL 客户成功]**&#x200B;类别下，选择&#x200B;**[!UICONTROL ServiceNow]**。 如果这是您第一次使用此连接器，请选择&#x200B;**[!UICONTROL 配置]**。 否则，请选择&#x200B;**[!UICONTROL 连接源]**&#x200B;以创建新的[!DNL ServiceNow]连接器。

![](../../../../images/tutorials/create/servicenow/catalog.png)

出现&#x200B;**[!UICONTROL 连接到ServiceNow]**&#x200B;页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您正在使用新凭据，请选择&#x200B;**[!UICONTROL 新帐户]**。 在显示的输入表单上，提供名称、可选描述和您的[!DNL ServiceNow]凭据。 完成后，选择&#x200B;**[!UICONTROL 连接]**，然后留出一些时间来建立新连接。

![](../../../../images/tutorials/create/servicenow/new.png)

### 现有账户

若要连接现有帐户，请选择您要连接的[!DNL ServiceNow]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![](../../../../images/tutorials/create/servicenow/existing.png)

## 后续步骤

通过学习本教程，您已建立与[!DNL ServiceNow]帐户的连接。 您现在可以继续下一教程，并[配置数据流以将数据导入 [!DNL Experience Platform]](../../dataflow/customer-success.md)。

---
title: 通过UI将您的Salesforce Marketing Cloud帐户连接到Experience Platform
description: 了解如何通过UI将您的Salesforce Marketing Cloud帐户连接到Experience Platform。
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 7ff0709b62590bb80c1ed664368f28cdc4a950ea
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 2%

---

# 通过UI将您的[!DNL Salesforce Marketing Cloud]帐户连接到Experience Platform

>[!WARNING]
>
>[!DNL Salesforce Marketing Cloud]源将于2026年1月被弃用。 作为替代方案，将在今年晚些时候发布新的信息源。 发布新源后，您必须计划在2026年1月底之前通过创建新帐户连接和数据流迁移到新源。

本教程提供了有关如何通过UI将您的[!DNL Salesforce Marketing Cloud]帐户连接到Adobe Experience Platform的步骤。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： [!DNL Experience Platform]用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有[!DNL Salesforce Marketing Cloud]帐户，则可以跳过本文档的其余部分，并继续学习关于使用UI](../../dataflow/marketing-automation.md)将营销自动化数据引入Experience Platform的[教程。

### 收集所需的凭据

要在Experience Platform上访问您的[!DNL Salesforce Marketing Cloud]帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| Host | 应用程序的主机服务器。 这通常是您的子域。 **注意：**&#x200B;在输入`host`值时，需要指定`{subdomain}.rest.marketingcloudapis.com`。 例如，如果您的主机URL是`https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`，则必须输入`acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/`作为主机值。 |
| 客户端 ID | 与您的[!DNL Salesforce Marketing Cloud]应用程序关联的客户端ID。 |
| 客户端密码 | 与您的[!DNL Salesforce Marketing Cloud]应用程序关联的客户端密钥。 |

有关[!DNL Salesforce Marketing Cloud]的身份验证的详细信息，请访问[[!DNL Salesforce] 身份验证文档](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm)。

## 连接您的[!DNL Salesforce Marketing Cloud]帐户

>[!IMPORTANT]
>
>[!DNL Salesforce Marketing Cloud]源集成当前不支持自定义对象摄取。

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL 目录]显示Experience Platform支持的各种源。

您可以从类别列表中选择相应的类别。 您还可以使用搜索栏筛选特定源。

在[!UICONTROL 营销自动化]类别下，选择&#x200B;**[!UICONTROL Salesforce Marketing Cloud]**，然后选择&#x200B;**[!UICONTROL 设置]**。

![已选择Salesforce Marketing Cloud源的源目录。](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

此时会显示&#x200B;**[!UICONTROL 连接到Salesforce Marketing Cloud]**&#x200B;页面。 在此页上，您可以创建新帐户或使用现有帐户。

### 新帐户

要创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，并提供帐户的名称、可选描述以及与您的[!DNL Salesforce Marketing Cloud]帐户对应的身份验证凭据。

完成后，选择&#x200B;**[!UICONTROL 连接到源]**，然后留出一些时间来建立新连接。

![新帐户界面，您可以在其中验证Salesforce Marketing Cloud的新帐户。](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### 现有账户

如果您已经拥有现有帐户，请选择&#x200B;**[!UICONTROL 现有帐户]**，然后从显示的列表中选择您要使用的帐户。

![可以从现有Salesforce Marketing Cloud帐户列表中选择的现有帐户界面。](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## 后续步骤

通过学习本教程，您已在[!DNL Salesforce Marketing Cloud]帐户与Experience Platform之间建立连接。 您现在可以继续下一教程并[创建数据流以将您的营销自动化数据导入Experience Platform](../../dataflow/marketing-automation.md)。

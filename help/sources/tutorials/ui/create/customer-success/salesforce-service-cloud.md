---
title: 使用Salesforce用户界面连接您的Experience Platform服务云帐户
description: 了解如何使用用户界面连接您的Salesforce Service Cloud帐户并将客户成功数据引入Experience Platform。
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: eab6303a3b420d4622185316922d242a4ce8a12d
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 2%

---

# 使用UI将您的[!DNL Salesforce Service Cloud]帐户连接到Experience Platform

本教程提供了有关如何使用Experience Platform用户界面连接[!DNL Salesforce Service Cloud]帐户并将客户成功数据引入Adobe Experience Platform的步骤。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)： Experience Platform用于组织客户体验数据的标准化框架。
   * [架构组合的基础知识](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建块，包括架构组合中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个源的汇总数据，提供统一的实时使用者个人资料。

如果您已经拥有有效的[!DNL Salesforce Service Cloud]连接，则可以跳过本文档的其余部分，并转到有关[配置数据流以实现客户成功](../../dataflow/customer-success.md)的教程

### 收集所需的凭据

>[!WARNING]
>
>[!DNL Salesforce Service Cloud]源的基本身份验证将于2026年1月被弃用。 您必须移至OAuth 2客户端凭据身份验证，才能继续使用该源并将数据从[!DNL Salesforce Service Cloud]帐户摄取到Experience Platform。

[!DNL Salesforce Service Cloud]源支持基本身份验证和OAuth2客户端凭据。

>[!BEGINTABS]

>[!TAB 基本身份验证]

你必须为以下凭据提供值，才能使用基本身份验证连接[!DNL Salesforce Service Cloud]帐户。

| 凭据 | 描述 |
| --- | --- |
| 环境 URL | [!DNL Salesforce Service Cloud]源实例的URL。 |
| 用户名 | [!DNL Salesforce Service Cloud]用户帐户的用户名。 |
| 密码 | [!DNL Salesforce Service Cloud]用户帐户的密码。 |
| 安全令牌 | [!DNL Salesforce Service Cloud]用户帐户的安全令牌。 |
| API版本 | （可选）您正在使用的[!DNL Salesforce Service Cloud]实例的REST API版本。 API版本的值必须使用小数格式设置。 例如，如果您使用的是API版本`52`，则必须以`52.0`的形式输入值。 如果此字段留空，Experience Platform将自动使用最新可用版本。 |

有关身份验证的详细信息，请参阅[此 [!DNL Salesforce Service Cloud] 身份验证指南](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm)。

>[!TAB OAuth2客户端凭据]

您必须为以下凭据提供值，才能使用OAuth2客户端凭据连接您的[!DNL Salesforce Service Cloud]帐户。

| 凭据 | 描述 |
| --- | --- |
| 环境 URL | [!DNL Salesforce Service Cloud]源实例的URL。 |
| 客户端 ID | 在OAuth2身份验证中，客户端ID与客户端密钥结合使用。 客户端ID和客户端密钥共同使您的应用程序能够代表您的帐户运行，方法是向[!DNL Salesforce Service Cloud]标识您的应用程序。 |
| 客户端密码 | 客户端密钥与客户端ID结合使用，作为OAuth2身份验证的一部分。 客户端ID和客户端密钥共同使您的应用程序能够代表您的帐户运行，方法是向[!DNL Salesforce Service Cloud]标识您的应用程序。 |
| API版本 | 您正在使用的[!DNL Salesforce Service Cloud]实例的REST API版本。 API版本的值必须使用小数格式设置。 例如，如果您使用的是API版本`52`，则必须以`52.0`的形式输入值。 如果此字段留空，Experience Platform将自动使用最新可用版本。 |

有关为[!DNL Salesforce Service Cloud]使用OAuth的更多信息，请阅读有关OAuth授权流程[&#128279;](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5)的[!DNL Salesforce Service Cloud] 指南。

>[!ENDTABS]

收集所需的凭据后，您可以按照以下步骤将您的[!DNL Salesforce Service Cloud]帐户连接到Experience Platform。

## 连接您的[!DNL Salesforce Service Cloud]帐户

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在&#x200B;*[!UICONTROL 客户成功]*&#x200B;类别下选择&#x200B;**[!DNL Salesforce Service Cloud]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

>[!TIP]
>
>当给定的源尚未具有经过身份验证的帐户时，源目录中的源会显示&#x200B;**[!UICONTROL 设置]**&#x200B;选项。 一旦存在经过身份验证的帐户，此选项将更改为&#x200B;**[!UICONTROL 添加数据]**。

![已选择Experience Platform Service Cloud源卡的Salesforce UI上的源目录。](../../../../images/tutorials/create/salesforce-service-cloud/catalog.png)

此时会显示&#x200B;**[!UICONTROL 连接到Salesforce Service Cloud]**&#x200B;页面。 在此页上，您可以使用新凭据或现有凭据。

### 使用现有帐户

若要使用现有帐户，请选择&#x200B;**[!UICONTROL 现有帐户]**，然后从显示的列表中选择所需的帐户。 完成后，选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![您的组织中已存在的经过身份验证的Salesforce Service Cloud帐户的列表。](../../../../images/tutorials/create/salesforce-service-cloud/existing.png)

### 创建新帐户

要创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，并为您的新[!DNL Salesforce Service Cloud]帐户提供名称和描述。

![通过提供适当的身份验证凭据来创建新的Salesforce Service Cloud帐户的界面。](../../../../images/tutorials/create/salesforce-service-cloud/new.png)

接下来，选择要用于新帐户的身份验证类型。

>[!BEGINTABS]

>[!TAB 基本身份验证]

对于基本身份验证，请选择&#x200B;**[!UICONTROL 基本身份验证]**，然后提供以下凭据的值：

* 环境 URL
* 用户名
* 密码
* API版本（可选）

完成后，选择&#x200B;**[!UICONTROL 连接到源]**。

![用于创建Salesforce帐户的基本身份验证界面。](../../../../images/tutorials/create/salesforce-service-cloud/basic.png)

>[!TAB OAuth2客户端凭据]

对于OAuth 2客户端凭据，选择&#x200B;**[!UICONTROL OAuth2客户端凭据]**，然后提供以下凭据的值：

* 环境 URL
* 客户端 ID
* 客户端密码
* API版本

完成后，选择&#x200B;**[!UICONTROL 连接到源]**。

![用于创建Salesforce帐户的OAuth接口。](../../../../images/tutorials/create/salesforce-service-cloud/oauth2.png)

>[!ENDTABS]

## 后续步骤

通过学习本教程，您已建立与[!DNL Salesforce Service Cloud]帐户的连接。 您现在可以继续下一教程，并[配置数据流以将客户成功数据引入Experience Platform](../../dataflow/customer-success.md)。

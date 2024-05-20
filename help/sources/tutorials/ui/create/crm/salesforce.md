---
title: 使用Experience Platform用户界面连接Salesforce帐户
description: 了解如何使用用户界面连接您的Salesforce帐户并将您的CRM数据引入Experience Platform。
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: 8d62cf4ca0071e84baa9399e0a25f7ebfb096c1a
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 1%

---

# 连接您的 [!DNL Salesforce] 要使用UIExperience Platform的帐户

本教程提供了有关如何连接 [!DNL Salesforce] ，并使用Experience Platform用户界面将您的CRM数据引入Adobe Experience Platform。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：Experience Platform用于组织客户体验数据的标准化框架。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有经过身份验证的 [!DNL Salesforce] 帐户，您可以跳过本文档的其余部分，并继续阅读上的教程 [为CRM数据配置工作流](../../dataflow/crm.md).

### 收集所需的凭据 {#gather-required-credentials}

此 [!DNL Salesforce] 源支持基本身份验证和OAuth2客户端凭据。

>[!BEGINTABS]

>[!TAB 基本身份验证]

必须提供以下凭据的值才能连接 [!DNL Salesforce] 使用基本身份验证的帐户。

| 凭据 | 描述 |
| --- | --- |
| 环境URL | 的URL [!DNL Salesforce] 源实例。 |
| 用户名 | 的用户名 [!DNL Salesforce] 用户帐户。 |
| 密码 | 的密码 [!DNL Salesforce] 用户帐户。 |
| 安全令牌 | 的安全令牌 [!DNL Salesforce] 用户帐户。 |
| API版本 | （可选） REST API版本的 [!DNL Salesforce] 您正在使用的实例。 API版本的值必须使用小数格式设置。 例如，如果您使用的是API版本 `52`，则必须输入值，如下所示 `52.0`. 如果此字段留空，则Experience Platform将自动使用最新可用版本。 |

有关身份验证的详细信息，请参阅 [此 [!DNL Salesforce] 身份验证指南](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB OAuth2客户端凭据]

必须提供以下凭据的值才能连接 [!DNL Salesforce] 使用OAuth2客户端凭据的帐户。

| 凭据 | 描述 |
| --- | --- |
| 环境URL | 的URL [!DNL Salesforce] 源实例。 |
| 客户端ID | 在OAuth2身份验证中，客户端ID与客户端密钥结合使用。 客户端ID和客户端密钥共同允许您的应用程序代表您的帐户运行，方法是将您的应用程序标识到 [!DNL Salesforce]. |
| 客户端密码 | 客户端密钥与客户端ID结合使用，作为OAuth2身份验证的一部分。 客户端ID和客户端密钥共同允许您的应用程序代表您的帐户运行，方法是将您的应用程序标识到 [!DNL Salesforce]. |
| API版本 | 的REST API版本 [!DNL Salesforce] 您正在使用的实例。 API版本的值必须使用小数格式设置。 例如，如果您使用的是API版本 `52`，则必须输入值，如下所示 `52.0`. 如果此字段留空，则Experience Platform将自动使用最新可用版本。 |

有关将OAuth用于 [!DNL Salesforce]，阅读 [[!DNL Salesforce] OAuth授权流指南](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

收集所需的凭据后，您可以按照以下步骤连接您的 [!DNL Salesforce] 帐户到Experience Platform。

## 连接您的 [!DNL Salesforce] 帐户

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在 *CRM* 类别，选择 **[!DNL Salesforce]**，然后选择 **[!UICONTROL 添加数据]**.

>[!TIP]
>
>源目录中的源显示 **[!UICONTROL 设置]** 选项。 经过身份验证的帐户存在后，此选项将更改为 **[!UICONTROL 添加数据]**.

![选择了Salesforce源卡的Experience PlatformUI上的源目录。](../../../../images/tutorials/create/salesforce/catalog.png)

此 **[!UICONTROL 连接到Salesforce]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 使用现有帐户

要使用现有帐户，请选择 **[!UICONTROL 现有帐户]** 然后从显示的列表中选择要使用的帐户。 完成后，选择 **[!UICONTROL 下一个]** 以继续。

![组织中已存在的经过身份验证的Salesforce帐户的列表。](../../../../images/tutorials/create/salesforce/existing.png)

### 创建新帐户

要创建新帐户，请选择 **[!UICONTROL 新帐户]** 并提供新项目的名称和描述 [!DNL Salesforce] 帐户。

![在界面中，通过提供适当的身份验证凭据来创建新的Salesforce帐户。](../../../../images/tutorials/create/salesforce/new.png)

接下来，选择要用于新帐户的身份验证类型。

>[!BEGINTABS]

>[!TAB 基本身份验证]

对于基本身份验证，选择 **[!UICONTROL 基本身份验证]** 然后提供以下凭证的值：

* 环境URL
* 用户名
* 密码
* API版本（可选）

完成后，选择 **[!UICONTROL 连接到源]**.

![创建Salesforce帐户的基本身份验证界面。](../../../../images/tutorials/create/salesforce/basic.png)

>[!TAB OAuth2客户端凭据]

对于OAuth 2客户端凭据，选择 **[!UICONTROL OAuth2客户端凭据]** 然后提供以下凭证的值：

* 环境URL
* 客户端ID
* 客户端密码
* API版本

完成后，选择 **[!UICONTROL 连接到源]**.

![用于创建Salesforce帐户的OAuth接口。](../../../../images/tutorials/create/salesforce/oauth2.png)

>[!ENDTABS]

## 后续步骤

通过学习本教程，您已建立与的连接 [!DNL Salesforce] 帐户。 您现在可以继续下一教程和 [配置数据流以将数据引入 [!DNL Platform]](../../dataflow/crm.md).

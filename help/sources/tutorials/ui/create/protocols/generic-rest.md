---
keywords: Experience Platform；主页；热门主题；通用REST API
title: 在UI中创建通用REST API Source连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建通用REST API源连接。
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 3%

---

# 在用户界面中创建[!DNL Generic REST API]源连接

>[!NOTE]
>
> [!DNL Generic REST API]源为测试版。 有关使用带有Beta标记的连接器的更多信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

本教程提供了使用Adobe Experience Platform用户界面创建[!DNL Generic REST API]源连接器的步骤。

## 快速入门

本教程需要对以下Experience Platform组件有一定的了解：

* [源](../../../../home.md)： Experience Platform允许从各种源摄取数据，同时让您能够使用Experience Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)： Experience Platform提供了将单个Experience Platform实例划分为多个单独的虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

### 收集所需的凭据

要在Experience Platform上访问您的[!DNL Generic REST API]帐户，您必须为您选择的身份验证类型提供有效凭据。 通用REST API支持OAuth 2刷新代码和基本身份验证。 有关两种受支持的身份验证类型的凭据的信息，请参见下表。

#### OAuth 2刷新代码

| 凭据 | 描述 |
| --- | --- |
| Host | 您向其发出请求的源的主机URL。 此值为必填，无法使用请求参数覆盖来绕过。 |
| 授权测试URL | （可选）创建基本连接时，授权测试URL用于验证凭据。 如果未提供，则会在源连接创建步骤中自动检查凭据。 |
| 客户端 ID | （可选）与您的用户帐户关联的客户端ID。 |
| 客户端密码 | （可选）与您的用户帐户关联的客户端密钥。 |
| 访问令牌 | 用于访问应用程序的主要身份验证凭据。 访问令牌表示应用程序的授权，用于访问用户数据的特定方面。 此值为必填，无法使用请求参数覆盖来绕过。 |
| 刷新令牌 | （可选）当访问令牌过期时，用于生成新访问令牌的令牌。 |
| 访问令牌URL | （可选）用于获取访问令牌的URL端点。 |
| 请求参数覆盖 | （可选）一个属性，它允许您指定要覆盖的凭据参数。 |


#### 基本身份验证

| 凭据 | 描述 |
| --- | --- |
| Host | 您向其发出请求的源的主机URL。 |
| 用户名 | 与您的用户帐户对应的用户名。 |
| 密码 | 与您的用户帐户对应的密码。 |

## 连接您的通用REST API帐户

在Experience Platform UI中，从左侧导航中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问[!UICONTROL 源]工作区。 [!UICONTROL Catalog]屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索栏查找要使用的特定源。

在[!UICONTROL 协议]类别下，选择&#x200B;**[!UICONTROL 通用REST API]**，然后选择&#x200B;**[!UICONTROL 添加数据]**。

![目录](../../../../images/tutorials/create/generic-rest/catalog.png)

此时会显示&#x200B;**[!UICONTROL 连接到通用REST API]**&#x200B;页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有账户

要连接现有帐户，请选择您要连接的通用REST API帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/generic-rest/existing.png)

### 新帐户

如果您正在创建新帐户，请选择&#x200B;**[!UICONTROL 新帐户]**，然后为您的新[!DNL Generic REST API]帐户提供名称和选项说明。

![新](../../../../images/tutorials/create/generic-rest/new.png)

#### 使用OAuth 2刷新代码进行身份验证

[!DNL Generic REST API]支持OAuth 2刷新代码和基本身份验证。 要使用OAuth2身份验证进行身份验证，请选择&#x200B;**[!UICONTROL OAuth2RefreshCode]**，提供您的OAuth 2凭据，然后选择&#x200B;**[!UICONTROL 连接到源]**。

![](../../../../images/tutorials/create/generic-rest/oauth2.png)

#### 使用基本身份验证进行身份验证

若要使用基本身份验证，请选择&#x200B;**[!UICONTROL 基本身份验证]**，提供主机、用户名和密码，然后选择&#x200B;**[!UICONTROL 连接到源]**。

![](../../../../images/tutorials/create/generic-rest/basic-authentication.png)

## 后续步骤

通过学习本教程，您已建立与通用REST API帐户的连接。 您现在可以继续下一教程，并[配置数据流以将数据导入Experience Platform](../../dataflow/protocols.md)。

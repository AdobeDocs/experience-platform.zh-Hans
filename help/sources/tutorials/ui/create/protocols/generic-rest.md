---
keywords: Experience Platform；主页；热门主题；通用REST API
title: 在UI中创建通用REST API源连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建通用REST API源连接。
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 1%

---

# 创建 [!DNL Generic REST API] UI中的源连接

>[!NOTE]
>
> 此 [!DNL Generic REST API] 源为测试版。 请参阅 [源概述](../../../../home.md#terms-and-conditions) 有关使用Beta标记的连接器的更多信息。

本教程提供了用于创建 [!DNL Generic REST API] 源连接器，使用Adobe Experience Platform用户界面。

## 快速入门

本教程需要深入了解Platform的以下组件：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

### 收集所需的凭据

要访问您的 [!DNL Generic REST API] 帐户，则必须为您选择的身份验证类型提供有效的凭据。 通用REST API支持OAuth 2刷新代码和基本身份验证。 有关两种受支持的身份验证类型的凭据的信息，请参阅下表。

#### OAuth 2刷新代码

| 凭据 | 描述 |
| --- | --- |
| Host | 您向其发出请求的源的主机URL。 此值为必需，不能使用请求参数覆盖进行绕过。 |
| 授权测试URL | （可选）授权测试URL用于在创建基本连接时验证凭据。 如果未提供，则在源连接创建步骤期间将自动检查凭据。 |
| 客户端ID | （可选）与您的用户帐户关联的客户端ID。 |
| 客户端密码 | （可选）与您的用户帐户关联的客户端密钥。 |
| 访问令牌 | 用于访问应用程序的主要身份验证凭据。 访问令牌表示应用程序对访问用户数据特定方面的授权。 此值为必需，不能使用请求参数覆盖进行绕过。 |
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

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示您可以用来创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索栏查找要使用的特定源。

在 [!UICONTROL 协议] 类别，选择 **[!UICONTROL 通用REST API]** 然后选择 **[!UICONTROL 添加数据]**.

![目录](../../../../images/tutorials/create/generic-rest/catalog.png)

此 **[!UICONTROL 连接到通用REST API]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要连接现有帐户，请选择要连接的Generic REST API帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/generic-rest/existing.png)

### 新帐户

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后为您的新页面提供名称和选项描述 [!DNL Generic REST API] 帐户。

![新](../../../../images/tutorials/create/generic-rest/new.png)

#### 使用OAuth 2刷新代码进行身份验证

[!DNL Generic REST API] 支持OAuth 2刷新代码和基本身份验证。 要使用OAuth2身份验证进行身份验证，请选择 **[!UICONTROL OAuth2RefreshCode]**，提供您的OAuth 2凭据，然后选择 **[!UICONTROL 连接到源]**.

![](../../../../images/tutorials/create/generic-rest/oauth2.png)

#### 使用基本身份验证进行身份验证

要使用基本身份验证，请选择 **[!UICONTROL 基本身份验证]**，提供主机、用户名和密码，然后选择 **[!UICONTROL 连接到源]**.

![](../../../../images/tutorials/create/generic-rest/basic-authentication.png)

## 后续步骤

通过学习本教程，您已建立与通用REST API帐户的连接。 您现在可以继续下一教程和 [配置数据流以将数据引入平台](../../dataflow/protocols.md).

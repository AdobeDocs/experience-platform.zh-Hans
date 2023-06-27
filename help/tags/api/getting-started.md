---
title: 身份验证和访问Reactor API
description: 了解如何开始使用Reactor API，包括生成所需访问凭据的步骤。
exl-id: fc1acc1d-6cfb-43c1-9ba9-00b2730cad5a
source-git-commit: 2c8ac35e9bf72c91743714da1591c3414db5c5e9
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 0%

---

# 身份验证和访问Reactor API

要使用 [Reactor API](https://developer.adobe.com/experience-platform-apis/references/reactor/) 要创建和管理Tags扩展，每个请求必须包含以下身份验证标头：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

本指南介绍如何使用Adobe Developer控制台收集每个标头的值，以便您开始调用Reactor API。

## 获取开发人员对Adobe Experience Platform的访问权限 {#gain-developer-access}

在为Reactor API生成身份验证值之前，您必须具有开发人员访问权限才能进行Experience Platform。 要获得开发人员访问权限，请按照 [Experience Platform身份验证教程](/help/landing/api-authentication.md). 一旦您完成 [获得用户访问权限](/help/landing/api-authentication.md#gain-user-access) 步骤，返回本教程以生成特定于Reactor API的凭据。

## 生成访问凭据 {#generate-access-credentials}

使用Adobe Developer Console，您必须生成以下三个访问凭据：

* `{ORG_ID}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

您组织的ID (`{ORG_ID}`)和API密钥(`{API_KEY}`)可在最初生成API调用后，在以后的API调用中重复使用。 但是，您的访问令牌(`{ACCESS_TOKEN}`)是临时的，必须每24小时重新生成一次。

下面详细介绍了生成这些值的步骤。

### 一次性设置 {#one-time-setup}

转到 [Adobe Developer控制台](https://www.adobe.com/go/devs_console_ui) 然后使用您的Adobe ID登录。 接下来，按照教程中概述的以下步骤进行操作： [创建空项目](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) 在开发人员控制台文档中。

创建项目后，选择 **添加API** 在 **项目概述** 屏幕。

![](../images/api/getting-started/add-api-button.png)

此 **添加API** 屏幕。 选择 **EXPERIENCE PLATFORM LAUNCHAPI** 从可用API列表中，然后选择 **下一个**.

![](../images/api/getting-started/add-launch-api.png)

接下来，选择身份验证类型以生成访问令牌并访问Experience PlatformAPI。

>[!IMPORTANT]
>
>选择 **[!UICONTROL OAuth服务器到服务器]** 方法，因为这将是向前移动时支持的唯一方法。 此 **[!UICONTROL 服务帐户(JWT)]** 方法已弃用。 虽然使用JWT身份验证方法的集成将继续工作到2025年1月1日，但Adobe强烈建议您在该日期之前将现有集成迁移到新的OAuth服务器到服务器方法。 在部分获取更多信息 [!BADGE 已弃用]{type=negative}[生成JSON Web令牌(JWT)](/help/landing/api-authentication.md#jwt) 在平台API身份验证教程中。

选择&#x200B;**下一步**&#x200B;以继续。

![选择OAuth服务器到服务器身份验证方法。](/help/tags/images/api/getting-started/oauth-authentication-method.png)

下一个屏幕提示您选择要与API集成关联的一个或多个产品配置文件。

>[!NOTE]
>
产品配置文件由您的组织通过Adobe Admin Console进行管理，并包含用于精细功能的特定权限集。 产品配置文件及其权限只能由组织内拥有管理员权限的用户管理。 如果您不确定要为API选择哪些产品配置文件，请联系您的管理员。

从列表中选择所需的产品配置文件，然后选择 **保存配置的API** 以完成API注册。

![](../images/api/getting-started/select-product-profile.png)

### 收集凭据 {#gather-credentials}

将API添加到项目后， **[!UICONTROL EXPERIENCE PLATFORMAPI]** 项目页面显示所有Experience PlatformAPI调用所需的以下凭据：

* `{API_KEY}` ([!UICONTROL 客户端ID])
* `{ORG_ID}` ([!UICONTROL 组织 ID])

![在开发人员控制台中添加API后的集成信息。](/help/tags/images/api/getting-started/api-integration-information.png)

### 生成访问令牌 {#generate-access-token}

下一步是生成 `{ACCESS_TOKEN}` 用于平台API调用的凭据。 与的值不同 `{API_KEY}` 和 `{ORG_ID}`，必须每24小时生成一个新令牌才能继续使用平台API。

>[!TIP]
>
这些令牌会在24小时后过期。 如果您将此集成用于应用程序，最好以编程方式从应用程序中获取持有者令牌。

根据您的用例，您有两个选项可生成访问令牌：

* [手动生成令牌](#manual)
* [自动生成令牌](#auto-token)

#### 手动生成访问令牌 {#manual}

要手动生成新的 `{ACCESS_TOKEN}`，导航到 **[!UICONTROL 凭据]** > **[!UICONTROL OAuth服务器到服务器]** 并选择 **[!UICONTROL 生成访问令牌]**，如下所示。

![在开发人员控制台UI中如何生成和访问令牌的屏幕录制。](/help/tags/images/api/getting-started/generate-access-token.gif)

将生成新的访问令牌，并提供用于将令牌复制到剪贴板的按钮。 此值用于所需的Authorization标头，必须以格式提供 `Bearer {ACCESS_TOKEN}`.

#### 自动生成令牌 {#auto-token}

您还可以使用Postman环境和集合来生成访问令牌。 有关更多信息，请阅读关于 [使用Postman验证和测试API调用](/help/landing/api-authentication.md#use-postman) 在Experience PlatformAPI身份验证指南中。

## 测试API凭据 {#test-api-credentials}

按照本教程中的步骤操作，您应该具有以下有效值： `{ORG_ID}`， `{API_KEY}`、和 `{ACCESS_TOKEN}`. 您现在可以通过在对Reactor API的简单cURL请求中使用这些值来测试这些值。

首先尝试对进行API调用 [列出所有公司](./endpoints/companies.md#list).

>[!NOTE]
>
您的组织中可能没有任何公司，在这种情况下，响应将为HTTP状态404 （未找到）。 只要您未收到403（禁止）错误，您的访问凭据即有效且有效。

确认访问凭据有效后，继续浏览其他API参考文档，了解API的多种功能。

## 正在读取示例API调用 {#read-sample-api-calls}

每个端点指南都提供了示例API调用，以演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../landing/api-guide.md#sample-api) 《平台API快速入门指南》中的。

## 后续步骤 {#next-steps}

现在您了解了要使用哪些标头，就可以开始调用Reactor API了。 选择一个端点指南以开始：

* [Reactor API参考文档](https://developer.adobe.com/experience-platform-apis/references/reactor/)
* [Reactor API指南概述](/help/tags/api/overview.md)

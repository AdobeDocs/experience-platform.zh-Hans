---
solution: Experience Platform
title: 身份验证和访问Experience PlatformAPI
type: Tutorial
description: 此文档分步说明了如何获取 Adobe Experience Platform 开发人员帐户访问权限以调用 Experience Platform API。
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: f598c6dabe9296044055d8e961cf5177a655f5fa
workflow-type: tm+mt
source-wordcount: '2205'
ht-degree: 7%

---


# 验证和访问 Experience Platform API

此文档分步说明了如何获取 Adobe Experience Platform 开发人员帐户访问权限以调用 Experience Platform API。在本教程结束时，您将生成或收集了所有平台API调用中作为标头所需的以下凭据：

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{ORG_ID}`

>[!TIP]
>
>除了上述三个凭据之外，许多Platform API还需要有效的 `{SANDBOX_NAME}` 将作为标头提供。 请参阅 [沙盒概述](../sandboxes/home.md) 有关沙盒和 [沙盒管理端点](/help/sandboxes/api/sandboxes.md#list) 文档，了解有关列出您的组织可用的沙盒的信息。

为了维护应用程序和用户的安全，所有对Experience PlatformAPI的请求都必须使用OAuth等标准进行身份验证和授权。

本教程介绍如何收集验证Platform API调用所需的凭据，如下面的流程图中所述。 您可以在初始一次性设置中收集大多数所需的凭据。 但是，必须每24小时刷新一次访问令牌。

![](./images/api-authentication/authentication-flowchart.png)

## 先决条件 {#prerequisites}

要成功调用Experience PlatformAPI，您必须具备以下条件：

* 有权访问Adobe Experience Platform的组织。
* 能够将您添加为产品配置文件的开发人员和用户的Admin Console管理员。
* Experience Platform系统管理员，可为您授予必要的基于属性的访问控制，以通过API对Experience Platform的各个部分执行读取或写入操作。

您还必须拥有Adobe ID才能完成本教程。 如果您没有Adobe ID，则可以使用以下步骤创建一个：

1. 转到 [Adobe Developer控制台](https://console.adobe.io).
2. 选择 **[!UICONTROL 创建新帐户]**.
3. 完成注册过程。

## 获得Experience Platform的开发人员和用户访问权限 {#gain-developer-user-access}

在Adobe Developer控制台上创建集成之前，您的帐户必须具有Adobe Admin Console中Experience Platform产品配置文件的开发人员和用户权限。

### 获取开发人员访问权限 {#gain-developer-access}

联系 [!DNL Admin Console] 管理员将您作为开发人员添加到Experience Platform产品配置文件中 [[!DNL Admin Console]](https://adminconsole.adobe.com/). 请参阅 [!DNL Admin Console] 文档，以了解关于如何 [管理产品配置文件的开发人员访问权限](https://helpx.adobe.com/cn/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).

一旦您被分配为开发人员，您就可以开始在中创建集成 [Adobe Developer控制台](https://www.adobe.com/go/devs_console_ui). 这些集成是从外部应用程序和服务到AdobeAPI的管道。

### 获得用户访问权限 {#gain-user-access}

您的 [!DNL Admin Console] 管理员还必须将您作为用户添加到同一产品配置文件。 凭借用户访问权限，您可以在UI中查看您执行的API操作的结果。

请参阅指南，网址为 [在中管理用户组 [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) 以了解更多信息。

## 生成API密钥（客户端ID）和组织ID {#generate-credentials}

>[!NOTE]
>
>如果您正在从 [Privacy ServiceAPI指南](../privacy-service/api/getting-started.md)，您现在可以返回该指南以生成对唯一的访问凭据 [!DNL Privacy Service].

在您通过获得对Platform的开发人员和用户访问权限后 [!DNL Admin Console]，下一步是生成 `{ORG_ID}` 和 `{API_KEY}` Adobe Developer控制台中的凭据。 这些凭据只需生成一次，可在以后的Platform API调用中重复使用。

### 将Experience Platform添加到项目 {#add-platform-to-project}

转到 [Adobe Developer控制台](https://www.adobe.com/go/devs_console_ui) 然后使用您的Adobe ID登录。 接下来，按照教程中概述的以下步骤进行操作： [创建空项目](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) 在Adobe Developer Console文档中。

创建新项目后，选择 **[!UICONTROL 添加API]** 在 **[!UICONTROL 项目概述]** 屏幕。

>[!TIP]
>
>如果您配置了多个组织，请使用界面右上角的组织选择器，以确保您在所需的组织中。

![高亮显示了“添加API”选项的开发人员控制台屏幕。](./images/api-authentication/add-api.png)

此 **[!UICONTROL 添加API]** 屏幕。 选择Adobe Experience Platform的产品图标，然后选择 **[!UICONTROL EXPERIENCE PLATFORMAPI]** 选择之前 **[!UICONTROL 下一个]**.

![选择Experience PlatformAPI。](./images/api-authentication/platform-api.png)

>[!TIP]
>
>选择 **[!UICONTROL 查看文档]** 在单独的浏览器窗口中导航以完成 [Experience PlatformAPI参考文档](https://developer.adobe.com/experience-platform-apis/).

### 选择OAuth服务器到服务器身份验证类型 {#select-oauth-server-to-server}

接下来，选择身份验证类型以生成访问令牌并访问Experience PlatformAPI。

>[!IMPORTANT]
>
>选择 **[!UICONTROL OAuth服务器到服务器]** 方法，因为这将是今后唯一支持的方法。 此 **[!UICONTROL 服务帐户(JWT)]** 方法已弃用。 虽然使用JWT身份验证方法的集成将继续工作到2025年1月1日，但Adobe强烈建议您在该日期之前将现有集成迁移到新的OAuth服务器到服务器方法。 在部分获取更多信息 [!BADGE 已弃用]{type=negative}[生成JSON Web令牌(JWT)](#jwt).

![选择Experience PlatformAPI。](./images/api-authentication/oauth-authentication-method.png)

### 为您的集成选择产品配置文件 {#select-product-profiles}

在 **[!UICONTROL 配置API]** 屏幕，选择 **[!UICONTROL AEP-Default-All-Users]**.

<!--
Your integration's service account will gain access to granular features through the product profiles selected here.

-->

>[!IMPORTANT]
>
要访问Platform中的某些功能，您还需要系统管理员授予您必要的基于属性的访问控制权限。 有关更多信息，请参阅部分。 [获取必要的基于属性的访问控制权限](#get-abac-permissions).

![为您的集成选择产品配置文件。](./images/api-authentication/select-product-profiles.png)

选择 **[!UICONTROL 保存配置的API]** 准备就绪后。

以下视频教程中也提供了上述步骤的演练，以设置与Experience PlatformAPI的集成：

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on)

### 收集凭据 {#gather-credentials}

将API添加到项目后， **[!UICONTROL EXPERIENCE PLATFORMAPI]** 项目页面显示所有Experience PlatformAPI调用所需的以下凭据：

![在Developer Console中添加API后的集成信息。](./images/api-authentication/api-integration-information.png)

* `{API_KEY}` ([!UICONTROL 客户端ID])
* `{ORG_ID}` ([!UICONTROL 组织 ID])

<!--

![](././images/api-authentication/api-key-ims-org.png)

<!--

In addition to the above credentials, you also need the generated **[!UICONTROL Client Secret]** for a future step. Select **[!UICONTROL Retrieve client secret]** to reveal the value, and then copy it for later use.

![](././images/api-authentication/client-secret.png)

-->

## 生成访问令牌 {#generate-access-token}

下一步是生成 `{ACCESS_TOKEN}` 用于平台API调用的凭据。 与的值不同 `{API_KEY}` 和 `{ORG_ID}`，必须每24小时生成一个新令牌才能继续使用平台API。 选择 **[!UICONTROL 生成访问令牌]**，如下所示。

![显示如何生成访问令牌](././images/api-authentication/generate-access-token.gif)

>[!TIP]
>
您还可以使用Postman环境和收藏集来生成访问令牌。 有关更多信息，请阅读关于 [使用Postman验证和测试API调用](#use-postman).

## [!BADGE 已弃用]{type=negative}生成JSON Web令牌(JWT) {#jwt}

>[!WARNING]
>
已弃用用于生成访问令牌的JWT方法。 所有新的集成都必须使用 [OAuth服务器到服务器身份验证方法](#select-oauth-server-to-server). Adobe 还建议您将现有集成迁移到 OAuth 方法。请阅读以下重要文档：
> 
* [应用程序从JWT到OAuth的迁移指南](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)
* [采用 OAuth 的新旧应用程序的实施指南](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/)
* [使用OAuth服务器到服务器凭据方法的优势](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#why-oauth-server-to-server-credentials)

+++ 查看已弃用的信息

下一步是根据您的帐户凭据生成JSON Web令牌(JWT)。 此值用于生成 `{ACCESS_TOKEN}` 用于平台API调用的凭据，必须每24小时重新生成一次。

>[!IMPORTANT]
>
在本教程中，以下步骤概述了如何在开发人员控制台中生成JWT。 但是，这种生成方法只应用于测试和评估目的。
>
对于常规使用，必须自动生成JWT。 有关如何以编程方式生成JWT的更多信息，请参阅 [服务帐户身份验证指南](https://www.adobe.io/developer-console/docs/guides/authentication/JWT/) 在Adobe Developer上。

选择 **[!UICONTROL 服务帐户(JWT)]** 在左侧导航中，然后选择 **[!UICONTROL 生成JWT]**.

![](././images/api-authentication/generate-jwt.png)

在以下位置提供的文本框中： **[!UICONTROL 生成自定义JWT]**，粘贴您之前在将平台API添加到服务帐户时生成的私钥的内容。 然后，选择 **[!UICONTROL 生成令牌]**.

![](././images/api-authentication/paste-key.png)

页面将更新以显示生成的JWT，以及一个允许您生成访问令牌的示例cURL命令。 在本教程中，选择 **[!UICONTROL 复制]** 旁边 **[!UICONTROL 生成的JWT]** 以将令牌复制到剪贴板。

![](././images/api-authentication/copy-jwt.png)

**生成访问令牌**

生成JWT后，您可以在API调用中使用它来生成 `{ACCESS_TOKEN}`. 与的值不同 `{API_KEY}` 和 `{ORG_ID}`，必须每24小时生成一个新令牌才能继续使用平台API。

**请求**

以下请求生成一个新的 `{ACCESS_TOKEN}` 基于有效负载中提供的凭据。 此端点仅接受表单数据作为其有效负载，因此必须为 `Content-Type` 页眉 `multipart/form-data`.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| 属性 | 描述 |
| --- | --- |
| `{API_KEY}` | 此 `{API_KEY}` ([!UICONTROL 客户端ID])中检索到的值 [上一步](#api-ims-secret). |
| `{SECRET}` | 您在中检索到的客户端密码 [上一步](#api-ims-secret). |
| `{JWT}` | 您在中生成的JWT [上一步](#jwt). |

>[!NOTE]
>
您可以使用相同的API密钥、客户端密钥和JWT为每个会话生成新的访问令牌。 这允许您在应用程序中自动生成访问令牌。

**响应**

```json
{
  "token_type": "bearer",
  "access_token": "{ACCESS_TOKEN}",
  "expires_in": 86399992
}
```

| 属性 | 描述 |
| --- | --- |
| `token_type` | 返回的令牌的类型。 对于访问令牌，此值始终为 `bearer`. |
| `access_token` | 生成的 `{ACCESS_TOKEN}`. 此值，以单词为前缀 `Bearer`，必须作为 `Authentication` 所有平台API调用的标头。 |
| `expires_in` | 访问令牌过期前剩余的毫秒数。 一旦此值达到0，必须生成新的访问令牌才能继续使用平台API。 |

+++

## 测试访问凭据 {#test-credentials}

收集完所有三个所需的凭据（访问令牌、API密钥和组织ID）后，您可以尝试进行以下API调用。 此调用列出了所有标准 [!DNL Experience Data Model] (XDM)类可供您的组织使用。 在中导入并执行调用 [Postman](#use-postman).

>[!BEGINSHADEBOX]

**请求**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}'
```

**响应**

如果您的响应与下面显示的响应类似，则您的凭据有效且有效。 （此响应已因空间而被截断。）

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

>[!ENDSHADEBOX]

>[!IMPORTANT]
>
虽然上述调用足以测试您的访问凭据，但请注意，如果没有基于属性的正确访问控制权限，您将无法访问或修改多个资源。 有关更多信息，请参阅 **获取必要的基于属性的访问控制权限** 部分。

## 获取必要的基于属性的访问控制权限 {#get-abac-permissions}

要访问或修改Experience Platform中的多个资源，您必须具有相应的访问控制权限。 系统管理员可以向您授予 [所需的权限](/help/access-control/ui/permissions.md). 在部分中获取有关 [管理角色的API凭据](/help/access-control/abac/ui/permissions.md#manage-api-credentials-for-role).

以下视频教程中也提供了有关系统管理员如何授予通过API访问Platform资源所需的权限的详细信息：

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on&t=159)

## 使用Postman验证和测试API调用 {#use-postman}

[Postman](https://www.postman.com/) 是一个常用的工具，它允许开发人员探索和测试RESTful API。 您可以使用Experience PlatformPostman收藏集和环境来加速使用Experience PlatformAPI。 详细了解 [在Experience Platform中使用Postman](/help/landing/postman.md) 以及收藏集和环境的快速入门。

以下视频教程中也提供了有关将Postman与Experience Platform集合和环境结合使用的详细信息：

**下载并导入要与Experience PlatformAPI一起使用的Postman环境**

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on&t=106)

**使用Postman收藏集生成访问令牌**

下载 [Identity Management服务Postman收藏集](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) 并观看以下视频，了解如何生成访问令牌。

>[!VIDEO](https://video.tv.adobe.com/v/29698/?learn=on)

**下载Experience PlatformAPI Postman收藏集并与API交互**

>[!VIDEO](https://video.tv.adobe.com/v/29704/?learn=on)

<!--
This [Medium post](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) describes how you can set up Postman to automatically perform JWT authentication and use it to consume Platform APIs.
-->

## 系统管理员：通过Experience Platform权限授予开发人员和API访问控制 {#grant-developer-and-api-access-control}

>[!NOTE]
>
只有系统管理员才能在“权限”中查看和管理API凭据。

在Adobe Developer控制台上创建集成之前，您的帐户必须具有Adobe Admin Console中Experience Platform产品配置文件的开发人员和用户权限。

### 将开发人员添加到产品配置文件 {#add-developers-to-product-profile}

转至[[!DNL Admin Console]](https://adminconsole.adobe.com/)并使用您的 Adobe ID 登录。

选择 **[!UICONTROL 产品]**，然后选择 **[!UICONTROL Adobe Experience Platform]** 从产品列表中。

![Admin Console上的产品列表](././images/api-authentication/products.png)

从 **[!UICONTROL 产品配置文件]** 选项卡，选择 **[!UICONTROL AEP-Default-All-Users]**. 或者，使用搜索栏通过输入名称来搜索产品配置文件。

![搜索产品配置文件](././images/api-authentication/select-product-profile.png)

选择 **[!UICONTROL 开发人员]** 选项卡，然后选择 **[!UICONTROL 添加开发人员]**.

![从“开发人员”选项卡添加开发人员](././images/api-authentication/add-developer1.png)

输入开发人员的 **[!UICONTROL 电子邮件或用户名]**. 有效的 [!UICONTROL 电子邮件或用户名] 将显示开发人员详细信息。 选择&#x200B;**[!UICONTROL 保存]**。

![使用开发人员的电子邮件或用户名添加开发人员](././images/api-authentication/add-developer-email.png)

开发人员已成功添加，并显示在 [!UICONTROL 开发人员] 选项卡。

![“开发人员”选项卡上列出的开发人员](././images/api-authentication/developer-added.png)

<!--

Commenting out this part since it duplicates information from the section Add Experience Platform to a project

### Set up an API

A developer can add and configure an API within a project in the Adobe Developer Console.

Select your project, then select **[!UICONTROL Add API]**.

![Add API to a project](././images/api-authentication/add-api-project.png)

In the **[!UICONTROL Add an API]** dialog box select **[!UICONTROL Adobe Experience Platform]**, then select **[!UICONTROL Experience Platform API]**.

![Add an API in Experience Platform](././images/api-authentication/add-api-platform.png)

In the **[!UICONTROL Configure API]** screen, select **[!UICONTROL AEP-Default-All-Users]**.

-->

### 将API分配给角色

系统管理员可以在Experience PlatformUI中将API分配给角色。

选择 **[!UICONTROL 权限]** 以及要将API添加到的角色。 选择 **[!UICONTROL API凭据]** 选项卡，然后选择 **[!UICONTROL 添加API凭据]**.

![选定角色中的“API凭据”选项卡](././images/api-authentication/api-credentials.png)

选择要添加到角色的API，然后选择 **[!UICONTROL 保存]**.

![可供选择的API列表](././images/api-authentication/select-api.png)

您将返回 [!UICONTROL API凭据] 选项卡，其中列出了新添加的API。

![包含新添加的API的“API凭据”选项卡](././images/api-authentication/api-credentials-with-added-api.png)

## 其他资源 {#additional-resources}

请参阅下面链接的其他资源，以获取开始使用Experience PlatformAPI的更多帮助

* [验证和访问Experience PlatformAPI](https://experienceleague.adobe.com/docs/platform-learn/tutorials/platform-api-authentication.html?lang=zh-Hans) 视频教程页面
* [Identity Management服务Postman收藏集](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) 用于生成访问令牌
* [Experience PlatformAPI Postman收藏集](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)

## 后续步骤 {#next-steps}

通过阅读本文档，您已收集并成功测试您的Platform API访问凭据。 现在，您可以遵循在整个过程中提供的示例API调用 [文档](../landing/documentation/overview.md).

除了您在本教程中收集的身份验证值之外，许多Platform API还需要有效的 `{SANDBOX_NAME}` 将作为标头提供。 有关更多信息，请参阅[沙盒概述](../sandboxes/home.md)。
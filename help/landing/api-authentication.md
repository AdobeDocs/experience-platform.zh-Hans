---
keywords: Experience Platform；主页；热门主题；身份验证；访问
solution: Experience Platform
title: 验证和访问Experience PlatformAPI
topic: 教程
type: 教程
description: '此文档分步说明了如何获取 Adobe Experience Platform 开发人员帐户访问权限以调用 Experience Platform API。 '
translation-type: tm+mt
source-git-commit: ca5c8527b1b54856aa1e762a06ddbe404f30ec42
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 4%

---


# 验证和访问[!DNL Experience Platform] API

本文档提供了一个分步教程，用于获取对Adobe Experience Platform开发人员帐户的访问权限，以便对[!DNL Experience Platform] API进行调用。

## 进行身份验证以发出API调用

为了维护应用程序和用户的安全，对Adobe I/OAPI的所有请求必须使用OAuth和JSON Web令牌(JWT)等标准进行身份验证和授权。 然后，JWT与客户特定信息一起使用，以生成您的个人访问令牌。

本教程介绍通过创建以下流程图中概述的访问令牌进行身份验证的步骤：
![](images/api-authentication/authentication-flowchart.png)

## 先决条件

为了成功调用[!DNL Experience Platform] API，您需要：

* 可访问Adobe Experience Platform的IMS组织
* 已注册的Adobe ID帐户
* Admin Console管理员将您添加为产品的&#x200B;**开发人员**&#x200B;和&#x200B;**用户**。

以下部分将逐步介绍创建Adobe ID以及成为组织的开发人员和用户的步骤。

### 创建Adobe ID

如果您没有Adobe ID，则可以使用以下步骤创建一个：

1. 转到[Adobe开发人员控制台](https://console.adobe.io)
2. 选择&#x200B;**[!UICONTROL 创建新帐户]**
3. 完成注册过程

## 成为组织[!DNL Experience Platform]的开发人员和用户

在Adobe I/O上创建集成之前，您的帐户必须对IMS组织中的某个产品具有开发人员权限。 有关该Admin Console的开发者帐户的详细信息，请参阅[支持文档](https://helpx.adobe.com/cn/enterprise/using/manage-developers.html)，以管理开发者。

**获得开发人员访问权限**

请联系您组织中的[!DNL Admin Console]管理员，将您添加为使用[[!DNL Admin Console]](https://adminconsole.adobe.com/)的贵组织某个产品的开发者。

![](images/api-authentication/assign-developer.png)

管理员必须将您指定为开发人员，以便至少向一个产品用户档案分配以继续。

![](images/api-authentication/add-developer.png)

一旦您被分配为开发人员，您将拥有在[Adobe I/O](https://www.adobe.com/go/devs_console_ui)上创建集成的访问权限。 这些集成是从外部应用程序和服务到Adobe API的管道。

**获取用户访问权限**

您的[!DNL Admin Console]管理员还必须以用户身份将您添加到产品中。

![](images/api-authentication/assign-users.png)

与添加开发人员的过程类似，管理员必须将您分配给至少一个产品用户档案才能继续。

![](images/api-authentication/assign-user-details.png)

## 在Adobe Developer Console中生成访问凭据

>[!NOTE]
>
>如果您正在从[Privacy Service开发人员指南](../privacy-service/api/getting-started.md)中执行此文档，您现在可以返回该指南，生成[!DNL Privacy Service]特有的访问凭据。

使用Adobe Developer Console，您必须生成以下三个访问凭据：

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

您的`{IMS_ORG}`和`{API_KEY}`只需生成一次，就可以在将来的[!DNL Platform] API调用中重用。 但是，您的`{ACCESS_TOKEN}`是临时的，必须每24小时重新生成一次。

下面详细介绍了这些步骤。

### 一次性设置

转到[Adobe Developer Console](https://www.adobe.com/go/devs_console_ui)并使用您的Adobe ID登录。 接下来，按照教程中概述的步骤操作，该教程位于“Adobe开发人员控制台”文档中的[创建空项目](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md)。

创建新项目后，在&#x200B;**项目概述**&#x200B;屏幕上选择&#x200B;**[!UICONTROL 添加API]**。

![](images/api-authentication/add-api-button.png)

出现&#x200B;**添加API**&#x200B;屏幕。 选择Adobe Experience Platform的产品图标，然后选择&#x200B;**[!UICONTROL Experience PlatformAPI]**，然后选择&#x200B;**[!UICONTROL 下一步]**。

![](images/api-authentication/add-platform-api.png)

选择[!DNL Experience Platform]作为要添加到项目的API后，请按照教程中概述的步骤，使用服务帐户(JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md)（从“配置API”步骤开始）将API添加到项目。 [

将API添加到项目后，**项目概述**&#x200B;页面将显示对[!DNL Experience Platform] API的所有调用中所需的以下凭据：

* `{API_KEY}` （客户端ID）
* `{IMS_ORG}` (Organization ID)

![](./images/api-authentication/api-key-ims-org.png)

### 每个会话的身份验证

您必须收集的最终必需凭据是您的`{ACCESS_TOKEN}`。 与`{API_KEY}`和`{IMS_ORG}`的值不同，必须每24小时生成一个新令牌才能继续使用[!DNL Platform] API。

要生成新`{ACCESS_TOKEN}`，请按照“开发人员控制台凭据指南”中的步骤[生成JWT令牌](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md)。

## 测试访问凭据

收集所有三个必需凭据后，您可以尝试进行以下API调用。 此调用将列表模式注册表`global`容器中的所有[!DNL Experience Data Model](XDM)类：

**API格式**

```http
GET /global/classes
```

**请求**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**响应**

如果您的响应与下面所示的类似，则您的凭据有效且有效。 （此响应已截断空间。）

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

## 使用Postman进行JWT身份验证和API调用

[Postman](https://www.postman.com/) 是使用RESTful API的常用工具。此[中篇帖子](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)介绍如何设置邮件人以自动执行JWT身份验证并使用它使用Adobe Experience Platform API。

## 后续步骤

通过阅读此文档，您收集并成功测试了[!DNL Platform] API的访问凭据。 您现在可以按照[平台API快速入门指南](api-guide.md)中提供的示例进行操作。 本指南包含指向每个平台服务的API指南的链接，并提供其他信息。 错误、Postman和JSON。

除了在本教程中收集的身份验证值之外，许多[!DNL Platform] API还要求提供有效的`{SANDBOX_NAME}`作为头。 有关详细信息，请参阅[沙箱概述](../sandboxes/home.md)。
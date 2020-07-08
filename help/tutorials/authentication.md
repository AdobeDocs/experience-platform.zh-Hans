---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 验证和访问Experience PlatformAPI
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 1%

---


# 验证和访问Experience PlatformAPI

此文档提供了一个分步教程，用于获取对Adobe Experience Platform开发者帐户的访问权，以便调用Experience PlatformAPI。

## 进行身份验证以进行API调用

为了维护应用程序和用户的安全性，对Adobe I/O API的所有请求都必须使用OAuth和JSON Web令牌(JWT)等标准进行身份验证和授权。 然后，JWT与客户特定信息一起使用，以生成您的个人访问令牌。

本教程介绍通过创建流程图中概述的访问令牌进行身份验证的步骤：
![](images/authentication/authentication-flowchart.png)

## 先决条件

为了成功调用Experience PlatformAPI，您需要：

* 可访问Adobe Experience Platform的IMS组织
* 注册的Adobe ID帐户
* Admin Console管理员将您添加为 **开发** 人 **员** 和产品用户。

以下部分将逐步介绍创建Adobe ID以及成为组织的开发人员和用户的步骤。

### 创建Adobe ID

如果您没有Adobe ID，可以使用以下步骤创建一个：

1. 转到Adobe [开发人员控制台](https://console.adobe.io)
2. 单击 **创建新帐户**
3. 完成注册过程

## 成为组织的Experience Platform开发人员和用户

在Adobe I/O上创建集成之前，您的帐户必须对IMS组织中的某个产品具有开发人员权限。 有关该Admin Console的开发人员帐户的详细信息，请参阅 [支持文档](https://helpx.adobe.com/cn/enterprise/using/manage-developers.html) ，以管理开发人员。

**获得开发人员访问权限**

与组织中的Admin Console管理员联系，将您添加为使用Admin Console的贵组织某个产品的开发 [人员](https://adminconsole.adobe.com/)。

![](images/authentication/assign-developer.png)

管理员必须将您指定为开发人员，以便至少让一个产品用户档案继续。

![](images/authentication/add-developer.png)

一旦您被分配为开发人员，您将拥有在Adobe I/O上创建集 [成的访问权限](https://www.adobe.com/go/devs_console_ui)。 这些集成是从外部应用程序和服务到Adobe API的管道。

**获得用户访问权限**

您的Admin Console管理员还必须以用户身份将您添加到产品中。

![](images/authentication/assign-users.png)

与添加开发人员的过程类似，管理员必须将您分配给至少一个产品用户档案才能继续。

![](images/authentication/assign-user-details.png)

## 在Adobe Developer Console中生成访问凭据

>[!NOTE]
>
>如果您正在从文档开发人 [员指南中遵循此Privacy Service](../privacy-service/api/getting-started.md)，您现在可返回该指南以生成Privacy Service特有的访问凭据。

使用Adobe Developer Console，您必须生成以下三个访问凭据：

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

您 `{IMS_ORG}` 的 `{API_KEY}` 只需生成一次，以后的Platform API调用中即可重用。 但是，您的计 `{ACCESS_TOKEN}` 划是临时的，必须每24小时再生一次。

下面详细介绍了这些步骤。

### 一次性设置

转到 [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) ，使用Adobe ID登录。 接下来，按照教程中概述的步 [骤操作，在Adobe](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) Developer Console文档中创建空项目。

创建新项目后，单击“项 **[!UICONTROL 目概述]** ”屏 _幕上的“添加API_ ”。

![](images/authentication/add-api-button.png)

出 _现添加API_ 屏幕。 单击Adobe Experience Platform的产品图标，然后选择 **[!UICONTROL Experience PlatformAPI]** ，然后单 **[!UICONTROL 击下一]**&#x200B;步。

![](images/authentication/add-platform-api.png)

选择Experience Platform作为要添加到项目的API后，请按照教程中概述的步骤，使用服务帐户( [JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) （从“配置API”步骤开始）将API添加到项目，以完成该过程。

将API添加到项目后，“项目 _概述_ ”页将显示对Experience PlatformAPI的所有调用中所需的以下凭据：

* `{API_KEY}` （客户端ID）
* `{IMS_ORG}` (Organization ID)

![](./images/authentication/api-key-ims-org.png)

### 每个会话的身份验证

您必须收集的最终所需凭据是您的 `{ACCESS_TOKEN}`。 与和的值 `{API_KEY}` 不 `{IMS_ORG}`同，必须每24小时生成一个新令牌才能继续使用平台API。

要生成新代码， `{ACCESS_TOKEN}`请按照“开发人 [员控制台凭据指南](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) ”中的步骤生成JWT令牌。

## 测试访问凭据

收集所有三个必需凭据后，您可以尝试进行以下API调用。 此调用将列表模式注册表容器中的所有体验数据模型(XDM)类 `global` :

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

如果您的响应与下面显示的响应类似，则您的凭据有效且有效。 （此响应已被截断为空间。）

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

[Postman](https://www.getpostman.com/) 是使用REST风格的API的常用工具。 此 [中篇文章](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) 介绍如何设置邮递员以自动执行JWT身份验证，并使用它使用Adobe Experience PlatformAPI。

## 后续步骤

通过阅读此文档，您已收集并成功测试了Platform API的访问凭据。 您现在可以按照文档中提供的示例API调 [用操作](../landing/documentation/overview.md)。

除了在本教程中收集的身份验证值之外，许多平台API还要求以标 `{SANDBOX_NAME}` 头形式提供有效。 有关更多 [信息，请参](../sandboxes/home.md) 阅沙箱概述。
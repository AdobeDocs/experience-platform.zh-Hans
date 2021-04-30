---
keywords: Experience Platform；主页；热门主题；身份验证；访问
solution: Experience Platform
title: 验证和访问Experience PlatformAPI
topic-legacy: tutorial
type: Tutorial
description: 此文档分步说明了如何获取 Adobe Experience Platform 开发人员帐户访问权限以调用 Experience Platform API。
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
translation-type: tm+mt
source-git-commit: ef00f50ea2cda2c173208075123b3fe2b2d7ecd4
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 6%

---


# 身份验证和访问 Experience Platform API

此文档分步说明了如何获取 Adobe Experience Platform 开发人员帐户访问权限以调用 Experience Platform API。在本教程结束时，您将生成所有平台API调用所需的以下凭据：

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{IMS_ORG}`

为了维护应用程序和用户的安全，对Adobe I/OAPI的所有请求必须使用OAuth和JSON Web令牌(JWT)等标准进行身份验证和授权。 JWT与客户特定信息一起使用，以生成您的个人访问令牌。

本教程介绍如何收集所需凭据以验证平台API调用，如下流程图中所述：

![](./images/api-authentication/authentication-flowchart.png)

## 先决条件

要成功调用Experience Platform API，您必须具有以下条件：

* 可访问Adobe Experience Platform的IMS组织。
* Admin Console管理员，能够将您添加为产品用户档案的开发人员和用户。

您还必须有一个Adobe ID才能完成本教程。 如果您没有Adobe ID，则可以使用以下步骤创建一个：

1. 转到[Adobe开发人员控制台](https://console.adobe.io)。
2. 选择 **[!UICONTROL Create a new account]**。
3. 完成注册过程。

## 获得开发人员和用户对Experience Platform的访问

在Adobe Developer Console上创建集成之前，您的帐户必须对Adobe Admin Console中的Experience Platform产品用户档案具有开发人员和用户权限。

### 获得开发人员访问权限

请联系您组织中的[!DNL Admin Console]管理员，以使用[[!DNL Admin Console]](https://adminconsole.adobe.com/)将您添加为Experience Platform产品用户档案的开发人员。 有关如何[管理产品用户档案的开发者访问](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html)的具体说明，请参阅[!DNL Admin Console]文档。

一旦您被分配为开发人员，您就可以开始在[Adobe开发人员控制台](https://www.adobe.com/go/devs_console_ui)中创建集成。 这些集成是从外部应用程序和服务到Adobe API的管道。

### 获取用户访问权限

您的[!DNL Admin Console]管理员还必须将您作为用户添加到同一产品用户档案。 有关详细信息，请参阅 [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html)中的[管理用户组指南。

## 生成API密钥、IMS组织ID和客户端密钥{#api-ims-secret}

>[!NOTE]
>
>如果您正在从[Privacy Service开发人员指南](../privacy-service/api/getting-started.md)中执行此文档，您现在可以返回该指南，生成[!DNL Privacy Service]特有的访问凭据。

在您通过[!DNL Admin Console]获得开发人员和用户对平台的访问权限后，下一步是在Adobe开发人员控制台中生成您的`{IMS_ORG}`和`{API_KEY}`凭据。 这些凭据只需生成一次即可，在将来的Platform API调用中可重复使用。

### 向项目添加Experience Platform

转到[Adobe Developer Console](https://www.adobe.com/go/devs_console_ui)并使用您的Adobe ID登录。 接下来，按照教程中概述的步骤操作，该教程位于“Adobe开发人员控制台”文档中的[创建空项目](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md)。

创建新项目后，在&#x200B;**[!UICONTROL Project Overview]**&#x200B;屏幕上选择&#x200B;**[!UICONTROL Add API]**。

![](./images/api-authentication/add-api.png)

出现&#x200B;**[!UICONTROL Add an API]**&#x200B;屏幕。 选择Adobe Experience Platform的产品图标，然后选择&#x200B;**[!UICONTROL Experience Platform API]**&#x200B;后再选择&#x200B;**[!UICONTROL Next]**。

![](./images/api-authentication/platform-api.png)

在此处，按照教程中概述的步骤，使用服务帐户(JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md)（从“配置API”步骤开始）将API添加到项目，以完成该过程。[

>[!IMPORTANT]
>
>在上面链接的过程中，浏览器会在某个步骤中自动下载私钥和关联的公共证书。 请注意此私钥存储在您的计算机上的位置，因为本教程的稍后步骤中需要此私钥。

### 收集凭据

将API添加到项目后，项目的&#x200B;**[!UICONTROL Experience Platform API]**&#x200B;页面将显示对Experience Platform API的所有调用中所需的以下凭据：

* `{API_KEY}` ([!UICONTROL Client ID])
* `{IMS_ORG}` ([!UICONTROL Organization ID])

![](././images/api-authentication/api-key-ims-org.png)

除了上述凭据之外，您还需要生成&#x200B;**[!UICONTROL Client Secret]**&#x200B;以用于将来的步骤。 选择&#x200B;**[!UICONTROL Retrieve client secret]**&#x200B;以显示该值，然后复制该值以备以后使用。

![](././images/api-authentication/client-secret.png)

## 生成JSON Web令牌(JWT){#jwt}

下一步是根据您的帐户凭据生成JSON Web令牌(JWT)。 此值用于生成`{ACCESS_TOKEN}`凭据以用于平台API调用，必须每24小时重新生成一次。

在左侧导航中选择&#x200B;**[!UICONTROL Service Account (JWT)]**，然后选择&#x200B;**[!UICONTROL Generate JWT]**。

![](././images/api-authentication/generate-jwt.png)

在&#x200B;**[!UICONTROL Generate custom JWT]**&#x200B;下提供的文本框中，粘贴之前在将平台API添加到服务帐户时生成的私钥的内容。 然后，选择&#x200B;**[!UICONTROL Generate Token]**。

![](././images/api-authentication/paste-key.png)

页面将更新以显示生成的JWT，以及允许您生成访问令牌的示例cURL命令。 为本教程的目的，请选择&#x200B;**[!UICONTROL Generated JWT]**&#x200B;旁边的&#x200B;**[!UICONTROL Copy]**&#x200B;以将令牌复制到剪贴板。

![](././images/api-authentication/copy-jwt.png)

## 生成访问令牌

生成JWT后，您可以在API调用中使用它生成`{ACCESS_TOKEN}`。 与`{API_KEY}`和`{IMS_ORG}`的值不同，必须每24小时生成一个新令牌才能继续使用平台API。

**请求**

以下请求根据在有效负荷中提供的凭据生成新的`{ACCESS_TOKEN}`。 此端点仅接受表单数据作为其有效负荷，因此必须为它提供`multipart/form-data`的`Content-Type`头。

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| 属性 | 描述 |
| --- | --- |
| `{API_KEY}` | 您在上一步[中检索的`{API_KEY}`([!UICONTROL Client ID])。](#api-ims-secret) |
| `{SECRET}` | 您在上一步[中检索到的客户端密码](#api-ims-secret)。 |
| `{JWT}` | 您在上一步[中生成的JWT](#jwt)。 |

>[!NOTE]
>
>您可以使用相同的API密钥、客户端机密和JWT为每个会话生成新访问令牌。 这使您能够在应用程序中自动生成访问令牌。

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
| `token_type` | 要返回的标记类型。 对于访问令牌，此值始终为`bearer`。 |
| `access_token` | 生成的`{ACCESS_TOKEN}`。 此值前缀为`Bearer`，是所有平台API调用的`Authentication`头。 |
| `expires_in` | 在访问令牌过期之前剩余的毫秒数。 此值达到0后，必须生成新访问令牌才能继续使用平台API。 |

## 测试访问凭据

收集所有三个必需凭据后，您可以尝试进行以下API调用。 此调用将列表组织可用的所有标准[!DNL Experience Data Model](XDM)类。

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

## 使用Postman验证和测试API调用

[Postman是](https://www.postman.com/) 一款流行的工具，它允许开发人员探索和测试REST风格的API。此[Medium post](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f)说明如何设置Postman以自动执行JWT身份验证并使用它使用平台API。

## 后续步骤

通过阅读此文档，您收集并成功测试了平台API的访问凭据。 现在，您可以跟随在[文档](../landing/documentation/overview.md)中提供的示例API调用。

除了在本教程中收集的身份验证值之外，许多平台API还要求以有效的`{SANDBOX_NAME}`作为头提供。 有关详细信息，请参阅[沙箱概述](../sandboxes/home.md)。
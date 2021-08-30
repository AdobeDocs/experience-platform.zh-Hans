---
title: Reactor API快速入门
description: 了解如何开始使用Reactor API，包括生成所需访问凭据的步骤。
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---

# Reactor API快速入门

要使用[Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/)，每个请求必须包含以下身份验证标头：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

本指南介绍如何使用Adobe开发人员控制台收集每个标头的值，以便您开始调用Reactor API。

## 获取开发人员访问Adobe Experience Platform的权限

在为Reactor API生成身份验证值之前，您必须拥有开发人员Experience Platform权限。 要获得开发人员访问权限，请按照[Experience Platform身份验证教程](http://www.adobe.com/go/platform-api-authentication-en)中的开始步骤操作。 在您完成步骤“在Adobe开发人员控制台中生成访问凭据”后，返回到本教程以生成特定于Reactor API的凭据。

## 生成访问凭据

使用Adobe开发人员控制台，您必须生成以下三个访问凭据：

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

您的IMS组织的ID(`{IMS_ORG}`)和API密钥(`{API_KEY}`)在最初生成之后，可以在将来的API调用中重复使用。 但是，您的访问令牌(`{ACCESS_TOKEN}`)是临时的，必须每24小时重新生成一次。

有关生成这些值的步骤，请参见下文。

### 一次性设置

转到[Adobe开发人员控制台](https://www.adobe.com/go/devs_console_ui)并使用Adobe ID登录。 接下来，按照开发人员控制台文档中[创建空项目](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md)的教程中概述的步骤操作。

创建项目后，在&#x200B;**项目概述**&#x200B;屏幕上选择&#x200B;**添加API** 。

![](../images/api/getting-started/add-api-button.png)

出现&#x200B;**添加API**&#x200B;屏幕。 在选择&#x200B;**Next**&#x200B;之前，从可用API列表中选择&#x200B;**Experience PlatformReactor API**。

![](../images/api/getting-started/add-launch-api.png)

在下一个屏幕中，系统会提示您创建JSON Web令牌(JWT)凭据，以生成新密钥对或上传您自己的公钥。 在本教程中，选择&#x200B;**生成键对**&#x200B;选项，然后选择右下角的&#x200B;**生成键对** 。

![](../images/api/getting-started/create-jwt.png)

下一个屏幕确认密钥对已成功生成，并且包含公共证书和私钥的压缩文件夹会自动下载到您的计算机。 在后续步骤中需要此私钥才能生成访问令牌。

选择&#x200B;**Next**&#x200B;以继续。

![](../images/api/getting-started/keypair-generated.png)

下一个屏幕会提示您选择一个或多个要与API集成关联的产品配置文件。

>[!NOTE]
>
>产品配置文件由您的组织通过Adobe Admin Console进行管理，并包含针对具体功能的特定权限集。 产品配置文件及其权限只能由组织内具有管理员权限的用户管理。 如果不确定要为API选择哪些产品配置文件，请联系您的管理员。

从列表中选择所需的产品配置文件，然后选择&#x200B;**保存配置的API**&#x200B;以完成API注册。

![](../images/api/getting-started/select-product-profile.png)

将API添加到项目后，项目页面会重新显示在Experience PlatformReactor API页面中。 从此处，向下滚动到&#x200B;**服务帐户(JWT)**&#x200B;部分，该部分提供所有Reactor API调用中所需的以下访问凭据：

* **客户端ID**:客户端ID是必需ID， `{API_KEY}` 必须在标头中提 `x-api-key` 供。
* **组织ID**:组织ID是必 `{IMS_ORG}` 须在标题中使用的 `x-gw-ims-org-id` 值。

![](../images/api/getting-started/access-creds.png)

### 每个会话的身份验证

现在，您已拥有`{API_KEY}`和`{IMS_ORG}`值，最后一步是生成`{ACCESS_TOKEN}`值。

>[!NOTE]
>
>这些令牌在24小时后过期。 如果您将此集成用于应用程序，最好从应用程序内以编程方式获取载体令牌。

根据用例的不同，您有两个选项可用于生成访问令牌：

* [手动生成令牌](#manual)
* [以编程方式生成令牌](#program)

#### 手动生成访问令牌 {#manual}

在文本编辑器或浏览器中打开之前下载的私钥，并复制其内容。 然后，导航回开发人员控制台，并在选择&#x200B;**生成令牌**&#x200B;之前，将私钥粘贴到项目Reactor API页面的&#x200B;**生成访问令牌**&#x200B;部分。

![](../images/api/getting-started/paste-private-key.png)

将生成新的访问令牌，并提供一个用于将令牌复制到剪贴板的按钮。 此值用于所需的`Authorization`标头，且必须以`Bearer {ACCESS_TOKEN}`格式提供。

![](../images/api/getting-started/token-generated.png)

#### 以编程方式生成访问令牌 {#program}

如果您将集成用于应用程序，则可以通过API请求以编程方式生成访问令牌。 要完成此操作，您必须获取以下值：

* 客户端ID(`{API_KEY}`)
* 客户端密钥(`{SECRET}`)
* JSON Web令牌(`{JWT}`)

可以从项目的主页获取您的客户端ID和密钥，如[上一步](#one-time-setup)中所示。

![](../images/api/getting-started/auto-access-creds.png)

要获取JWT凭据，请导航到左侧导航中的&#x200B;**服务帐户(JWT)**，然后选择&#x200B;**生成JWT**&#x200B;选项卡。 在本页的&#x200B;**生成自定义JWT**&#x200B;下，将私钥的内容粘贴到提供的文本框中，然后选择&#x200B;**生成令牌**。

![](../images/api/getting-started/generate-jwt.png)

生成的JWT在完成处理后即会显示在下方，并且还会显示一个示例cURL命令，您可以根据需要使用该命令来测试令牌。 使用&#x200B;**Copy**&#x200B;按钮将令牌复制到剪贴板。

![](../images/api/getting-started/jwt-generated.png)

收集凭据后，您可以将下面的API调用集成到您的应用程序中，以便以编程方式生成访问令牌。

**请求**

请求必须发送`multipart/form-data`负载，并提供您的身份验证凭据，如下所示：

```shell
curl -X POST \
  https://ims-na1.adobelogin.com/ims/exchange/jwt/ \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

**响应**

成功响应会返回新的访问令牌，以及到其过期的剩余秒数。

```json
{
  "token_type": "bearer",
  "access_token": "{ACCESS_TOKEN}",
  "expires_in": 86399999
}
```

| 属性 | 描述 |
| :-- | :-- |
| `access_token` | 新生成的访问令牌值。 此值用于所需的`Authorization`标头，且必须以`Bearer {ACCESS_TOKEN}`格式提供。 |
| `expires_in` | 令牌过期的剩余时间（以毫秒为单位）。 令牌过期后，必须生成一个新令牌。 |

{style=&quot;table-layout:auto&quot;}

## 后续步骤

按照本教程中的步骤，您应具有`{IMS_ORG}`、`{API_KEY}`和`{ACCESS_TOKEN}`的有效值。 您现在可以在对Reactor API的简单cURL请求中使用这些值来测试这些值。

首先尝试对[列出所有公司](./endpoints/companies.md#list)进行API调用。

>[!NOTE]
>
>您的组织中可能没有任何公司，在这种情况下，响应将为HTTP状态404（未找到）。 只要没有收到403（禁止）错误，您的访问凭据就有效且有效。

确认您的访问凭据正在工作后，请继续浏览其他API参考文档，以了解API的许多功能。

## 其他资源

JWT库和SDK:[https://jwt.io/](https://jwt.io/)

Postman API开发：[https://www.postman.com/](https://www.postman.com/)

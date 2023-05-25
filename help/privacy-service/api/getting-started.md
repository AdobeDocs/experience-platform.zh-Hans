---
title: Privacy ServiceAPI快速入门
description: 在文档中了解如何对Privacy ServiceAPI进行身份验证以及如何解释示例API调用。
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 1%

---

# Privacy ServiceAPI快速入门

本指南介绍了在尝试调用Adobe Experience Platform Privacy Service API之前需要了解的核心概念。

## 先决条件

本指南要求您实际了解 [Privacy Service](../home.md) 以及它如何允许您跨Adobe Experience Cloud应用程序管理来自数据主体（客户）的访问和删除请求。

为了创建API的访问凭据，贵组织中的管理员之前必须已在Adobe Admin Console中设置用于Privacy Service的产品配置文件。 您分配给API集成的产品配置文件决定了集成在访问Privacy Service功能时具有的权限。 请参阅指南，网址为 [管理Privacy Service权限](../permissions.md) 了解更多信息。

## 收集所需标题的值

要调用Privacy ServiceAPI，您必须首先收集要在所需标头中使用的访问凭据：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

使用以下方式生成这些值 [Adobe Developer控制台](https://developer.adobe.com/console). 您的 `{ORG_ID}` 和 `{API_KEY}` 只需生成一次，并可在以后的API调用中重复使用。 但是，您的 `{ACCESS_TOKEN}` 是临时的，必须每24小时重新生成一次。

下面详细介绍了生成这些值的步骤。

### 一次性设置

转到 [Adobe Developer控制台](https://developer.adobe.com/console) 然后使用您的Adobe ID登录。 接下来，按照教程中概述的以下步骤进行操作： [创建空项目](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) 在开发人员控制台文档中。

创建新项目后，选择 **[!UICONTROL 添加到项目]** 并选择 **[!UICONTROL API]** 下拉菜单中。

![正在从中选择的API选项 [!UICONTROL 添加到项目] 开发人员控制台中项目详细信息页面的下拉列表](../images/api/getting-started/add-api-button.png)

#### 选择API并生成密钥对 {#keypair}

此 **[!UICONTROL 添加API]** 屏幕。 选择 **[!UICONTROL Experience Cloud]** 要缩小可用API的列表，请选择卡以用于 **[!UICONTROL PRIVACY SERVICEAPI]** 选择之前 **[!UICONTROL 下一个]**.

![从可用API列表中选择的Privacy ServiceAPI卡](../images/api/getting-started/add-privacy-service-api.png)

此 **[!UICONTROL 配置API]** 屏幕。 选择选项以 **[!UICONTROL 生成密钥对]**，然后选择 **[!UICONTROL 生成密钥对]**.

![此 [!UICONTROL 生成密钥对] 选项选择时间： [!UICONTROL 配置API] screen](../images/api/getting-started/generate-key-pair.png)

密钥对会自动生成，并且浏览器将下载包含私钥和公共证书的ZIP文件（以便在后续步骤中使用）。 选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![在UI中显示的生成的密钥对，其值由浏览器自动下载](../images/api/getting-started/key-pair-generated.png)

#### 通过产品配置文件分配权限 {#product-profiles}

最终配置步骤是选择此集成将继承其权限的产品配置文件。 如果选择多个配置文件，则其权限集将针对集成进行合并。

>[!NOTE]
>
>产品配置文件及其提供的粒度权限由管理员通过Adobe Admin Console创建和管理。 请参阅指南，网址为 [Privacy Service权限](../permissions.md) 了解更多信息。

完成后，选择 **[!UICONTROL 保存配置的API]**.

![在保存配置之前从列表中选择单个产品配置文件](../images/api/getting-started/select-product-profiles.png)

将API添加到项目后，项目页面会重新出现在 **Privacy ServiceAPI概述** 页面。 从这里，向下滚动到 **[!UICONTROL 服务帐户(JWT)]** 部分，其中提供了在Privacy ServiceAPI的所有调用中所需的以下访问凭据：

* **[!UICONTROL 客户端ID]**：客户端ID是必需的 `{API_KEY}` 必须在以下位置提供： `x-api-key` 标头。
* **[!UICONTROL 组织ID]**：组织ID是 `{ORG_ID}` 必须在以下位置使用的值： `x-gw-ims-org-id` 标头。

![配置API后，项目概述页面上显示的客户端ID和组织ID值](../images/api/getting-started/jwt-credentials.png)

### 每个会话的身份验证

您必须收集的最终必需凭据是 `{ACCESS_TOKEN}`，在Authorization标头中使用。 与的值不同 `{API_KEY}` 和 `{ORG_ID}`，必须每24小时生成一个新令牌才能继续使用API。

通常，有两种生成访问令牌的方法：

* [手动生成令牌](#manual-token) 用于测试和开发。
* [自动生成令牌](#auto-token) 用于API集成。

#### 手动生成令牌 {#manual-token}

要手动生成新的 `{ACCESS_TOKEN}`，打开之前下载的私钥并将其内容粘贴到旁边的文本框中 **[!UICONTROL 生成访问令牌]** 选择之前 **[!UICONTROL 生成令牌]**.

![将之前生成的访问令牌粘贴到项目的概述页面上，并使用 [!UICONTROL 生成令牌] 按钮选择晚于](../images/api/getting-started/paste-private-key.png)

将生成新的访问令牌，并提供用于将令牌复制到剪贴板的按钮。 此值用于所需的Authorization标头，必须以格式提供 `Bearer {ACCESS_TOKEN}`.

![正在从UI复制生成的访问令牌](../images/api/getting-started/generated-access-token.png)

#### 自动生成令牌 {#auto-token}

您可以通过向AdobeIdentity Management服务(IMS)发出POST请求来发送JSON Web令牌(JWT)，从而为自动化流程生成新的访问令牌。 请参阅上的开发人员控制台文档 [JWT身份验证](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) 以了解详细步骤。

## 正在读取示例API调用

每个端点指南都提供了示例API调用，以演示如何设置请求的格式。 这些资源包括路径、必需的标头和格式正确的请求负载。 此外，还提供了在API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅以下章节： [如何读取示例API调用](../../landing/api-guide.md#sample-api) 《平台API快速入门指南》中的。

## 后续步骤

现在，您已了解要使用哪些标头，可以开始调用Privacy ServiceAPI。 选择一个端点指南以开始：

* [隐私作业](./privacy-jobs.md)
* [同意](./consent.md)

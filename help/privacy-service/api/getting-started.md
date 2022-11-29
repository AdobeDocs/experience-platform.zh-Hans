---
title: Privacy ServiceAPI快速入门
description: 了解如何对Privacy ServiceAPI进行身份验证，以及如何解释文档中的示例API调用。
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 59dc28a84971dc8c21d633741cfe2dc1b44ea1a6
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 1%

---

# Privacy ServiceAPI快速入门

本指南简要介绍在尝试调用Adobe Experience Platform Privacy Service API之前需要了解的核心概念。

## 先决条件

本指南需要对 [Privacy Service](../home.md) 以及它如何让您跨Adobe Experience Cloud应用程序管理来自数据主体（客户）的访问和删除请求。

要为API创建访问凭据，您组织内的管理员之前必须已设置产品配置文件，以便在Adobe Admin Console中Privacy Service。 您分配给API集成的产品配置文件可决定集成在访问Privacy Service功能时具有的权限。 请参阅 [管理Privacy Service权限](../permissions.md) 以了解更多信息。

## 收集所需标题的值

要调用Privacy ServiceAPI，必须先收集要在所需标头中使用的访问凭据：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

这些值是使用 [Adobe Developer控制台](https://developer.adobe.com/console). 您的 `{ORG_ID}` 和 `{API_KEY}` 只需生成一次，便可在将来的API调用中重复使用。 但是，您的 `{ACCESS_TOKEN}` 是临时的，必须每24小时重新生一次。

有关生成这些值的步骤，请参见下文。

### 一次性设置

转到 [Adobe Developer控制台](https://developer.adobe.com/console) 然后使用您的Adobe ID登录。 接下来，按照 [创建空项目](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) 中的文档。

创建新项目后，选择 **[!UICONTROL 添加到项目]** 选择 **[!UICONTROL API]** 下拉菜单中。

![从 [!UICONTROL 添加到项目] 开发人员控制台中项目详细信息页面的下拉列表](../images/api/getting-started/add-api-button.png)

#### 选择API并生成密钥对 {#keypair}

的 **[!UICONTROL 添加API]** 屏幕。 选择 **[!UICONTROL Experience Cloud]** 要缩小可用API的列表，请选择 **[!UICONTROL Privacy ServiceAPI]** 选择 **[!UICONTROL 下一个]**.

![从可用API列表中选择的Privacy ServiceAPI卡](../images/api/getting-started/add-privacy-service-api.png)

的 **[!UICONTROL 配置API]** 屏幕。 选择要 **[!UICONTROL 生成键对]**，然后选择 **[!UICONTROL 生成密钥对]**.

![的 [!UICONTROL 生成键对] 选项 [!UICONTROL 配置API] 屏幕](../images/api/getting-started/generate-key-pair.png)

密钥对将自动生成，并且您的浏览器会下载包含私钥和公共证书的ZIP文件（将在稍后的步骤中使用）。 选择 **[!UICONTROL 下一个]** 继续。

![UI中显示的生成键对，其值由浏览器自动下载](../images/api/getting-started/key-pair-generated.png)

#### 通过产品配置文件分配权限 {#product-profiles}

最终配置步骤是选择此集成将继承其权限的产品配置文件。 如果您选择多个配置文件，则集成将合并其权限集。

>[!NOTE]
>
>产品配置文件及其提供的粒度权限由管理员通过Adobe Admin Console创建和管理。 请参阅 [Privacy Service权限](../permissions.md) 以了解更多信息。

完成后，选择 **[!UICONTROL 保存配置的API]**.

![在保存配置之前，从列表中选择单个产品配置文件](../images/api/getting-started/select-product-profiles.png)

将API添加到项目后，项目页面会重新显示在 **Privacy ServiceAPI概述** 页面。 从此处，向下滚动到 **[!UICONTROL 服务帐户(JWT)]** 部分，该部分提供了所有Privacy ServiceAPI调用中所需的以下访问凭据：

* **[!UICONTROL 客户端ID]**:客户ID是必需的 `{API_KEY}` 必须在 `x-api-key` 标题。
* **[!UICONTROL 组织ID]**:组织ID是 `{ORG_ID}` 的值 `x-gw-ims-org-id` 标题。

![配置API后，项目概述页面上显示的客户端ID和组织ID值](../images/api/getting-started/jwt-credentials.png)

### 每个会话的身份验证

您必须收集的最终所需凭据是 `{ACCESS_TOKEN}`，用于授权标头。 与 `{API_KEY}` 和 `{ORG_ID}`，则必须每24小时生成一个新令牌，才能继续使用API。

通常，有两种方法可生成访问令牌：

* [手动生成令牌](#manual-token) 用于测试和开发。
* [自动生成令牌](#auto-token) （用于API集成）。

#### 手动生成令牌 {#manual-token}

手动生成新 `{ACCESS_TOKEN}`，打开之前下载的私钥并将其内容粘贴到旁边的文本框中 **[!UICONTROL 生成访问令牌]** 选择 **[!UICONTROL 生成令牌]**.

![之前生成的访问令牌将粘贴到项目的概述页面上，其中 [!UICONTROL 生成令牌] 按钮](../images/api/getting-started/paste-private-key.png)

将生成新的访问令牌，并提供一个用于将令牌复制到剪贴板的按钮。 此值用于所需的授权标头，且必须以格式提供 `Bearer {ACCESS_TOKEN}`.

![要从UI复制的生成访问令牌](../images/api/getting-started/generated-access-token.png)

#### 自动生成令牌 {#auto-token}

您可以通过向AdobeIdentity Management服务(IMS)的POST请求发送JSON Web令牌(JWT)，从而为自动化进程生成新的访问令牌。 请参阅 [JWT身份验证](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) 以了解详细步骤。

## 读取示例API调用

每个端点指南都提供了示例API调用，以演示如何设置请求的格式。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/api-guide.md#sample-api) 平台API快速入门指南中的。

## 后续步骤

现在，您已经了解要使用哪些标头，接下来便可以开始调用Privacy ServiceAPI。 选择要开始使用的端点指南之一：

* [隐私作业](./privacy-jobs.md)
* [同意](./consent.md)

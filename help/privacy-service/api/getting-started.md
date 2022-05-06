---
title: Privacy ServiceAPI快速入门
description: 了解如何对Privacy ServiceAPI进行身份验证，以及如何解释文档中的示例API调用。
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# Privacy ServiceAPI快速入门

本指南简要介绍在尝试调用Privacy ServiceAPI之前需要了解的核心概念。

## 先决条件

本指南需要了解以下功能：

* [Adobe Experience Platform Privacy Service](../home.md):提供RESTful API和用户界面，允许您跨Adobe Experience Cloud应用程序管理来自数据主体（客户）的访问和删除请求。

## 收集所需标题的值

要调用Privacy ServiceAPI，必须先收集要在所需标头中使用的访问凭据：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

这包括在Adobe Admin Console中获取Adobe Experience Platform的开发人员权限，然后在Adobe Developer控制台中生成凭据。

### 获取开发人员访问Experience Platform

要获取开发人员访问 [!DNL Platform]，请按照 [Experience Platform身份验证教程](https://www.adobe.com/go/platform-api-authentication-en). 进入“在Adobe Developer控制台中生成访问凭据”步骤后，请返回本教程以生成特定于Privacy Service的凭据。

### 生成访问凭据

使用Adobe Developer控制台，您必须生成以下三个访问凭据：

* `{ORG_ID}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

您的 `{ORG_ID}` 和 `{API_KEY}` 只需生成一次，便可在将来的API调用中重复使用。 但是，您的 `{ACCESS_TOKEN}` 是临时的，必须每24小时重新生一次。

有关生成这些值的步骤，请参见下文。

#### 一次性设置

转到 [Adobe开发人员控制台](https://www.adobe.com/go/devs_console_ui) 然后使用您的Adobe ID登录。 接下来，按照 [创建空项目](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) (在Adobe Developer控制台文档中)。

创建新项目后，选择 **[!UICONTROL 添加API]** 在 **[!UICONTROL 项目概述]** 屏幕。

![](../images/api/getting-started/add-api-button.png)

的 **[!UICONTROL 添加API]** 屏幕。 选择 **[!UICONTROL Privacy ServiceAPI]** 从可用API列表中选择 **[!UICONTROL 下一个]**.

![](../images/api/getting-started/add-privacy-service-api.png)

的 **[!UICONTROL 配置API]** 屏幕。 选择要 **[!UICONTROL 生成键对]**，然后选择 **[!UICONTROL 生成密钥对]** 在右下角。

![](../images/api/getting-started/generate-key-pair.png)

密钥对将自动生成，并将包含私钥和公共证书的ZIP文件下载到本地计算机（将在后续步骤中使用）。 选择 **[!UICONTROL 保存配置的API]** 以完成配置。

![](../images/api/getting-started/key-pair-generated.png)

将API添加到项目后，项目页面会重新显示在 **Privacy ServiceAPI概述** 页面。 从此处，向下滚动到 **[!UICONTROL 服务帐户(JWT)]** 部分，该部分提供了所有Privacy ServiceAPI调用中所需的以下访问凭据：

* **[!UICONTROL 客户端ID]**:客户ID是必需的 `{API_KEY}` ，则必须在x-api-key标头中提供。
* **[!UICONTROL 组织ID]**:组织ID是 `{ORG_ID}` 必须在x-gw-ims-org-id标头中使用的值。

![](../images/api/getting-started/jwt-credentials.png)

#### 每个会话的身份验证

您必须收集的最终所需凭据是 `{ACCESS_TOKEN}`，用于授权标头。 与 `{API_KEY}` 和 `{ORG_ID}`，则必须每24小时生成一个新令牌，才能继续使用 [!DNL Platform] API。

生成新 `{ACCESS_TOKEN}`，打开之前下载的私钥并将其内容粘贴到旁边的文本框中 **[!UICONTROL 生成访问令牌]** 选择 **[!UICONTROL 生成令牌]**.

![](../images/api/getting-started/paste-private-key.png)

将生成新的访问令牌，并提供一个用于将令牌复制到剪贴板的按钮。 此值用于所需的授权标头，且必须以格式提供 `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## 读取示例API调用

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅 [如何阅读示例API调用](../../landing/api-guide.md#sample-api) 平台API快速入门指南中的。

## 后续步骤

现在，您已经了解要使用哪些标头，接下来便可以开始调用Privacy ServiceAPI。 选择要开始使用的端点指南之一：

* [隐私作业](./privacy-jobs.md)
* [同意](./consent.md)

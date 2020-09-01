---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Privacy Service开发人员指南
description: 使用RESTful API跨Adobe Experience Cloud应用程序管理数据主体的个人数据
topic: developer guide
translation-type: tm+mt
source-git-commit: 1bb896f7629d7b71b94dd107eeda87701df99208
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---


# [!DNL Privacy Service] 开发人员指南

Adobe Experience Platform [!DNL Privacy Service] 提供了RESTful API和用户界面，允许您跨Adobe Experience Cloud应用程序管理（访问和删除）数据主体（客户）的个人数据。 [!DNL Privacy Service] 还提供了一个中央审计和日志记录机制，允许您访问涉及应用程序的作业的状态和 [!DNL Experience Cloud] 结果。

本指南介绍如何使用 [!DNL Privacy Service] API。 有关如何使用UI的详细信息，请参阅 [Privacy ServiceUI概述](../ui/overview.md)。 有关API中所有可用端点的全面 [!DNL Privacy Service] 列表，请参阅 [API参考](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html)。

## 入门指南 {#getting-started}

本指南需要了解以下功 [!DNL Experience Platform] 能：

* [[!DNLPrivacy Service]](../home.md):提供REST风格的API和用户界面，允许您跨Adobe Experience Cloud应用程序管理来自数据主体（客户）的访问和删除请求。

以下各节提供了成功调用Privacy ServiceAPI所需了解的其他信息。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅疑难解答 [指南中有关如何阅读示例API调](../../landing/troubleshooting.md) 用 [!DNL Experience Platform] 一节。

## 收集所需标题的值

要调用API，您必 [!DNL Privacy Service] 须首先收集要在所需标头中使用的访问凭据：

* 授权：承载者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

这包括在Adobe Admin Console获取开 [!DNL Experience Platform] 发人员权限，然后在Adobe开发人员控制台中生成凭据。

### 获得开发人员访问 [!DNL Experience Platform]

要获得开发人员访 [!DNL Platform]问权限，请按照Experience Platform身份验证教 [程中的开始步骤](../../tutorials/authentication.md)。 在进入步骤“在Adobe开发人员控制台中生成访问凭据”后，请返回本教程以生成特定于的凭据 [!DNL Privacy Service]。

### 生成访问凭据

使用Adobe开发人员控制台，您必须生成以下三个访问凭据：

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

您 `{IMS_ORG}` 的 `{API_KEY}` 只需生成一次，以后的API调用中可以重复使用。 但是，您的计 `{ACCESS_TOKEN}` 划是临时的，必须每24小时再生一次。

生成这些值的步骤详见下文。

#### 一次性设置

转到 [Adobe开发人](https://www.adobe.com/go/devs_console_ui) 员控制台并登录您的Adobe ID。 接下来，按照Adobe开发人员控制台文档中 [有关创建空项目](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) 的教程中概述的步骤操作。

创建新项目后，单击“项 **[!UICONTROL 目概述]** ”屏 **[!UICONTROL 幕上的“添加API]** ”。

![](../images/api/getting-started/add-api-button.png)

出 **[!UICONTROL 现添加API]** 屏幕。 在单 **[!UICONTROL 击]** “下一步”之前，从可用API的列表中选择 **[!UICONTROL Privacy ServiceAPI]**。

![](../images/api/getting-started/add-privacy-service-api.png)

将出 **[!UICONTROL 现配置]** API屏幕。 选择“Generate a **[!UICONTROL key pair]**（生成键对）”选 **[!UICONTROL 项，然后单击右]** 下角的“Generate keypair（生成键对）”。

![](../images/api/getting-started/generate-key-pair.png)

将自动生成密钥对，并将包含私钥和公共证书的ZIP文件下载到您的本地计算机（稍后将使用）。 选择 **[!UICONTROL 保存配置的]** API以完成配置。

![](../images/api/getting-started/key-pair-generated.png)

将API添加到项目后，项目页面将重新显示在 _Privacy ServiceAPI概述_ 页面。 从此处向下滚动到服 **[!UICONTROL 务帐户(JWT)]** ，该部分提供对API的所有调用所需的以下访问凭 [!DNL Privacy Service] 据：

* **[!UICONTROL 客户端ID]**:客户端ID是必须 `{API_KEY}` 在x-api-key头中提供的客户端ID。
* **[!UICONTROL 组织ID]**:组织ID是 `{IMS_ORG}` 必须在x-gw-ims-org-id标题中使用的值。

![](../images/api/getting-started/jwt-credentials.png)

#### 每个会话的身份验证

您必须收集的最终必需凭 `{ACCESS_TOKEN}`据是您的，在授权头中使用。 与和的值 `{API_KEY}` 不 `{IMS_ORG}`同，必须每24小时生成一个新令牌才能继续使用 [!DNL Platform] API。

要生成新密 `{ACCESS_TOKEN}`钥，请打开之前下载的私钥，并将其内容粘贴到“生成访问令牌”旁的 **[!UICONTROL 文本框中]** ，然后单 **[!UICONTROL 击“生成令牌”]**。

![](../images/api/getting-started/paste-private-key.png)

将生成新访问令牌，并提供一个按钮以将令牌复制到剪贴板。 此值用于所需的授权头，并且必须以格式提供 `Bearer {ACCESS_TOKEN}`。

![](../images/api/getting-started/generated-access-token.png)

## 后续步骤

现在，您已经了解要使用哪些标头，便可开始调用 [!DNL Privacy Service] API。 隐私工作 [文档](privacy-jobs.md) ，将遍历您可以使用API进行的各种API [!DNL Privacy Service] 调用。 每个示例调用都包括常规API格式、显示所需标头的示例请求和示例响应。

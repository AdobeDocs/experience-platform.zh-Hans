---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Privacy ServiceAPI指南
description: Privacy ServiceAPI允许开发人员创建和管理客户请求，以跨Experience Cloud应用程序访问或删除其个人数据，这符合法律隐私法规。 请阅读本指南，了解如何使用API执行关键操作。
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 0%

---

# [!DNL Privacy Service] API指南

Adobe Experience Platform [!DNL Privacy Service]提供了RESTful API和用户界面，允许您跨Adobe Experience Cloud应用程序管理（访问和删除）数据主体（客户）的个人数据。 [!DNL Privacy Service] 此外，还提供了中央审核和日志记录机制，允许您访问涉及应用程序的作业的状态和 [!DNL Experience Cloud] 结果。

本指南介绍如何使用[!DNL Privacy Service] API。 有关如何使用UI的详细信息，请参阅[Privacy ServiceUI概述](../ui/overview.md)。 有关[!DNL Privacy Service] API中所有可用端点的完整列表，请参阅[ API引用](https://www.adobe.io/experience-platform-apis/references/privacy-service/)。

## 快速入门 {#getting-started}

本指南需要了解以下[!DNL Experience Platform]功能：

* [[!DNL Privacy Service]](../home.md):提供RESTful API和用户界面，允许您跨Adobe Experience Cloud应用程序管理来自数据主体（客户）的访问和删除请求。

以下部分提供了成功调用Privacy ServiceAPI所需了解的其他信息。

### 读取示例API调用

本教程提供了用于演示如何设置请求格式的示例API调用。 这包括路径、所需标头以及格式正确的请求负载。 还提供了API响应中返回的示例JSON。 有关示例API调用文档中使用的惯例的信息，请参阅[!DNL Experience Platform]疑难解答指南中[如何阅读示例API调用](../../landing/troubleshooting.md)一节。

## 收集所需标题的值

要调用[!DNL Privacy Service] API，必须先收集要在所需标头中使用的访问凭据：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

这包括在Adobe Admin Console中获取[!DNL Experience Platform]的开发人员权限，然后在Adobe开发人员控制台中生成凭据。

### 获取对[!DNL Experience Platform]的开发人员访问权限

要获得对[!DNL Platform]的开发人员访问权限，请按照[Experience Platform身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)中的开始步骤操作。 进入“在Adobe开发人员控制台中生成访问凭据”步骤后，请返回本教程以生成特定于[!DNL Privacy Service]的凭据。

### 生成访问凭据

使用Adobe开发人员控制台，您必须生成以下三个访问凭据：

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

您的`{IMS_ORG}`和`{API_KEY}`只需生成一次，即可在以后的API调用中重复使用。 但是，您的`{ACCESS_TOKEN}`是临时的，必须每24小时重新生一次。

有关生成这些值的步骤，请参见下文。

#### 一次性设置

转到[Adobe开发人员控制台](https://www.adobe.com/go/devs_console_ui)并使用Adobe ID登录。 接下来，按照Adobe开发人员控制台文档中[创建空项目](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md)上教程中概述的步骤操作。

创建新项目后，在&#x200B;**[!UICONTROL 项目概述]**&#x200B;屏幕上选择&#x200B;**[!UICONTROL 添加API]**。

![](../images/api/getting-started/add-api-button.png)

出现&#x200B;**[!UICONTROL 添加API]**&#x200B;屏幕。 在选择&#x200B;**[!UICONTROL Next]**&#x200B;之前，从可用API列表中选择&#x200B;**[!UICONTROL Privacy ServiceAPI]**。

![](../images/api/getting-started/add-privacy-service-api.png)

出现&#x200B;**[!UICONTROL 配置API]**&#x200B;屏幕。 选择&#x200B;**[!UICONTROL 生成键对]**&#x200B;选项，然后选择右下角的&#x200B;**[!UICONTROL 生成键对]**&#x200B;选项。

![](../images/api/getting-started/generate-key-pair.png)

密钥对将自动生成，并将包含私钥和公共证书的ZIP文件下载到本地计算机（将在稍后的步骤中使用）。 选择&#x200B;**[!UICONTROL 保存配置的API]**&#x200B;以完成配置。

![](../images/api/getting-started/key-pair-generated.png)

将API添加到项目后，项目页面会重新显示在&#x200B;**Privacy ServiceAPI概述**&#x200B;页面上。 从此处，向下滚动到&#x200B;**[!UICONTROL 服务帐户(JWT)]**&#x200B;部分，该部分提供了对[!DNL Privacy Service] API的所有调用中所需的以下访问凭据：

* **[!UICONTROL 客户端ID]**:客户端ID是必须 `{API_KEY}` 在x-api-key标头中提供的客户端ID。
* **[!UICONTROL 组织ID]**:组织ID是必 `{IMS_ORG}` 须在x-gw-ims-org-id标头中使用的值。

![](../images/api/getting-started/jwt-credentials.png)

#### 每个会话的身份验证

您必须收集的最终必需凭据是`{ACCESS_TOKEN}`，该凭据将用在Authorization标头中。 与`{API_KEY}`和`{IMS_ORG}`的值不同，必须每24小时生成一个新令牌，以继续使用[!DNL Platform] API。

要生成新的`{ACCESS_TOKEN}`，请打开之前下载的私钥并将其内容粘贴到&#x200B;**[!UICONTROL 生成访问令牌]**&#x200B;旁边的文本框中，然后再选择&#x200B;**[!UICONTROL 生成令牌]**。

![](../images/api/getting-started/paste-private-key.png)

将生成新的访问令牌，并提供一个用于将令牌复制到剪贴板的按钮。 此值用于所需的授权标头，且必须以`Bearer {ACCESS_TOKEN}`格式提供。

![](../images/api/getting-started/generated-access-token.png)

## 后续步骤

了解了要使用的标头后，您便可以开始调用[!DNL Privacy Service] API。 有关[隐私作业](privacy-jobs.md)的文档将介绍您可以使用[!DNL Privacy Service] API进行的各种API调用。 每个示例调用都包括常规API格式、显示所需标头的示例请求以及示例响应。

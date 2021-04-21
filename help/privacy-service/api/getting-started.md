---
keywords: Experience Platform；主页；热门主题
solution: Experience Platform
title: Privacy Service API指南
description: Privacy Service API允许开发人员创建和管理客户请求，以便在Experience Cloud应用程序中访问或删除其个人数据，这符合法律隐私法规。 请按照本指南学习如何使用API执行关键操作。
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# [!DNL Privacy Service] API指南

Adobe Experience Platform [!DNL Privacy Service]提供一个RESTful API和用户界面，允许您跨Adobe Experience Cloud应用程序管理（访问和删除）数据主体（客户）的个人数据。 [!DNL Privacy Service] 还提供一个中央审核和日志记录机制，允许您访问涉及应用程序的作业的状态和 [!DNL Experience Cloud] 结果。

本指南介绍如何使用[!DNL Privacy Service] API。 有关如何使用UI的详细信息，请参阅[Privacy ServiceUI概述](../ui/overview.md)。 有关[!DNL Privacy Service] API中所有可用端点的全面列表，请参阅[ API参考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml)。

## 入门指南 {#getting-started}

本指南需要了解以下[!DNL Experience Platform]功能：

* [[!DNL Privacy Service]](../home.md):提供一个RESTful API和用户界面，允许您跨Adobe Experience Cloud应用程序管理来自数据主体（客户）的访问和删除请求。

以下各节提供了成功调用Privacy Service API所需了解的其他信息。

### 读取示例API调用

本教程提供示例API调用，以演示如何设置请求的格式。 这包括路径、必需的标头和格式正确的请求负载。 还提供API响应中返回的示例JSON。 有关示例API调用文档中使用的约定的信息，请参阅[!DNL Experience Platform]疑难解答指南中关于如何读取示例API调用](../../landing/troubleshooting.md)的部分。[

## 收集所需标题的值

要调用[!DNL Privacy Service] API，必须首先收集要在所需标头中使用的访问凭据：

* 授权：承载`{ACCESS_TOKEN}`
* x-api-key:`{API_KEY}`
* x-gw-ims-org-id:`{IMS_ORG}`

这包括获取Adobe Admin Console中[!DNL Experience Platform]的开发人员权限，然后在Adobe开发人员控制台中生成凭据。

### 获得对[!DNL Experience Platform]的开发者访问权限

要获得对[!DNL Platform]的开发人员访问权限，请按照[Experience Platform身份验证教程](https://www.adobe.com/go/platform-api-authentication-en)中的开始步骤进行操作。 当您到达步骤“在Adobe Developer Console中生成访问凭据”后，请返回本教程以生成特定于[!DNL Privacy Service]的凭据。

### 生成访问凭据

使用Adobe Developer Console，您必须生成以下三个访问凭据：

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

您的`{IMS_ORG}`和`{API_KEY}`只需生成一次即可，在将来的API调用中可以重用。 但是，您的`{ACCESS_TOKEN}`是临时的，必须每24小时重新生成一次。

下面详细介绍了生成这些值的步骤。

#### 一次性设置

转到[Adobe Developer Console](https://www.adobe.com/go/devs_console_ui)并使用您的Adobe ID登录。 接下来，按照教程中概述的步骤操作，该教程位于“Adobe开发人员控制台”文档中的[创建空项目](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md)。

创建新项目后，在&#x200B;**[!UICONTROL Project Overview]**&#x200B;屏幕上选择&#x200B;**[!UICONTROL Add API]**。

![](../images/api/getting-started/add-api-button.png)

出现&#x200B;**[!UICONTROL Add an API]**&#x200B;屏幕。 在选择&#x200B;**[!UICONTROL Next]**&#x200B;之前，从可用API的列表中选择&#x200B;**[!UICONTROL Privacy Service API]**。

![](../images/api/getting-started/add-privacy-service-api.png)

出现&#x200B;**[!UICONTROL Configure API]**&#x200B;屏幕。 选择&#x200B;**[!UICONTROL Generate a key pair]**&#x200B;选项，然后选择右下角的&#x200B;**[!UICONTROL Generate keypair]**。

![](../images/api/getting-started/generate-key-pair.png)

将自动生成密钥对，并将包含私钥和公共证书的ZIP文件下载到您的本地计算机（将在后续步骤中使用）。 选择&#x200B;**[!UICONTROL Save configured API]**&#x200B;以完成配置。

![](../images/api/getting-started/key-pair-generated.png)

将API添加到项目后，项目页面将重新显示在&#x200B;**Privacy ServiceAPI概述**&#x200B;页面上。 从此处向下滚动到&#x200B;**[!UICONTROL Service Account (JWT)]**&#x200B;部分，该部分提供对[!DNL Privacy Service] API的所有调用所需的以下访问凭据：

* **[!UICONTROL CLIENT ID]**:必须在x-api-key `{API_KEY}` 标头中提供客户端ID才能使用。
* **[!UICONTROL ORGANIZATION ID]**:组织ID是必须 `{IMS_ORG}` 在x-gw-ims-org-id头中使用的值。

![](../images/api/getting-started/jwt-credentials.png)

#### 每个会话的身份验证

您必须收集的最终必需凭据是`{ACCESS_TOKEN}`，它在“授权”标头中使用。 与`{API_KEY}`和`{IMS_ORG}`的值不同，必须每24小时生成一个新令牌才能继续使用[!DNL Platform] API。

要生成新`{ACCESS_TOKEN}`，请打开之前下载的私钥并将其内容粘贴到&#x200B;**[!UICONTROL Generate access token]**&#x200B;旁边的文本框中，然后选择&#x200B;**[!UICONTROL Generate Token]**。

![](../images/api/getting-started/paste-private-key.png)

将生成新访问令牌，并提供一个按钮以将令牌复制到剪贴板。 此值用于所需的授权头，且格式必须为`Bearer {ACCESS_TOKEN}`。

![](../images/api/getting-started/generated-access-token.png)

## 后续步骤

既然您了解了要使用哪些标头，就可以开始调用[!DNL Privacy Service] API。 有关[隐私作业](privacy-jobs.md)的文档将遍历您可以使用[!DNL Privacy Service] API进行的各种API调用。 每个示例调用都包括常规API格式、显示所需标头的示例请求和示例响应。

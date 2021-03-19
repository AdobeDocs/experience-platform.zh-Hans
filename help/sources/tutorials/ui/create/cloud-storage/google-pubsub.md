---
keywords: Experience Platform；主页；热门主题；Google PubSub;google pubsub
solution: Experience Platform
title: 在UI中创建Google PubSub源连接
topic: 概述
type: 教程
description: 了解如何使用平台用户界面创建Google PubSub源连接器。
translation-type: tm+mt
source-git-commit: b5358ce206888c413035b46fe751520fd9aefb14
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---


# 在UI中创建[!DNL Google PubSub]源连接

>[!NOTE]
>
> [!DNL Google PubSub]连接器处于测试状态。 有关使用测试版标记的连接器的详细信息，请参阅[源概述](../../../../home.md#terms-and-conditions)。

本教程提供了使用平台用户界面创建[!DNL Google PubSub]（以下称“[!DNL PubSub]”）的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [来源](../../../../home.md):Experience Platform允许从各种来源摄取数据，同时使您能够使用平台服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供将单个平台实例分为单独虚拟环境的虚拟沙箱，以帮助开发和发展数字体验应用程序。

如果您已有有效的[!DNL PubSub]连接，则可以跳过此文档的其余部分，继续学习有关[配置数据流](../../dataflow/batch/cloud-storage.md)的教程。

### 收集所需凭据

要将[!DNL PubSub]连接到平台，您必须为以下凭据提供有效值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `projectId` | 验证[!DNL PubSub]所需的项目ID。 |
| `credentials` | 验证[!DNL PubSub]所需的凭据或私钥ID。 |

有关这些值的详细信息，请参阅以下[PubSub身份验证](https://cloud.google.com/pubsub/docs/authentication)文档。 如果您使用基于服务帐户的身份验证，请参阅以下[PubSub指南](https://cloud.google.com/docs/authentication/production#create_service_account)，了解有关如何生成凭据的步骤。

>[!TIP]
>
>如果您使用基于服务帐户的身份验证，请确保您已授予对您的服务帐户的足够用户访问权限，并且在复制和粘贴凭据时，JSON中没有额外的空白。

收集所需凭据后，您可以按照以下步骤将您的[!DNL PubSub]帐户链接到平台。

## 连接您的[!DNL PubSub]帐户

在[平台UI](https://platform.adobe.com)中，从左侧导航栏中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问[!UICONTROL Sources]工作区。 [!UICONTROL Catalog]屏幕显示了可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索栏找到要处理的特定源。

在[!UICONTROL Cloud storage]类别下，选择&#x200B;**[!UICONTROL Google PubSub]**，然后选择&#x200B;**[!UICONTROL Add data]**。

![目录](../../../../images/tutorials/create/google-pubsub/catalog.png)

将显示&#x200B;**[!UICONTROL Connect to Google PubSub]**&#x200B;页。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择要用来创建新数据流的[!DNL PubSub]帐户，然后选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![现有](../../../../images/tutorials/create/google-pubsub/existing.png)

### 新帐户

如果要创建新帐户，请选择&#x200B;**[!UICONTROL New account]**，然后在输入表单上提供名称、可选说明和[!DNL PubSub]身份验证凭据。 完成后，选择&#x200B;**[!UICONTROL Connect to source]**，然后为新连接建立留出一些时间。

![新](../../../../images/tutorials/create/google-pubsub/new.png)

## 后续步骤

通过本教程，您已在[!DNL PubSub]帐户和平台之间创建了连接。 您现在可以继续下一个教程，并[配置一个数据流，以将来自您的云存储的流数据引入Platform](../../dataflow/streaming/cloud-storage-streaming.md)。

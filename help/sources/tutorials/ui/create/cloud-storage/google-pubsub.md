---
keywords: Experience Platform；主页；热门主题；Google PubSub;google Pubsub
solution: Experience Platform
title: 在UI中创建Google PubSub源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Platform用户界面创建Google PubSub源连接器。
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: da7b6fe8f9d274b8e5f27138a1baf8caf63a0c01
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---

# 创建 [!DNL Google PubSub] UI中的源连接

本教程提供了创建 [!DNL Google PubSub] (以下简称“[!DNL PubSub]“”)。

## 快速入门

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [源](../../../../home.md):Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供将单个Platform实例分区为单独虚拟环境的虚拟沙盒，以帮助开发和改进数字体验应用程序。

如果您已经拥有 [!DNL PubSub] 连接时，您可以跳过本文档的其余部分，并继续阅读上的教程 [配置数据流](../../dataflow/batch/cloud-storage.md).

### 收集所需的凭据

为了连接 [!DNL PubSub] 对于Platform，必须为以下凭据提供有效值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `projectId` | 验证所需的项目ID [!DNL PubSub]. |
| `credentials` | 验证所需的凭据或私钥ID [!DNL PubSub]. |

有关这些值的更多信息，请参阅以下内容 [PubSub身份验证](https://cloud.google.com/pubsub/docs/authentication) 文档。 如果您使用基于服务帐户的身份验证，请参阅以下内容 [PubSub指南](https://cloud.google.com/docs/authentication/production#create_service_account) 以了解有关如何生成凭据的步骤。

>[!TIP]
>
>如果您使用基于服务帐户的身份验证，请确保您已向您的服务帐户授予足够的用户访问权限，并且在复制和粘贴凭据时，JSON中没有额外的空格。

收集所需的凭据后，您可以按照以下步骤链接 [!DNL PubSub] 帐户到平台。

## 连接 [!DNL PubSub] 帐户

在 [平台UI](https://platform.adobe.com)，选择 **[!UICONTROL 源]** 从左侧导航栏访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您也可以使用搜索栏找到要使用的特定源。

在 [!UICONTROL 云存储] 类别，选择 **[!UICONTROL Google PubSub]**，然后选择 **[!UICONTROL 添加数据]**.

![目录](../../../../images/tutorials/create/google-pubsub/catalog.png)

的 **[!UICONTROL 连接到Google PubSub]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择 [!DNL PubSub] 创建新数据流的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/google-pubsub/existing.png)

### 新帐户

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后提供名称、可选描述以及 [!DNL PubSub] 输入窗体上的身份验证凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后，再留出一些时间建立新连接。

![新建](../../../../images/tutorials/create/google-pubsub/new.png)

## 后续步骤

通过阅读本教程，您可以在 [!DNL PubSub] 帐户和平台。 您现在可以继续下一个教程和 [配置数据流，以将云存储中的流数据引入平台](../../dataflow/streaming/cloud-storage-streaming.md).

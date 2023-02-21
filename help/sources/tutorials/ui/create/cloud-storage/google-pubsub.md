---
title: 在UI中创建Google PubSub源连接
description: 了解如何使用Platform用户界面创建Google PubSub源连接器。
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: 2b72d384e8edd91c662364dfac31ce4edff79172
workflow-type: tm+mt
source-wordcount: '658'
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
| 项目 ID | 验证所需的项目ID [!DNL PubSub]. |
| 凭据 | 验证所需的凭据或私钥ID [!DNL PubSub]. |
| 主题ID | 的ID [!DNL PubSub] 表示消息馈送的资源。 如果要提供对中特定数据流的访问权限，则必须指定主题ID [!DNL Google PubSub] 来源。 |
| 订阅 ID | 您的 [!DNL PubSub] 订阅。 在 [!DNL PubSub]，则通过订阅已发布消息的主题，可接收消息。 |

有关这些值的更多信息，请参阅以下内容 [PubSub身份验证](https://cloud.google.com/pubsub/docs/authentication) 文档。 如果您使用基于服务帐户的身份验证，请参阅以下内容 [PubSub指南](https://cloud.google.com/docs/authentication/production#create_service_account) 以了解有关如何生成凭据的步骤。

>[!TIP]
>
>如果您使用基于服务帐户的身份验证，请确保您已向您的服务帐户授予足够的用户访问权限，并且在复制和粘贴凭据时，JSON中没有额外的空格。

收集所需的凭据后，您可以按照以下步骤链接 [!DNL PubSub] 帐户到平台。

## 连接 [!DNL PubSub] 帐户

在平台UI中，选择 **[!UICONTROL 源]** 从左侧导航栏访问 [!UICONTROL 源] 工作区。 的 [!UICONTROL 目录] 屏幕会显示您可以创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项找到要处理的特定源。

在 [!UICONTROL 云存储] 类别，选择 **[!UICONTROL Google PubSub]**，然后选择 **[!UICONTROL 添加数据]**.

![Experience PlatformUI上的源目录。](../../../../images/tutorials/create/google-pubsub/catalog.png)

的 **[!UICONTROL 连接到Google PubSub]** 页面。 在此页面上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择 [!DNL PubSub] 创建新数据流的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![源工作流中的现有帐户选择。](../../../../images/tutorials/create/google-pubsub/existing.png)

### 新帐户

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后提供名称、可选描述以及 [!DNL PubSub] 输入窗体上的身份验证凭据。 在此步骤中，您可以通过提供主题ID来定义您的帐户有权访问的数据。 只能访问与该主题ID关联的订阅。

>[!NOTE]
>
>在 [!DNL PubSub] 项目。 如果要添加主体（角色）以有权访问特定主题，则还必须将该主体（角色）添加到该主题的相应订阅中。 有关更多信息，请阅读 [[!DNL PubSub] 访问控制文档](https://cloud.google.com/pubsub/docs/access-control).

完成后，选择 **[!UICONTROL 连接到源]** 然后，再留出一些时间建立新连接。

![源工作流中的新帐户界面。](../../../../images/tutorials/create/google-pubsub/new.png)

## 后续步骤

通过阅读本教程，您可以在 [!DNL PubSub] 帐户和平台。 您现在可以继续下一个教程和 [配置数据流，以将云存储中的流数据引入平台](../../dataflow/streaming/cloud-storage-streaming.md).

---
title: 在UI中创建Google PubSub源连接
description: 了解如何使用Platform用户界面创建Google PubSub源连接器。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: 563ad16304894cab1ee1ead06f63a5b3f65c4ec2
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 1%

---

# 创建 [!DNL Google PubSub] UI中的源连接

>[!IMPORTANT]
>
>此 [!DNL Google PubSub] 源目录中的源可供已购买Real-time Customer Data Platform Ultimate的用户使用。

本教程提供了用于创建 [!DNL Google PubSub] (以下简称“[!DNL PubSub]“)使用Platform用户界面。

## 快速入门

本教程需要对以下Adobe Experience Platform组件有一定的了解：

* [源](../../../../home.md)：Experience Platform允许从各种源摄取数据，同时让您能够使用Platform服务来构建、标记和增强传入数据。
* [沙盒](../../../../../sandboxes/home.md)：Experience Platform提供了可将单个Platform实例划分为多个单独的虚拟环境的虚拟沙箱，以帮助开发和改进数字体验应用程序。

如果您已经拥有有效的 [!DNL PubSub] 连接，您可以跳过本文档的其余部分，并继续阅读以下教程： [配置数据流](../../dataflow/batch/cloud-storage.md).

### 收集所需的凭据

为了连接 [!DNL PubSub] 对于Platform，必须为以下凭据提供有效值：

>[!BEGINTABS]

>[!TAB 基于项目的身份验证]

| 凭据 | 描述 |
| --- | --- |
| 项目 ID | 验证时需要项目ID [!DNL PubSub]. |
| 凭据 | 身份验证所需的凭据 [!DNL PubSub]. 您必须确保从凭据中删除空格后放入完整的JSON文件。 |

>[!TAB 主题和基于订阅的身份验证]

| 凭据 | 描述 |
| --- | --- |
| 凭据 | 身份验证所需的凭据 [!DNL PubSub]. 您必须确保从凭据中删除空格后放入完整的JSON文件。 |
| 主题名称 | 您的名称 [!DNL PubSub] 订阅。 在 [!DNL PubSub]，订阅允许您通过订阅消息已发布到的主题来接收消息。 **注意**：单个 [!DNL PubSub] 订阅只能用于一个数据流。 要创建多个数据流，您必须有多个订阅。 |
| 订阅名称 | 您的名称 [!DNL PubSub] 订阅。 在 [!DNL PubSub]，订阅允许您通过订阅消息已发布到的主题来接收消息。 |

>[!ENDTABS]

有关这些值的更多信息，请参阅以下内容 [PubSub身份验证](https://cloud.google.com/pubsub/docs/authentication) 文档。 如果您使用基于服务帐户的身份验证，请参阅以下内容 [PubSub指南](https://cloud.google.com/docs/authentication/production#create_service_account) 以了解有关如何生成凭据的步骤。

>[!TIP]
>
>如果您使用的是基于服务帐户的身份验证，请确保在复制和粘贴凭据时，您已经向服务帐户授予了足够的用户访问权限，并且JSON中没有额外的空格。

收集所需的凭据后，您可以按照以下步骤链接您的 [!DNL PubSub] Platform帐户。

## 连接您的 [!DNL PubSub] 帐户

在Platform UI中，选择 **[!UICONTROL 源]** 从左侧导航访问 [!UICONTROL 源] 工作区。 此 [!UICONTROL 目录] 屏幕显示了您可以用来创建帐户的各种来源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找您要使用的特定源。

在 [!UICONTROL 云存储] 类别，选择 **[!UICONTROL Google PubSub]**，然后选择 **[!UICONTROL 添加数据]**.

![Experience PlatformUI上的源目录。](../../../../images/tutorials/create/google-pubsub/catalog.png)

此 **[!UICONTROL 连接到Google PubSub]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 现有帐户

要使用现有帐户，请选择 [!DNL PubSub] 要用于创建新数据流的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![源工作流中的现有帐户选择。](../../../../images/tutorials/create/google-pubsub/existing.png)

### 新帐户

>[!TIP]
>
>* 在创建具有受限访问权限的帐户时，您必须至少提供一个主题名称或订阅名称。 如果缺少这两个值，身份验证将失败。
>* 创建后，便无法更改的身份验证类型 [!DNL Google PubSub] 基本连接。 要更改身份验证类型，必须创建新的基本连接。

如果要创建新帐户，请选择 **[!UICONTROL 新帐户]**，然后为新页面提供名称和可选描述 [!DNL PubSub] 帐户。

![源工作流中Google PubSub源的新帐户界面](../../../../images/tutorials/create/google-pubsub/new.png)

此 [!DNL PubSub] 源允许您指定在身份验证期间允许的访问类型。 您可以将帐户设置为使用基于项目的身份验证或基于主题和基于订阅的身份验证。 基于项目的身份验证允许您授予对帐户中根级别项目的访问权限，而基于主题和订阅的身份验证允许您限制对特定项目的访问 [!DNL PubSub] 主题和订阅。

>[!BEGINTABS]

>[!TAB 基于项目的身份验证]

创建具有根访问权限的帐户 [!DNL PubSub] 项目文件夹。 选择 **[!UICONTROL Google PubSub身份验证凭据]** 作为您的身份验证类型，并提供您的项目ID和凭据。 完成后，选择 **[!UICONTROL 连接到源]** 然后等待一段时间以建立新连接。

![已选择根访问权限的Google PubSub源的新帐户接口。](../../../../images/tutorials/create/google-pubsub/root.png)

>[!TAB 主题和基于订阅的身份验证]

创建仅对特定具有受限访问权限的帐户 [!DNL PubSub] 主题和订阅，选择 **[!UICONTROL Google PubSub作用域内的身份验证凭据]** 然后提供您的凭据、主题名称和/或订阅名称。 完成后，选择 **[!UICONTROL 连接到源]** 然后等待一段时间以建立新连接。

![已选择范围访问权限的Google PubSub源的新帐户接口。](../../../../images/tutorials/create/google-pubsub/scoped.png)

>[!ENDTABS]

>[!NOTE]
>
>分配给的主体（角色） [!DNL PubSub] 项目继承于内创建的所有主题和订阅中 [!DNL PubSub] 项目。 如果希望主体（角色）可以访问特定主题，则还必须将该主体（角色）添加到主题的相应订阅中。 欲知更多信息，请参阅 [[!DNL PubSub] 关于访问控制的文档](<https://cloud.google.com/pubsub/docs/access-control>).

## 选择数据

成功的身份验证将带您进入 [!UICONTROL 选择数据] 步骤，您可从中导航 [!DNL PubSub] 数据层次结构并选择要带入Experience Platform的数据。

>[!BEGINTABS]

>[!TAB 基于项目的身份验证]

如果您已通过基于项目的访问权限的身份验证， [!UICONTROL 选择数据] 界面将显示您的项目中具有附加主题的所有订阅。

![具有基于项目的身份验证的源工作流的选择数据步骤。](../../../../images/tutorials/create/google-pubsub/root-folders.png)

>[!TAB 主题和基于订阅的身份验证]

如果您已通过主题和基于订阅的访问权限的身份验证， [!UICONTROL 选择数据] 界面显示可能会因您提供的信息而异。

* 如果只提供主题名称，则界面将显示与所提供主题对应的所有主题订阅对。
* 如果仅提供订阅名称，则界面将显示与提供的订阅名称对应的所有主题订阅对。
* 如果同时提供了主题和预订名称，则界面将显示与两个提供的值对应的主题 — 预订对。

![具有主题和基于订阅的身份验证的源工作流的选择数据步骤。](../../../../images/tutorials/create/google-pubsub/scoped-folders.png)

>[!ENDTABS]

## 后续步骤

在本教程之后，您已创建了 [!DNL PubSub] 帐户和平台。 您现在可以继续下一教程和 [配置数据流以将云存储中的流数据引入平台](../../dataflow/streaming/cloud-storage-streaming.md).

---
keywords: Experience Platform；主页；热门主题；Azure事件中心；事件中心；Azure事件中心
solution: Experience Platform
title: 在UI中创建Azure事件中心源连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Azure事件中心源连接。
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---


# 创建 [!DNL Azure Event Hubs] UI中的源连接

Adobe Experience Platform中的源连接器提供了按计划摄取外部来源数据的功能。 本教程提供了验证 [!DNL Azure Event Hubs] (以下简称“ ”[!DNL Event Hubs]&quot;)源连接器使用 [!DNL Platform] 用户界面。

## 快速入门

本教程需要深入了解Adobe Experience Platform的以下组件：

- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   - [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   - [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的 [!DNL Event Hubs] 连接，您可以跳过本文档的其余部分，并继续阅读以下教程： [配置数据流](../../dataflow/streaming/cloud-storage-streaming.md).

### 收集所需的凭据

为了验证您的 [!DNL Event Hubs] 源连接器中，必须提供以下连接属性的值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `sasKeyName` | 授权规则的名称，也称为SAS密钥名称。 |
| `sasKey` | 的主键 [!DNL Event Hubs] 命名空间。 此 `sasPolicy` 该 `sasKey` 对应的必须具有 `manage` 为以下各项配置的权限 [!DNL Event Hubs] 要填充的列表。 |
| `namespace` | 的命名空间 [!DNL Event Hubs] 您正在访问。 |

有关这些值的更多信息，请参阅 [此 [!DNL Event Hubs] 文档](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## 连接您的 [!DNL Event Hubs] 帐户

收集所需的凭据后，您可以按照以下步骤链接您的 [!DNL Event Hubs] 目标帐户 [!DNL Platform].

登录 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 以访问 **[!UICONTROL 源]** 工作区。 此 **[!UICONTROL 目录]** 选项卡显示了您可以为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找要使用的特定源。

在 **[!UICONTROL 云存储]** 类别，选择 **[!UICONTROL Azure事件中心]**. 如果这是您第一次使用此连接器，请选择 **[!UICONTROL 配置]**. 否则，选择 **[!UICONTROL 添加数据]** 以创建新的事件中枢连接器。

![](../../../../images/tutorials/create/eventhub/catalog.png)

此 **[!UICONTROL 连接到Azure事件中心]** 对话框。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用的是新凭据，请选择 **[!UICONTROL 新建帐户]**. 在出现的输入表单上，提供名称、可选描述以及 [!DNL Event Hubs] 凭据。 完成后，选择 **[!UICONTROL Connect]** 然后留出一些时间来建立新连接。

![](../../../../images/tutorials/create/eventhub/new.png)

### 现有帐户

要连接现有帐户，请选择 [!DNL Event Hubs] 要连接的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![](../../../../images/tutorials/create/eventhub/existing.png)

## 后续步骤

按照本教程，您已连接 [!DNL Event Hubs] 目标帐户 [!DNL Platform]. 您现在可以继续下一教程和 [配置数据流以将数据从云存储引入 [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).

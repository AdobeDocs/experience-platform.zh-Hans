---
keywords: Experience Platform；主页；热门主题；Azure事件集线器；事件集线器；azure事件集线器
solution: Experience Platform
title: 在UI中创建Azure事件集线器源连接
topic: overview
type: Tutorial
description: 了解如何使用Adobe Experience PlatformUI创建Azure事件集线器源连接。
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 1%

---


# 在UI中创建[!DNL Azure Event Hubs]源连接

>[!NOTE]
>
> [!DNL Azure Event Hubs]接头为测试版。 有关使用测试版标签的连接器的详细信息，请参见[源概述](../../../../home.md#terms-and-conditions)。

Adobe Experience Platform的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用[!DNL Platform]用户界面验证[!DNL Azure Event Hubs]（以下称“[!DNL Event Hubs]”）源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   - [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有有效的[!DNL Event Hubs]连接，您可以跳过此文档的其余部分，继续学习有关配置数据流](../../dataflow/streaming/cloud-storage-streaming.md)的教程。[

### 收集所需的凭据

要验证[!DNL Event Hubs]源连接器，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `sasKeyName` | 授权规则的名称，也称为SAS密钥名称。 |
| `sasKey` | 生成的共享访问签名。 |
| `namespace` | 您访问的[!DNL Event Hubs]的命名空间。 |

有关这些值的详细信息，请参阅[this [!DNL Event Hubs] 文档](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。

## 连接您的[!DNL Event Hubs]帐户

收集所需凭据后，您可以按照以下步骤将[!DNL Event Hubs]帐户链接到[!DNL Platform]。

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL 源]**&#x200B;以访问&#x200B;**[!UICONTROL 源]**&#x200B;工作区。 **[!UICONTROL 目录]**&#x200B;选项卡显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在&#x200B;**[!UICONTROL 云存储]**&#x200B;类别下，选择&#x200B;**[!UICONTROL Azure事件集线器]**。 如果这是您首次使用此连接器，请选择&#x200B;**[!UICONTROL 配置]**。 否则，选择&#x200B;**[!UICONTROL 添加数据]**&#x200B;以创建新的事件集线器连接器。

![](../../../../images/tutorials/create/eventhub/catalog.png)

将显示&#x200B;**[!UICONTROL 连接到Azure事件集线器]**&#x200B;对话框。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择&#x200B;**[!UICONTROL 新建帐户]**。 在显示的输入表单上，提供名称、可选说明和[!DNL Event Hubs]凭据。 完成后，选择&#x200B;**[!UICONTROL Connect]**，然后为新连接建立留出一些时间。

![](../../../../images/tutorials/create/eventhub/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的[!DNL Event Hubs]帐户，然后选择&#x200B;**[!UICONTROL 下一步]**&#x200B;以继续。

![](../../../../images/tutorials/create/eventhub/existing.png)

## 后续步骤

按照本教程，您已将[!DNL Event Hubs]帐户连接到[!DNL Platform]。 现在，您可以继续阅读下一个教程，并[配置数据流，将数据从您的云存储引入 [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md)。
---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Azure事件集线器源连接器
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 1%

---


# 在UI [!DNL Azure Event Hubs] 中创建源连接器

>[!NOTE]
> 连接 [!DNL Azure Event Hubs] 器为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用用户 [!DNL Azure Event Hubs] 界面验证源连接器([!DNL Event Hubs]以下称“”) [!DNL Platform] 的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

- [体验数据模型(XDM)系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   - [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [实时客户用户档案](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有 [!DNL Event Hubs] 帐户，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/streaming/cloud-storage.md)。

### 收集所需的凭据

要验证源连接器的 [!DNL Event Hubs] 身份，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `sasKeyName` | 授权规则的名称，也称为SAS密钥名称。 |
| `sasKey` | 生成的共享访问签名。 |
| `namespace` | 您访问的 [!DNL Event Hubs] 命名空间。 |

有关这些值的详细信息，请参阅 [此事件中心文档](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。

## 连接帐 [!DNL Event Hubs] 户

收集所需凭据后，您可以按照以下步骤将帐户链 [!DNL Event Hubs] 接到 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 *“源”以访问* “源”工作区。 “目 *[!UICONTROL 录]* ”选项卡显示可连接到的各种源 [!DNL Platform]。 每个来源显示与其关联的现有帐户数。

在“云 *[!UICONTROL 存储]* ”类别下，选 **[!UICONTROL 择Azure事件集线器]** ，然后 **[!UICONTROL 选择添加数据]** ，以创建新的事件集线器连接器。

![](../../../../images/tutorials/create/eventhub/catalog.png)

将显 *[!UICONTROL 示“连接到Azure事件集线器]* ”对话框。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供名称、可选说明和您的事件中心凭据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新连接。

![](../../../../images/tutorials/create/eventhub/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的事件中心帐户，然后选择下 **[!UICONTROL 一步]** 以继续。

![](../../../../images/tutorials/create/eventhub/existing.png)

## 后续步骤

通过本教程，您已将事件中心帐户连接到 [!DNL Platform]。 您现在可以继续阅读下一个教程 [并配置数据流，将数据从云存储引入平台](../../dataflow/streaming/cloud-storage.md)。
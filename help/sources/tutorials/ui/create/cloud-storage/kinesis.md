---
keywords: Experience Platform;home;popular topics;Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: 在UI中创建AmazonKinesis源连接器
topic: overview
type: Tutorial
description: 本教程提供了使用平台用户界面验证AmazonKinesis(以下简称“Kinesis”)源连接器的步骤。
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---


# 在UI [!DNL Amazon Kinesis] 中创建源连接器

>[!NOTE]
>
>连接 [!DNL Amazon Kinesis] 器为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用用户 [!DNL Amazon Kinesis] 界面验证源连接 [!DNL "Kinesis"]器（以下简称）的 [!DNL Platform] 步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   - [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果已有有效的连 [!DNL Kinesis] 接，您可以跳过此文档的其余部分，继续学习配置 [数据流的教程](../../dataflow/streaming/cloud-storage-streaming.md)。

### 收集所需的凭据

要验证源连接器的 [!DNL Kinesis] 身份，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `accessKeyId` | 您的帐户的访问密钥 [!DNL Kinesis] ID。 |
| `Secret access key` | 帐户的秘密访问 [!DNL Kinesis] 密钥。 |
| `region` | 您的AWS服务器所在的区域。 |

有关这些值的详细信息，请参 [ [!DNL Kinesis] 阅本文档](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html)。

## 连接帐 [!DNL Kinesis] 户

收集所需凭据后，您可以按照以下步骤将帐户链 [!DNL Kinesis] 接到 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 **[!UICONTROL “源”以访问]** “源”工作区。 “ **[!UICONTROL 目录]** ”屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在云存储 **[!UICONTROL 类别下]** ，选择 **[!UICONTROL AmazonKinesis]**。 如果这是您首次使用此连接器，请选择“ **[!UICONTROL 配置]**”。 否则，选择 **[!UICONTROL 添加数据]** ，以创建新连 [!DNL Kinesis] 接器。

![](../../../../images/tutorials/create/kinesis/catalog.png)

出现 **[!UICONTROL “连接到Amazon·Kinesis]** ”对话框。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供名称、可选说明和凭 [!DNL Kinesis] 据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新连接。

![](../../../../images/tutorials/create/kinesis/new.png)

### 现有帐户

要连接现有帐户，请选 [!DNL Kinesis] 择要连接的帐户，然后选择 **[!UICONTROL 下一]** 步以继续。

![](../../../../images/tutorials/create/kinesis/existing.png)

## 后续步骤

按照本教程，您已将帐户 [!DNL Kinesis] 连接到 [!DNL Platform]。 您现在可以继续阅读下一个教程 [并配置数据流，将数据从云存储引入 [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md)。
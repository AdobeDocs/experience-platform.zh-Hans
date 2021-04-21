---
keywords: Experience Platform；主页；热门主题；Amazon Kinesis;amazon kinesis;Kinesis;kinesis
solution: Experience Platform
title: 在UI中创建Amazon Kinesis源连接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Amazon Kinesis UI创建Adobe Experience Platform源连接。
exl-id: 4152e48b-bec7-4b05-a172-eea71c9d9880
translation-type: tm+mt
source-git-commit: d6f1521470b8dc630060584189690545c724de6b
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 1%

---

# 在UI中创建[!DNL Amazon Kinesis]源连接

Adobe Experience Platform中的源连接器提供按计划收集外部源数据的能力。 本教程提供了使用[!DNL Platform]用户界面验证[!DNL Amazon Kinesis]（以下称[!DNL "Kinesis"]）源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

- [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   - [模式合成的基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建基块，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。

如果您已有有效的[!DNL Kinesis]连接，则可以跳过此文档的其余部分，继续学习有关[配置数据流](../../dataflow/streaming/cloud-storage-streaming.md)的教程。

### 收集所需凭据

要验证[!DNL Kinesis]源连接器，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `accessKeyId` | [!DNL Kinesis]帐户的访问密钥ID。 |
| `Secret access key` | [!DNL Kinesis]帐户的密钥访问密钥。 |
| `region` | 您的AWS服务器的区域。 |

有关这些值的详细信息，请参阅[this [!DNL Kinesis] 文档](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html)。

## 连接您的[!DNL Kinesis]帐户

收集所需凭据后，您可以按照以下步骤将您的[!DNL Kinesis]帐户链接到[!DNL Platform]。

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问&#x200B;**[!UICONTROL Sources]**&#x200B;工作区。 **[!UICONTROL Catalog]**&#x200B;屏幕显示了可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在&#x200B;**[!UICONTROL Cloud Storage]**&#x200B;类别下，选择&#x200B;**[!UICONTROL Amazon Kinesis]**。 如果这是您首次使用此连接器，请选择&#x200B;**[!UICONTROL Configure]**。 否则，选择&#x200B;**[!UICONTROL Add data]**&#x200B;以创建新[!DNL Kinesis]连接器。

![](../../../../images/tutorials/create/kinesis/catalog.png)

出现&#x200B;**[!UICONTROL Connect to Amazon Kinesis]**&#x200B;对话框。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择&#x200B;**[!UICONTROL New Account]**。 在显示的输入表单上，提供名称、可选说明和[!DNL Kinesis]凭据。 完成后，选择&#x200B;**[!UICONTROL Connect]**，然后为新连接建立留出一些时间。

![](../../../../images/tutorials/create/kinesis/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的[!DNL Kinesis]帐户，然后选择&#x200B;**[!UICONTROL Next]**&#x200B;以继续。

![](../../../../images/tutorials/create/kinesis/existing.png)

## 后续步骤

按照本教程，您已将[!DNL Kinesis]帐户连接到[!DNL Platform]。 现在，您可以继续阅读下一个教程，并[配置一个数据流，以将来自您的云存储的数据引入 [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md)。

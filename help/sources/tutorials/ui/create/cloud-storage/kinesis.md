---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Amazon Kinesis源连接器
topic: overview
translation-type: tm+mt
source-git-commit: 1eb6883ec9b78e5d4398bb762bba05a61c0f8308
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---


# 在UI中创建Amazon Kinesis源连接器

>[!NOTE]
> Amazon Kinesis连接器为测试版。 功能和文档可能会发生更改。

Adobe Experience Platform中的源连接器提供按计划收集外部源数据的能力。 本教程提供使用平台用户界面验证Amazon Kinesis（以下称“Kinesis”）源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

- [体验数据模型(XDM)系统](../../../../../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
   - [模式合成基础](../../../../../xdm/schema/composition.md): 了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md): 了解如何使用模式编辑器UI创建自定义模式。
- [实时客户用户档案](../../../../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有Kinesis帐户，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/streaming/cloud-storage.md)。

### 收集所需的凭据

要验证Kinesis源连接器，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `accessKeyId` | 您的Kinesis帐户的访问密钥ID。 |
| `Secret access key` | Kinesis帐户的机密访问密钥。 |
| `region` | 您的AWS服务器所在的区域。 |

有关这些值的详细信息，请参 [阅此Kinesis文档](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html)。

## 连接您的Kinesis帐户

收集所需凭据后，您可以按照以下步骤将Kinesis帐户链接到平台。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **侧导航栏** 中 *选择“源* ”以访问“源”工作区。 “目 *录* ”选项卡显示可连接到平台的各种源。 每个来源显示与其关联的现有帐户数。

在云 *存储* 类别下，选 **择Amazon Kinesis** ，然 **** 后单击+图标(+)以创建新的Kinesis连接器。

![](../../../../images/tutorials/create/eventhub/catalog.png)

将显 *示“连接到Amazon* Kinesis”对话框。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **新帐户**”。 在显示的输入表单上，提供名称、可选说明和您的Kinesis凭据。 完成后，选 **择** Connect，然后允许一段时间建立新连接。

![](../../../../images/tutorials/create/eventhub/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的Kinesis帐户，然后选择“下 **一步** ”继续。

![](../../../../images/tutorials/create/eventhub/existing.png)

## 后续步骤

通过遵循本教程，您已将Kinesis帐户连接到平台。 您现在可以继续阅读下一个教程 [并配置数据流，将数据从云存储引入平台](../../dataflow/streaming/cloud-storage.md)。
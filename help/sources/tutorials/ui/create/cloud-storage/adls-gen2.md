---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Azure Data Lake存储Gen2源连接器
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# 在UI中创建Azure Data Lake存储Gen2源连接器

Adobe Experience Platform中的源连接器提供了按计划收集外部来源数据的能力。 本教程提供了使用平台用户界面验证Azure数据湖存储Gen2（以下简称“ADLS Gen2”）源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

- [体验数据模型(XDM)系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   - [模式合成的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [实时客户用户档案](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。

如果您已经有ADLS Gen2基本连接，您可以跳过本文档的其余部分并继续学习配置数据 [流的教程](../../dataflow/cloud-storage.md)。

### 收集所需的凭据

要验证ADLS Gen2源连接器的身份，必须为以下连接属性提供值：

| 凭证 | 描述 |
| ---------- | ----------- |
| `url` | ADLS Gen2的端点。 |
| `servicePrincipalId` | 应用程序的客户端ID。 |
| `servicePrincipalKey` | 应用程序的密钥。 |
| `tenant` | 包含您的应用程序的租户信息。 |

有关这些值的详细信息，请参 [阅此ADLS Gen2文档](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)。

## 连接您的ADLS Gen2帐户

收集所需凭据后，您可以按照以下步骤创建新的入站基本连接，以将ADLS Gen2帐户关联到平台。

登录到 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然后从左侧导航栏中选 **择“源** ”以访问“源 ** ”工作区。 “目 *录* ”选项卡显示用于创建入站基本连接的各种源。 每个源显示与它们关联的现有基本连接的数量。

在“ *云存储* ”类别下，选择 **Azure Data Lake Gen2** ，在屏幕右侧显示一个信息栏。 信息栏提供所选源的简短说明以及与源视图及其文档连接的选项。 要创建新的入站基本连接，请单击“ **Connect源”**。

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

将显 *示“连接到Azure数据湖Gen2* ”对话框。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用的是新凭据，请选择“ **新帐户”**。 在显示的输入表单上，为基本连接提供名称、可选说明和您的ADLS Gen2凭据。 完成后，选择 **Connect** ，然后为新的基本连接建立留出一些时间。

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### 现有帐户

要连接现有帐户，请选择要连接的ADLS Gen2帐户，然后选择“下 **一步** ”继续。

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## 后续步骤

通过本教程，您已经与ADLS Gen2帐户建立了基本连接。 您现在可以继续阅读下一个教程并配 [置数据流，以将数据从您的云存储引入平台](../../dataflow/cloud-storage.md)。
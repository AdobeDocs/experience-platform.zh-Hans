---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Azure表存储源连接器
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# 在UI中创建Azure表存储源连接器

Adobe Experience Platform中的源连接器提供了按计划收集外部来源数据的能力。 本教程提供了使用平台用户界面创建Azure表存储（以下简称“ATS”）源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [体验数据模型(XDM)系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [实时客户用户档案](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。

如果您已经有有效的ATS连接，您可以跳过本文档的其余部分，继续学习配置数据 [流的教程](../../dataflow/databases.md)。

### 收集所需的凭据

要在平台上访问您的ATS帐户，您必须提供以下值：

| 凭证 | 描述 |
| ---------- | ----------- |
| `connectionString` | 连接到Azure表存储实例的连接字符串。 |

有关快速入门的详细信息，请参 [阅此Azure表存储文档](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction)。

## 连接您的Azure表存储帐户

收集所需凭据后，您可以按照以下步骤创建新的ATS帐户以连接到平台。

登录到 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然后从左侧导航栏中选 **择“源** ”以访问“源 ** ”工作区。 “目 *录* ”屏幕显示可为其创建入站帐户的各种源，每个源显示与它们关联的现有帐户和数据集流的数量。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您也可以使用搜索选项找到要处理的特定源。

在“数 *据库* ”类别下，选 **择“Azure表存储”** ，在屏幕右侧显示一个信息栏。 信息栏提供所选源的简短说明以及与源或视图其文档的连接选项。 要创建新的入站连接，请选择“ **Connect源”**。

![目录](../../../../images/tutorials/create/ats/catalog.png)

将显 *示“连接到Azure表存储* ”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **新帐户”**。 在显示的输入表单上，为连接提供名称、可选说明和ATS凭据。 完成后，选择 **Connect** ，然后为新帐户建立留出一些时间。

![connect](../../../../images/tutorials/create/ats/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的ATS帐户，然后选择“下一 **步** ”继续。

![现有](../../../../images/tutorials/create/ats/existing.png)

## 后续步骤

通过本教程，您已经建立了与ATS帐户的连接。 您现在可以继续阅读下一个教程，并 [配置一个数据流以将数据引入平台](../../dataflow/databases.md)。
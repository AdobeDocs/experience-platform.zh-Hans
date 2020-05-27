---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Azure Blob或Amazon S3源连接器
topic: overview
translation-type: tm+mt
source-git-commit: 0a2247a9267d4da481b3f3a5dfddf45d49016e61
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 1%

---


# 在UI中创建Azure Blob或Amazon S3源连接器

Adobe Experience Platform中的源连接器提供按计划收集外部源数据的能力。 本教程提供了使用平台用户界面创建Azure Blob（以下称为“Blob”）或Amazon S3（下称为“S3”）源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

- [体验数据模型(XDM)系统](../../../../../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
   - [模式合成基础](../../../../../xdm/schema/composition.md): 了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md): 了解如何使用模式编辑器UI创建自定义模式。
- [实时客户用户档案](../../../../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有Blob或S3基本连接，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/batch/cloud-storage.md)。

### 支持的文件格式

Experience Platform支持从外部存储摄取的以下文件格式：

- 分隔符分隔值(DSV): 目前，对DSV格式化数据文件的支持仅限于逗号分隔的值。 DSV格式化文件中字段标题的值只能由字母数字字符和下划线组成。 今后将提供对一般DSV文件的支持。
- JavaScript对象表示法(JSON): JSON格式数据文件必须符合XDM。
- Apache Parke: 必须符合XDM规范，但必须符合XDM格式。

### 收集所需的凭据

要在平台上访问您的Blob存储，您必须为以下凭据提供有效值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 访问Blob存储中的数据所需的连接字符串。 Blob连接字符串模式为： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

有关快速入门的详细信息，请 [访问此Azure Blob文档](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)。

同样，在平台上访问S3存储段需要您为以下凭据提供有效值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `s3AccessKey` | S3存储的访问密钥ID。 |
| `s3SecretKey` | S3存储的密钥ID。 |

有关入门的更多信息，请访 [问此AWS文档](https://aws.amazon.com/blogs/security/wheres-my-secret-access-key/)。

## 连接您的Blob或S3帐户

云存储凭据准备就绪后，您可以按照以下步骤创建新的入站基础连接，以将您的Blob或S3帐户链接到平台。

登录到 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然后从左 **侧导航栏** 中选择“源”以访问源工作区。 “目 *录* ”屏幕显示可为其创建入站基本连接的各种源，每个源显示与它们关联的现有基本连接数。

在云 *存储* 类别下，选 **择Azure Blob存储** 或 **Amazon S3** ，在屏幕右侧显示一个信息栏。 信息栏提供所选源的简短说明以及视图其文档或与源连接的选项。 要创建新的入站基本连接，请单击“ **连接源”**。

![](../../../../images/tutorials/create/s3/s3_sources_catalog.png)

在输入表单上，为基本连接提供名称、可选说明以及Blob或S3凭据。 最后，单 **击** “连接”，然后允许一些时间建立新的基本连接。

![](../../../../images/tutorials/create/s3/s3_credentials.png)

## 后续步骤

通过本教程，您已建立到Azure Blob或Amazon S3帐户的基本连接。 您现在可以继续阅读下一个教程， [并配置数据流以将数据引入平台](../../dataflow/batch/cloud-storage.md)。
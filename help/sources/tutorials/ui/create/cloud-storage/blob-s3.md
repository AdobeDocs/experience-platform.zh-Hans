---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Azure Blob或Amazon S3源连接器
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# 在UI中创建Azure Blob或Amazon S3源连接器

Adobe Experience Platform中的源连接器提供了按计划收集外部来源数据的能力。 本教程提供了使用平台用户界面创建Azure Blob（以下称为“Blob”）或Amazon S3（以下称为“S3”）源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [体验数据模型(XDM)系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [实时客户用户档案](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。

如果您已经有Blob或S3基本连接，则可以跳过本文档的其余部分，继续学习有关配置数据 [流的教程](../../dataflow/cloud-storage.md)。

### 支持的文件格式

Experience Platform支持以下从外部存储摄取的文件格式：

* 分隔符分隔值(DSV):目前，对DSV格式化数据文件的支持仅限于逗号分隔的值。 DSV格式文件中字段标题的值只能由字母数字字符和下划线组成。 将来将提供对一般DSV文件的支持。
* JavaScript对象表示法(JSON):JSON格式的数据文件必须符合XDM规范。
* Apache Parce:必须符合XDM规范，但必须符合镶木格式的数据文件。

### 收集所需的凭据

要访问平台上的Blob存储，您必须提供有效的 **Azure存储连接字符串**。 您可以进一步了解连接字符串，包括通过此Microsoft Azure文档获 <a href="https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string" target="_blank">取这些字符串的方法</a>。

同样，在平台上访问S3存储段需要您提供 **S3访问密钥****和S3密钥**。 有关详细信息，请参 <a href="https://aws.amazon.com/blogs/security/wheres-my-secret-access-key/" target="_blank">阅此AWS文档</a>。

## 连接您的Blob或S3帐户

在您的云存储凭据准备就绪后，您可以按照以下步骤创建新的入站基本连接，以将您的Blob或S3帐户关联到平台。

登录到 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然后从左侧导航栏 **中选择源** ，以访问源工作区。 “目 *录* ”屏幕显示各种来源，您可以为其创建入站基本连接，每个来源显示与这些来源关联的现有基本连接的数量。

在“ *云存储* ”类别下，选择“ **Azure Blob存储** ”或“ **Amazon S3** ”，在屏幕右侧显示一个信息栏。 信息栏提供所选源的简短说明以及视图其文档或与源连接的选项。 要创建新的入站基本连接，请单击“ **Connect源”**。

![](../../../../images/tutorials/create/s3/s3_sources_catalog.png)

在输入表单上，为基本连接提供名称、可选说明以及Blob或S3凭据。 最后，单击 **Connect** ，然后为建立新的基本连接留出一些时间。

![](../../../../images/tutorials/create/s3/s3_credentials.png)

## 后续步骤

通过本教程，您已经建立了与Azure Blob或Amazon S3帐户的基本连接。 您现在可以继续阅读下一个教程，并 [配置一个数据流以将数据引入平台](../../dataflow/cloud-storage.md)。
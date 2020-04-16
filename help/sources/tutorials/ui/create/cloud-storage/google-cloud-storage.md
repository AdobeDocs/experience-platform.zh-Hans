---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Google Cloud存储源连接器
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# 在UI中创建Google Cloud存储源连接器

Adobe Experience Platform中的源连接器提供了按计划收集外部来源数据的能力。 本教程提供了使用平台用户界面创建Google Cloud存储（以下简称“GCS”）源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [体验数据模型(XDM)系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [实时客户用户档案](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。

如果您已经有GCS基本连接，则可以跳过本文档的其余部分，继续学习有关配置数 [据流的教程](../../dataflow/cloud-storage.md)。

### 支持的文件格式

Experience Platform支持以下从外部存储摄取的文件格式：

* 分隔符分隔值(DSV):目前，对DSV格式化数据文件的支持仅限于逗号分隔的值。 DSV格式文件中字段标题的值只能由字母数字字符和下划线组成。 将来将提供对一般DSV文件的支持。
* JavaScript对象表示法(JSON):JSON格式的数据文件必须符合XDM规范。
* Apache Parce:必须符合XDM规范，但必须符合镶木格式的数据文件。

### 收集所需的凭据

要在平台上访问GCS数据，您必须提供有效的GCS **访问密钥ID** 和 **机密**。 您可以阅读Google Cloud的服务器到服务器身份验证指 <a href="https://cloud.google.com/docs/authentication/production" target="_blank">南，进一步了解如何获取这些值</a> 。

## 连接您的GCS帐户

收集所需凭据后，您可以按照以下步骤创建新的入站基本连接，以将GCS帐户关联到平台。

登录到 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然后从左侧导航栏中选 **择“源** ”以访问“源 ** ”工作区。 “目 *录* ”屏幕显示各种来源，您可以为其创建入站基本连接，每个来源显示与这些来源关联的现有基本连接的数量。

在“ *云存储* ”类别下，选择 **Google Cloud存储** ，以在屏幕右侧显示一个信息栏。 信息栏提供所选源的简短说明以及与源视图及其文档连接或与源连接的选项。 要创建新的入站基本连接，请单击“ **Connect源”**。

![](../../../../images/tutorials/create/google-cloud-storage/sources-catalog.png)

将显 _示“连接到Google Cloud存储_ ”对话框。 在输入表单中，为基本连接提供名称、可选说明和GCS凭据。 完成后，单击 **Connect** ，然后为建立新的基本连接留出一些时间。

![](../../../../images/tutorials/create/google-cloud-storage/gcs-credentials.png)

建立基本连接后，您可以继续下一节，并配置数据流以将数据引入平台。

## 后续步骤

通过本教程，您已经与GCS帐户建立了基本连接。 您现在可以继续阅读下一个教程，并 [配置一个数据流以将数据引入平台](../../dataflow/cloud-storage.md)。
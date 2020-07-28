---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Google Cloud存储源连接器
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 1%

---


# 在UI [!DNL Google Cloud Storage] 中创建源连接器

Adobe Experience Platform中的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用用 [!DNL Google Cloud Storage] 户界面创建（下称“GCS”）源连接器 [!DNL Platform] 的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [体验数据模型(XDM)系统](../../../../../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md): 了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md): 了解如何使用模式编辑器UI创建自定义模式。
* [实时客户用户档案](../../../../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果已有GCS基础连接，您可以跳过本文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/batch/cloud-storage.md)。

### 支持的文件格式

[!DNL Experience Platform] 支持从外部存储摄取的以下文件格式：

* 分隔符分隔值(DSV): 目前，对DSV格式化数据文件的支持仅限于逗号分隔的值。 DSV格式化文件中字段标题的值只能由字母数字字符和下划线组成。 今后将提供对一般DSV文件的支持。
* JavaScript对象表示法(JSON): JSON格式数据文件必须符合XDM。
* Apache Parke: 必须符合XDM规范，但必须符合XDM格式。

### 收集所需的凭据

要访问上的GCS数据， [!DNL Platform]必须提供有效的GCS **访问密钥ID** 和 **机密**。 您可以通过阅读的服务器到服务器身份验证指 <a href="https://cloud.google.com/docs/authentication/production" target="_blank">南进一步了解如何获取这些值</a>[!DNL Google Cloud]。

## 连接您的GCS帐户

收集所需凭据后，您可以按照以下步骤创建要连接的新GCS帐户 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选 *[!UICONTROL 择源]* ，以访问源工作区。 “ *[!UICONTROL 目录]* ”屏幕显示可为其创建入站帐户的各种源，每个源显示与它们关联的现有帐户和数据流的数量。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“数 *[!UICONTROL 据库]* ”类别 **[!UICONTROL 下]** ，选择“Google Cloud **存储”** ，单击“+”图标(+)以创建新的GCS连接器。

![目录](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

此时 *[!UICONTROL 将显示“连接到Google Cloud存储]* ”页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供名称、可选说明和GCS凭据的连接。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新帐户。

![connect](../../../../images/tutorials/create/google-cloud-storage/connect.png)

### 现有帐户

要连接现有帐户，请选择要连接的GCS帐户，然后选择“下 **[!UICONTROL 一步]** ”继续。

![现有](../../../../images/tutorials/create/google-cloud-storage/existing.png)

## 后续步骤

按照本教程，您已建立了与GCS帐户的连接。 您现在可以继续阅读下一个教程 [并配置数据流，将数据从云存储引入平台](../../dataflow/batch/cloud-storage.md)。
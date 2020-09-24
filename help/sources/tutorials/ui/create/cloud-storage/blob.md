---
keywords: Experience Platform;home;popular topics;Azure Blob;azure blob;Azure blob connector
solution: Experience Platform
title: 在UI中创建Azure Blob源连接器
topic: overview
type: Tutorial
description: 本教程提供了使用平台用户界面创建Azure Blob（以下称“Blob”）的步骤。
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---


# 在UI [!DNL Azure Blob] 中创建源连接器

Adobe Experience Platform的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用用 [!DNL Azure Blob] 户界面创建([!DNL Blob]以下称“ [!DNL Platform] ”)的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

- [[!DNL Experience Data Model] (XDM)系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   - [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL实时客户用户档案]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果已有有效的连 [!DNL Blob] 接，您可以跳过此文档的其余部分，继续学习配置 [数据流的教程](../../dataflow/batch/cloud-storage.md)。

### 支持的文件格式

[!DNL Experience Platform] 支持从外部存储摄取的以下文件格式：

- 分隔符分隔值(DSV):目前，对DSV格式化数据文件的支持仅限于逗号分隔的值。 DSV格式化文件中字段标题的值只能由字母数字字符和下划线组成。 今后将提供对一般DSV文件的支持。
- JavaScript对象表示法(JSON):JSON格式数据文件必须符合XDM。
- Apache Parke:必须符合XDM规范，但必须符合XDM格式。

### 收集所需的凭据

要访问您的 [!DNL Blob] 存储, [!DNL Platform]您必须为以下凭据提供有效值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 访问Blob存储中的数据所需的连接字符串。 连接 [!DNL Blob] 字符串模式为： `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

有关快速入门的详细信息，请访 [ [!DNL Azure Blob] 问此文档](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string)。

## 连接您的Blob帐户

收集所需凭据后，您可以按照以下步骤将帐户链 [!DNL Blob] 接到 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 **[!UICONTROL “源”以访问]** “源”工作区。 “ **[!UICONTROL 目录]** ”屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“数 **[!UICONTROL 据库]** ”类别下， **[!UICONTROL 选择Azure Blob存储]**。 如果这是您首次使用此连接器，请选择“ **[!UICONTROL 配置]**”。 否则，选择 **[!UICONTROL 添加数据]** ，以创建新连 [!DNL Blob]接器。

![目录](../../../../images/tutorials/create/blob/catalog.png)

将显 **[!UICONTROL 示“连接到Azure Blob存储]** ”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供名称、可选说明和凭 [!DNL Blob] 据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新连接。

![connect](../../../../images/tutorials/create/blob/new.png)

### 现有帐户

要连接现有帐户，请选 [!DNL Blob] 择要连接的帐户，然后选择 **[!UICONTROL 下一]** 步以继续。

![现有](../../../../images/tutorials/create/blob/existing.png)

## 后续步骤和其他资源

按照本教程，您已建立了与帐户的 [!DNL Blob] 连接。 您现在可以继续阅读下一个教程 [并配置数据流，将数据从云存储引入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md)。
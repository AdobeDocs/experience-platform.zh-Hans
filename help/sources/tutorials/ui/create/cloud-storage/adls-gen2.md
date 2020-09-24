---
keywords: Experience Platform;home;popular topics;Azure Data Lake Storage Gen2;ADLS Gen2;adls gen2;adls connector
solution: Experience Platform
title: 在UI中创建Azure Data Lake存储Gen2源连接器
topic: overview
type: Tutorial
description: 本教程提供了使用平台用户界面验证Azure存储湖数据源Gen2（以下简称“ADLS Gen2”）源连接器的步骤。
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---


# 在UI [!DNL Azure Data Lake Storage Gen2] 中创建源连接器

Adobe Experience Platform的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用用户 [!DNL Azure Data Lake Storage Gen2] 界面验证源连接器([!DNL ADLS Gen2]以下称“”) [!DNL Platform] 的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

- [[!DNL Experience Data Model] (XDM)系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   - [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [[!DNL实时客户用户档案]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有有效的ADLS Gen2连接，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/batch/cloud-storage.md)。

### 收集所需的凭据

要验证源连接器的 [!DNL ADLS Gen2] 身份，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `url` | 的端点 [!DNL ADLS Gen2]。 |
| `servicePrincipalId` | 应用程序的客户端ID。 |
| `servicePrincipalKey` | 应用程序的密钥。 |
| `tenant` | 包含您的应用程序的租户信息。 |

有关这些值的详细信息，请参 [ [!DNL ADLS Gen2] 阅本文档](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)。

## 连接帐 [!DNL ADLS Gen2] 户

收集所需凭据后，您可以按照以下步骤将帐户链 [!DNL ADLS Gen2] 接到以连接 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 **[!UICONTROL “源”以访问]** “源”工作区。 “ **[!UICONTROL 目录]** ”屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“数 **[!UICONTROL 据库]** ”类别 **[!UICONTROL 下]**，选择Azure Data Lake Gen2。 如果这是您首次使用此连接器，请选择“ **[!UICONTROL 配置]**”。 否则，选 **[!UICONTROL 择“添加]** 数据”以创建新的ADLS Gen2连接器。

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

出 **[!UICONTROL 现“连接到Azure数据湖Gen2]** ”对话框。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供名称、可选说明和凭 [!DNL ADLS Gen2] 据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新连接。

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### 现有帐户

要连接现有帐户，请选 [!DNL ADLS Gen2] 择要连接的帐户，然后选择 **[!UICONTROL 下一]** 步以继续。

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## 后续步骤

按照本教程，您已建立了与帐户的 [!DNL ADLS Gen2] 连接。 您现在可以继续阅读下一个教程 [并配置数据流，将数据从云存储引入 [!DNL Platform]](../../dataflow/batch/cloud-storage.md)。
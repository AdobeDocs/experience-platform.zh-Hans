---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Azure Data Lake存储Gen2源连接器
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---


# 在UI [!DNL Azure Data Lake Storage Gen2] 中创建源连接器

Adobe Experience Platform的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用用 [!DNL Azure Data Lake Storage Gen2] 户界面验证源连接器（以下称“ADLS Gen2”）的 [!DNL Platform] 步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

- [体验数据模型(XDM)系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   - [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
- [实时客户用户档案](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有ADLS Gen2基本连接，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/batch/cloud-storage.md)。

### 收集所需的凭据

要验证ADLS Gen2源连接器的身份，必须为以下连接属性提供值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `url` | ADLS Gen2的端点。 |
| `servicePrincipalId` | 应用程序的客户端ID。 |
| `servicePrincipalKey` | 应用程序的密钥。 |
| `tenant` | 包含您的应用程序的租户信息。 |

有关这些值的详细信息，请参 [阅此ADLS Gen2文档](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)。

## 连接您的ADLS Gen2帐户

收集所需凭据后，您可以按照以下步骤创建新的入站基础连接，将ADLS Gen2帐户链接到 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 *[!UICONTROL “源”以访问]* “源”工作区。 “目 *[!UICONTROL 录]* ”选项卡显示各种源，可用于创建入站基本连接。 每个源显示与它们关联的现有基本连接数。

在“ *[!UICONTROL 云存储]* ”类别下， **[!UICONTROL 选择Azure Data Lake Gen2]** ，在屏幕的右侧显示一个信息栏。 信息栏提供所选源的简短说明，以及与源视图连接的选项（其文档）。 要创建新的入站基本连接，请单击“添 **[!UICONTROL 加数据”]**。

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

出 *[!UICONTROL 现“连接到Azure数据湖Gen2]* ”对话框。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供基本连接，包括名称、可选说明和您的ADLS Gen2凭据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新的基本连接。

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### 现有帐户

要连接现有帐户，请选择要连接的ADLS Gen2帐户，然后选择“下 **[!UICONTROL 一步]** ”以继续。

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## 后续步骤

通过遵循本教程，您已建立了与ADLS Gen2帐户的基本连接。 您现在可以继续阅读下一个教程 [并配置数据流，将数据从云存储引入平台](../../dataflow/batch/cloud-storage.md)。
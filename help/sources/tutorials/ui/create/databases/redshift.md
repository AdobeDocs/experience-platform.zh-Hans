---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建AmazonRedshift源连接器
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 1%

---


# 在UI [!DNL Amazon Redshift] 中创建源连接器

>The [!NOTE]
>连接 [!DNL Amazon Redshift] 器为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform中的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用用 [!DNL Amazon Redshift] 户界面创建(下[!DNL Redshift]称“”)源连接器 [!DNL Platform] 的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

- [体验数据模型(XDM)系统](../../../../../xdm/home.md): 组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   - [模式合成基础](../../../../../xdm/schema/composition.md): 了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   - [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md): 了解如何使用模式编辑器UI创建自定义模式。
- [实时客户用户档案](../../../../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果已有基本连 [!DNL Redshift] 接，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/databases.md)。

### 收集所需的凭据

要访问您的帐 [!DNL Redshift] 户， [!DNL Platform]您必须提供以下值：

| **凭据** | **描述** |
| -------------- | --------------- |
| `server` | 与您的帐户关联的 [!DNL Redshift] 服务器。 |
| `username` | 与您的帐户关联的 [!DNL Redshift] 用户名。 |
| `password` | 与您的帐户关联的 [!DNL Redshift] 密码。 |
| `database` | 您正 [!DNL Redshift] 在访问的数据库。 |

有关入门的详细信息，请参 [阅此Redshift文档](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html)。

## 连接帐 [!DNL Redshift] 户

收集所需凭据后，您可以按照以下步骤创建新的入站基础连接，以将帐户链 [!DNL Redshift] 接到 [!DNL Platform]。

登录到 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然后从左 **[!UICONTROL 侧导航栏]** 中选 *[!UICONTROL 择源]* ，以访问源工作区。 “目 *[!UICONTROL 录]* ”屏幕显示可为其创建入站基本连接的各种源，每个源显示与它们关联的现有基本连接数。

在“数 *[!UICONTROL 据库]* ”类别下， **[!UICONTROL 选择“]** Amazon红移”以显示屏幕右侧的信息栏。 信息栏提供所选源的简短描述以及与源或视图其文档的选项。 要创建新的入站基本连接，请选择“ **[!UICONTROL 连接源”]**。

![](../../../../images/tutorials/create/redshift/catalog.png)

将显 *[!UICONTROL 示“连接到AmazonRedshift]* ”页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供基本连接，包括名称、可选说明和凭 [!DNL Redshift] 据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新的基本连接。

![](../../../../images/tutorials/create/redshift/new.png)

### 现有帐户

要连接现有帐户，请选 [!DNL Redshift] 择要连接的帐户，然后选择 **[!UICONTROL 下一]** 步以继续。

![](../../../../images/tutorials/create/redshift/existing.png)

## 后续步骤

按照本教程，您已建立了与帐户的基本 [!DNL Redshift] 连接。 您现在可以继续阅读下一个教程， [并配置数据流以将数据引入平台](../../dataflow/databases.md)。
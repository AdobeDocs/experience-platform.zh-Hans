---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中的Azure HDInsights源连接器上创建Apache Hive
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---


# 在UI [!DNL Apache Hive] 中创 [!DNL Azure HDInsights] 建源连接器

>[!NOTE]
>
> 开 [!DNL Apache Hive] 关接 [!DNL Azure HDInsights] 头为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用用户界 [!DNL Apache Hive] 面创 [!DNL Azure HDInsights] 建源连接器的 [!DNL Platform] 步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

* [[!DNL Experience Data Model] (XDM)系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL实时客户用户档案]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果已有有效的连 [!DNL Hive] 接，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/databases.md)

### 收集所需的凭据

要访问您的帐 [!DNL Hive] 户， [!DNL Platform]您必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 服务器的IP地址或主 [!DNL Hive] 机名。 |
| `username` | 用于访问服务器的用 [!DNL Hive] 户名。 |
| `password` | 与用户对应的口令。 |

有关快速入门的详细信息，请参 [ [!DNL Hive] 阅本文档](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted)。

## 连接帐 [!DNL Hive] 户

收集所需凭据后，您可以按照以下步骤将帐户链 [!DNL Hive] 接到 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 **[!UICONTROL “源”以访问]** “源”工作区。 “ **[!UICONTROL 目录]** ”屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“数据 **[!UICONTROL 库]** ”类别下，选 **[!UICONTROL 择Hive]**。 如果这是您首次使用此连接器，请选择“ **[!UICONTROL 配置]**”。 否则，选择 **[!UICONTROL 添加数据]** ，以创建新连 [!DNL Hive] 接器。

![目录](../../../../images/tutorials/create/hive/catalog.png)

此时 **[!UICONTROL 将显示“连接到配置]** ”页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供名称、可选说明和凭 [!DNL Hive] 据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新连接。

![connect](../../../../images/tutorials/create/hive/new.png)

### 现有帐户

要连接现有帐户，请选 [!DNL Hive] 择要连接的帐户，然后选择 **[!UICONTROL 下一]** 步以继续。

![现有](../../../../images/tutorials/create/hive/existing.png)

## 后续步骤

按照本教程，您已建立了与帐户的 [!DNL Hive] 连接。 您现在可以继续学习下一个教程， [并配置一个数据流以将数据引入 [!DNL Platform]](../../dataflow/databases.md)。
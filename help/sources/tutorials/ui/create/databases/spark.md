---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中在Azure HDInsights源连接器上创建Apache Spark
topic: overview
translation-type: tm+mt
source-git-commit: 5ad763d2167c68f3293a2813248efaee22230a52
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---


# 在UI中在Azure HDInsights源连接器上创建Apache Spark

> [!NOTE]
> Azure HDInsights连接器上的Apache Spark处于测试阶段。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform中的源连接器提供按计划接收外部源数据的能力。 本教程提供了在Azure HDInsights源连接器上使用Platform用户界面创建Apache Spark的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [体验数据模型(XDM)系统](../../../../../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md): 了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md): 了解如何使用模式编辑器UI创建自定义模式。
* [实时客户用户档案](../../../../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有有效的Spark连接，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/databases.md)

### 收集所需的凭据

要在Platform时访问您的Spark帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | Spark服务器的IP地址或主机名。 |
| `username` | 用于访问Spark服务器的用户名。 |
| `password` | 与用户对应的口令。 |

有关快速入门的详细信息，请参 [阅此Spark文档](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview)。

## 连接您的Spark帐户

收集所需凭据后，您可以按照以下步骤创建新的Spark帐户以连接到Platform。

登录到 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然后从左 **侧导航栏** 中选 *择源* ，以访问源工作区。 “目 *录* ”屏幕显示您可以为其创建入站帐户的各种源，每个源显示与它们关联的现有帐户和数据集流的数量。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“数 *据库* ”类别下 **，选** 择Spark，在屏幕右侧显示一个信息栏。 信息栏提供所选源的简短描述以及与源或视图其文档的选项。 要创建新的入站连接，请选择“ **连接源”**。

![目录](../../../../images/tutorials/create/spark/catalog.png)

此时 *将显示“连接到* Spark”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **新帐户**”。 在显示的输入表单上，提供连接名称、可选说明和Spark凭据。 完成后，选 **择** Connect，然后允许一段时间建立新帐户。

![新](../../../../images/tutorials/create/spark/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的Spark帐户，然后选择“下 **一步** ”以继续。

![现有](../../../../images/tutorials/create/spark/existing.png)

## 后续步骤

按照本教程，您已建立了与Spark帐户的连接。 您现在可以继续学习下一个教程并 [配置数据流以将数据引入Platform](../../dataflow/databases.md)。
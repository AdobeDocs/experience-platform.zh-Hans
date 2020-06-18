---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Azure突触Analytics源连接器
topic: overview
translation-type: tm+mt
source-git-commit: 5ad763d2167c68f3293a2813248efaee22230a52
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---


# 在UI中创建Azure突触Analytics源连接器

> [!NOTE]
> Azure突触Analytics接头测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform中的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用Platform用户界面创建Azure突触Analytics（以下称“突触”）源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [体验数据模型(XDM)系统](../../../../../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md): 了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md): 了解如何使用模式编辑器UI创建自定义模式。
* [实时客户用户档案](../../../../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果已有Synapse基连接，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/databases.md)。

### 收集所需的凭据

要在Platform上访问Synapse帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 与Synapse身份验证关联的连接字符串。 Synapse连接字符串模式为 `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`。 |

有关此值的详细信息，请参 [阅此Synapse文档](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-sql-data-warehouse)。

## 连接您的突触帐户

收集所需凭据后，您可以按照以下步骤创建新的入站基础连接，将您的Synapse帐户链接到Platform。

登录到 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然后从左 **侧导航栏** 中选 *择源* ，以访问源工作区。 “目 *录* ”屏幕显示可为其创建入站基本连接的各种源，每个源显示与它们关联的现有基本连接数。

在“数 *据库* ”类别下， **选择“Azure突触Analytics** ”以在屏幕右侧显示一个信息栏。 信息栏提供所选源的简短描述以及与源或视图其文档的选项。 要创建新的入站基本连接，请选择“ **连接源”**。

![](../../../../images/tutorials/create/azure-synapse-analytics/catalog.png)

将显 *示“连接到Azure突触Analytics* ”页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **新帐户**”。 在显示的输入表单上，为基本连接提供名称、可选说明和您的突触凭据。 完成后，选 **择** Connect，然后允许一段时间建立新的基本连接。

![](../../../../images/tutorials/create/azure-synapse-analytics/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的突触帐户，然后选择“下 **一步** ”继续。

![](../../../../images/tutorials/create/azure-synapse-analytics/existing.png)

## 后续步骤

通过本教程，您已建立了与Synapse帐户的基本连接。 您现在可以继续学习下一个教程并 [配置数据流以将数据引入Platform](../../dataflow/databases.md)。
---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建GreenPlum源连接器
topic: overview
translation-type: tm+mt
source-git-commit: 5ad763d2167c68f3293a2813248efaee22230a52
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---


# 在UI中创建GreenPlum源连接器

> [!NOTE]
> GreenPlum连接器为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform中的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用Platform用户界面创建GreenPlum源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [体验数据模型(XDM)系统](../../../../../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md): 了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md): 了解如何使用模式编辑器UI创建自定义模式。
* [实时客户用户档案](../../../../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有有效的GreenPlum连接，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/databases.md)。

### 收集所需的凭据

以下各节提供您需要了解的其他信息，以便使用Flow Service API成功连接到GreenPlum。

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 用于连接到GreenPlum实例的连接字符串。 GreenPlum的连接串模式为 `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

有关入门的详细信息，请参 [阅此GreenPlum文档](https://gpdb.docs.pivotal.io/580/security-guide/topics/Authenticate.html#topic_fzv_wb2_jr__config_ssl_client_conn)。

## 连接您的GreenPlum帐户

收集所需凭据后，您可以按照以下步骤创建新的GreenPlum帐户以连接到Platform。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选 *[!UICONTROL 择源]* ，以访问源工作区。 “目 *[!UICONTROL 录]* ”屏幕显示可为其创建入站帐户的各种源，每个源显示与它们关联的现有帐户和数据集流的数量。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“数 *[!UICONTROL 据库]* ”类别 **[!UICONTROL 下]** ，选择“GreenPlum **”，单** 击+图标(+)以创建新的GreenPlum连接器。

![目录](../../../../images/tutorials/create/greenplum/catalog.png)

将显 *[!UICONTROL 示“连接到GreenPlum]* ”页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，为连接提供名称、可选说明和GreenPlum凭据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新帐户。

![connect](../../../../images/tutorials/create/greenplum/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的GreenPlum帐户，然后 **[!UICONTROL 选择]** 右上角的“下一步”以继续。

![现有](../../../../images/tutorials/create/greenplum/existing.png)

## 后续步骤

通过遵循本教程，您已建立了与GreenPlum帐户的连接。 您现在可以继续学习下一个教程并 [配置数据流以将数据引入Platform](../../dataflow/databases.md)。
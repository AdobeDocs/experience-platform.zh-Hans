---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建HP Vertica源连接器
topic: overview
translation-type: tm+mt
source-git-commit: a015d2612bc5a72004e15dc5706c7718617a0af4
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---


# 在UI中创建HP Vertica源连接器

> [!NOTE]
> HP Vertica连接器处于测试阶段。 功能和文档可能会发生更改。

Adobe Experience Platform中的源连接器提供按计划收集外部源数据的能力。 本教程提供了使用平台用户界面创建HP Vertica源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [体验数据模型(XDM)系统](../../../../../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md): 了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md): 了解如何使用模式编辑器UI创建自定义模式。
* [实时客户用户档案](../../../../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有有效的HP Vertica连接，您可以跳过本文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/databases.md)。

### 收集所需的凭据

以下各节提供了使用Flow Service API成功连接到HP Vertica所需的其他信息。

| 凭据 | 描述 |
| ---------- | ----------- |
| `connectionString` | 用于连接到HP Vertica实例的连接字符串。 HP Vertica的连接字符串模式是 `Server=<server>;Port=<port>;Database=<database>;UID=<user name>;PWD=<password>` |

有关快速入门的详细信息，请参 [阅此HP Vertica文档](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm)。

## 连接您的HP Vertica帐户

收集所需凭据后，您可以按照以下步骤创建新的HP Vertica帐户以连接到平台。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中 *[!UICONTROL 选择“源]* ”以访问“源”工作区。 “目 *[!UICONTROL 录]* ”屏幕显示可为其创建入站帐户的各种源，每个源显示与它们关联的现有帐户和数据集流的数量。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“数 *[!UICONTROL 据库]* ”类别 **[!UICONTROL 下]** ，选择“HP Vertica **”，单** 击+图标(+)以创建新的HP Vertica连接器。

![目录](../../../../images/tutorials/create/hp-vertica/catalog.png)

将显 *[!UICONTROL 示“Connect to HP Vertica]* ”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供连接名称、可选说明和您的HP Vertica凭据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新帐户。

![connect](../../../../images/tutorials/create/hp-vertica/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的HP Vertica帐户，然后 **[!UICONTROL 选择]** 右上角的“下一步”以继续。

![现有](../../../../images/tutorials/create/hp-vertica/existing.png)

## 后续步骤

按照本教程，您已建立了与HP Vertica帐户的连接。 您现在可以继续阅读下一个教程， [并配置数据流以将数据引入平台](../../dataflow/databases.md)。
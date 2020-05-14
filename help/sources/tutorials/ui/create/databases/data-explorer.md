---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Azure Data Explorer源连接器
topic: overview
translation-type: tm+mt
source-git-commit: 2162c66b1664ecaaf0b609fe3f7ccf58c4a5d31d
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---


# 在UI中创建Azure Data Explorer源连接器

> [!NOTE]
> Azure Data Explorer连接器处于测试状态。 功能和文档可能会发生更改。

Adobe Experience Platform中的源连接器提供按计划收集外部源数据的能力。 本教程提供了使用平台用户界面创建Azure Data Explorer（以下称“Data Explorer”）源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [体验数据模型(XDM)系统](../../../../../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md): 了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md): 了解如何使用模式编辑器UI创建自定义模式。
* [实时客户用户档案](../../../../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有有效的文档资源管理器连接，您可以跳过此连接的其余部分，继续学习有关配置数据 [流的教程](../../dataflow/databases.md)。

### 收集所需的凭据

要在平台上访问您的Data Explorer帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `endpoint` | Data Explorer服务器的端点。 |
| `database` | Data Explorer数据库的名称。 |
| `tenant` | 用于连接到Data Explorer数据库的唯一租户ID。 |
| `servicePrincipalId` | 用于连接到Data Explorer数据库的唯一服务主体ID。 |
| `servicePrincipalKey` | 用于连接到Data Explorer数据库的唯一服务主体键。 |

有关快速入门的详细信息，请参 [阅此数据浏览器文档](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad)。

## 连接您的Azure Data Explorer帐户

收集所需凭据后，您可以按照以下步骤创建新的Data Explorer帐户以连接到平台。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中 *选择“源* ”以访问“源”工作区。 “目 *[!UICONTROL 录]* ”屏幕显示您可以为其创建入站帐户的各种源，每个源显示与它们关联的现有帐户和数据集流的数量。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“数 *[!UICONTROL 据库]* ”类别下，选 **[!UICONTROL 择Azure Data Explorer]** ，然 **** 后单击+图标(+)以创建新的Data Explorer连接器。

![目录](../../../../images/tutorials/create/data-explorer/catalog.png)

将显 *[!UICONTROL 示“连接到Azure Data Explorer]* ”页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供连接的名称、可选说明和您的数据浏览器凭据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新帐户。

![connect](../../../../images/tutorials/create/data-explorer/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的Data Explorer帐户，然后选择“下 **[!UICONTROL 一步]** ”继续。

![现有](../../../../images/tutorials/create/data-explorer/existing.png)

## 后续步骤

按照本教程，您已建立了与Data Explorer帐户的连接。 您现在可以继续阅读下一个教程， [并配置数据流以将数据引入平台](../../dataflow/databases.md)。
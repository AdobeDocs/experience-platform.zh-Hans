---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Google大查询源连接器
topic: overview
translation-type: tm+mt
source-git-commit: 2162c66b1664ecaaf0b609fe3f7ccf58c4a5d31d
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---


# 在UI中创建Google大查询源连接器

> [!NOTE]
> Google BigQuery连接器处于测试阶段。 功能和文档可能会发生更改。

Adobe Experience Platform中的源连接器提供按计划收集外部源数据的能力。 本教程提供了使用平台用户界面创建Google大查询（以下称“GBQ”）源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [体验数据模型(XDM)系统](../../../../../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md): 了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md): 了解如何使用模式编辑器UI创建自定义模式。
* [实时客户用户档案](../../../../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果已有GBQ基连接，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/databases.md)。

### 收集所需的凭据

要在平台上访问您的GBQ帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `project` | 要查询的默认BigQuery项目的项目ID。 |
| `clientID` | 用于生成刷新令牌的ID值。 |
| `clientSecret` | 用于生成刷新令牌的机密值。 |
| `refreshToken` | 从Google获取的用于授权访问BigQuery的刷新令牌。 |

有关这些值的详细信息，请参 [阅此GBQ文档](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing)。

## 连接您的GBQ帐户

收集所需凭据后，您可以按照以下步骤创建新的入站基础连接，将GBQ帐户链接到平台。

登录到 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然后从左 **侧导航栏** 中 *选择“源* ”以访问“源”工作区。 “目 *录* ”屏幕显示可为其创建入站基本连接的各种源，每个源显示与它们关联的现有基本连接数。

在“ *类别* ”下， **选择Google Big查询** ，以在屏幕右侧显示一个信息栏。 信息栏提供所选源的简短描述以及与源或视图其文档的选项。 要创建新的入站基本连接，请选择“ **连接源”**。

![](../../../../images/tutorials/create/google-big-query/sources-catalog.png)

将显 *示“连接到Google Big查询* ”页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **新帐户**”。 在显示的输入表单上，提供基本连接，包括名称、可选说明和GBQ凭据。 完成后，选 **择** Connect，然后允许一段时间建立新的基本连接。

![](../../../../images/tutorials/create/google-big-query/gbq-new-credentials.png)

### 现有帐户

要连接现有帐户，请选择要连接的GBQ帐户，然后选择“下 **一步** ”以继续。

![](../../../../images/tutorials/create/google-big-query/gbq-existing-credentials.png)

## 后续步骤

按照本教程，您已建立了与GBQ帐户的基本连接。 您现在可以继续阅读下一个教程， [并配置数据流以将数据引入平台](../../dataflow/databases.md)。
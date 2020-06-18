---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建HubSpot源连接器
topic: overview
translation-type: tm+mt
source-git-commit: 7328226b8349ffcdddadbd27b74fc54328b78dc5
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---


# 在UI中创建HubSpot源连接器

> [!NOTE]
> HubSpot连接器为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform中的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用Platform用户界面创建HubSpot源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有一定的了解：

* [体验数据模型(XDM)系统](../../../../../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md): 了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md): 了解如何使用模式编辑器UI创建自定义模式。
* [实时客户用户档案](../../../../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已有HubSpot基连接，您可以跳过本文档的其余部分，继续学习有关配置营销 [自动化数据流的教程](../../dataflow/marketing-automation.md)。

### 收集所需的凭据

要在Platform访问HubSpot帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `clientId` | 与您的HubSpot应用程序关联的客户端ID。 |
| `clientSecret` | 与您的HubSpot应用程序关联的客户端机密。 |
| `accessToken` | 最初验证您的OAuth集成时获得的访问令牌。 |
| `refreshToken` | 最初验证您的OAuth集成时获取的刷新令牌。 |

有关快速入门的详细信息，请参阅此 [HubSpot文档](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)。

## 连接您的HubSpot帐户

收集所需凭据后，您可以按照以下步骤创建新的入站基础连接，将HubSpot帐户链接到Platform。

登录到 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然后从左 **侧导航栏** 中选 *择源* ，以访问源工作区。 “目 *录* ”屏幕显示可为其创建入站基本连接的各种源，每个源显示与它们关联的现有基本连接数。

在“营 *销自动化* ”类别下， **选择HubSpot** ，在屏幕的右侧显示一个信息栏。 信息栏提供所选源的简短描述以及与源或视图其文档的选项。 要创建新的入站基本连接，请选择“ **连接源”**。

![目录](../../../../images/tutorials/create/hubspot/catalog.png)

将显 *示“连接到HubSpot* ”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **新帐户**”。 在显示的输入表单上，提供基本连接，包括名称、可选说明和HubSpot凭据。 完成后，选 **择** Connect，然后允许一段时间建立新的基本连接。

![connect](../../../../images/tutorials/create/hubspot/connect.png)

### 现有帐户

要连接现有帐户，请选择要连接的HubSpot帐户，然后选择“下 **一步** ”继续。

![现有](../../../../images/tutorials/create/hubspot/existing.png)

## 后续步骤

通过本教程，您已建立了与HubSpot帐户的基本连接。 您现在可以继续阅读下一个教程并 [配置数据流，将营销自动化系统数据引入Platform](../../dataflow/marketing-automation.md)。
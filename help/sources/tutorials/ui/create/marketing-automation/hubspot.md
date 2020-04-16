---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建HubSpot源连接器
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# 在UI中创建HubSpot源连接器

Adobe Experience Platform中的源连接器提供了按计划收集外部来源数据的能力。 本教程提供了使用平台用户界面创建HubSpot源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [体验数据模型(XDM)系统](../../../../../xdm/home.md):Experience Platform组织客户体验数据的标准化框架。
   * [模式合成的基础知识](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [实时客户用户档案](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。

如果您已有HubSpot基本连接，则可跳过本文档的其余部分，继续学习有关配置营销自动化 [数据流的教程](../../dataflow/marketing-automation.md)。

### 收集所需的凭据

要在平台上访问HubSpot帐户，必须提供以下值：

| 凭证 | 描述 |
| ---------- | ----------- |
| `clientId` | 与您的HubSpot应用程序关联的客户端ID。 |
| `clientSecret` | 与您的HubSpot应用程序关联的客户端机密。 |
| `accessToken` | 首次验证OAuth集成时获得的访问令牌。 |
| `refreshToken` | 首次验证OAuth集成时获取的刷新令牌。 |

有关快速入门的详细信息，请参阅此 [HubSpot文档](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)。

## 连接您的HubSpot帐户

收集所需凭据后，您可以按照以下步骤创建新的入站基本连接，以将HubSpot帐户关联到平台。

登录到 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然后从左侧导航栏中选 **择“源** ”以访问“源 ** ”工作区。 “目 *录* ”屏幕显示各种来源，您可以为其创建入站基本连接，每个来源显示与这些来源关联的现有基本连接的数量。

在“营 *销自动化* ”类别下，选择 **HubSpot** ，在屏幕右侧显示一个信息栏。 信息栏提供所选源的简短说明以及与源或视图其文档的连接选项。 要创建新的入站基本连接，请选择“ **Connect源”**。

![目录](../../../../images/tutorials/create/hubspot/catalog.png)

将显 *示“连接到HubSpot* ”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **新帐户”**。 在显示的输入表单上，为基本连接提供名称、可选说明和HubSpot凭据。 完成后，选择 **Connect** ，然后为新的基本连接建立留出一些时间。

![connect](../../../../images/tutorials/create/hubspot/connect.png)

### 现有帐户

要连接现有帐户，请选择要连接的HubSpot帐户，然后选择“下一 **步** ”继续。

![现有](../../../../images/tutorials/create/hubspot/existing.png)

## 后续步骤

通过本教程，您已经建立了与HubSpot帐户的基本连接。 您现在可以继续阅读下一个教程并配 [置数据流，以将营销自动化系统数据引入平台](../../dataflow/marketing-automation.md)。
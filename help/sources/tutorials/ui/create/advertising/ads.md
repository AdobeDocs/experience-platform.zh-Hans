---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Google AdWords源连接器
topic: overview
translation-type: tm+mt
source-git-commit: e7211c9ebfd8fecff3780198d71e18436f3ffab3
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---


# 在UI中创建Google AdWords源连接器

Adobe Experience Platform中的源连接器提供按计划收集外部源数据的能力。 本教程提供了使用平台用户界面创建Google AdWords源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [体验数据模型(XDM)系统](../../../../../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md): 了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md): 了解如何使用模式编辑器UI创建自定义模式。
* [实时客户用户档案](../../../../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已有Google AdWords连接，则可跳过本文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/payments.md)

### 收集所需的凭据

要访问您的Google AdWords帐户平台，您必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `clientCustomerId` | AdWords帐户的客户客户ID。 |
| `developerToken` | 与管理者帐户关联的开发者令牌。 |
| `refreshToken` | 从Google获取的用于授权访问AdWords的刷新令牌。 |
| `clientId` | 用于获取刷新令牌的Google应用程序的客户端ID。 |
| `clientSecret` | 用于获取刷新令牌的google应用程序的客户端机密。 |

有关快速入门的更多信息，请参 [阅此Google AdWords文档](https://developers.google.com/adwords/api/docs/guides/authentication)。

## 连接您的Google AdWords帐户

收集所需凭据后，您可以按照以下步骤创建新的入站基础连接，将您的Google AdWords帐户链接到平台。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **侧导航栏** 中 *选择“源* ”以访问“源”工作区。 “目 *录* ”屏幕显示可为其创建入站基本连接的各种源，每个源显示与它们关联的现有基本连接数。

在“ *广告* ”类别 **下** ，选择Google AdWords，在屏幕右侧显示一个信息栏。 信息栏提供所选源的简短描述以及与源或视图其文档的选项。 要创建新的入站基本连接，请选择“ **连接源”**。

![目录](../../../../images/tutorials/create/ads/catalog.png)

将显 *示“连接到Google AdWords* ”页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **新帐户**”。 在显示的输入表单上，提供基本连接，包括名称、可选说明和您的Google AdWords凭据。 完成后，选 **择** Connect，然后允许一段时间建立新的基本连接。

![connect](../../../../images/tutorials/create/ads/connect.png)

### 现有帐户

要连接现有帐户，请选择要连接的Google AdWords帐户，然后选择“下 **一** 步”继续。

![现有](../../../../images/tutorials/create/ads/existing.png)

## 后续步骤

通过遵循本教程，您已建立了与Google AdWords帐户的基本连接。 您现在可以继续阅读下一个教程， [并配置一个数据流，将广告数据引入平台](../../dataflow/advertising.md)。
---
keywords: Experience Platform;home;popular topics;Google AdWords;Google AdWords source connector;google adwords connector
solution: Experience Platform
title: 在UI中创建Google AdWords源连接器
topic: overview
description: 本教程提供了使用平台用户界面创建Google AdWords源连接器的步骤。
translation-type: tm+mt
source-git-commit: 0da686743e8bc57d310f7eff6f1bf812a8f31238
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---


# 在UI [!DNL Google AdWords] 中创建源连接器

>[!NOTE]
>
>连接 [!DNL Google AdWords] 器为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用用户界 [!DNL Google AdWords] 面创建源连接器 [!DNL Platform] 的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

* [[!DNL Experience Data Model] (XDM)系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL实时客户用户档案]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果已有有效的连 [!DNL Google AdWords] 接，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/payments.md)

### 收集所需的凭据

要访问您的帐 [!DNL Google AdWords] 户， [!DNL Platform]您必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `clientCustomerId` | 帐户的客户客户 [!DNL AdWords] ID。 |
| `developerToken` | 与管理者帐户关联的开发人员令牌。 |
| `refreshToken` | 从获取的用于授 [!DNL Google] 权访问的刷新令牌 [!DNL AdWords]。 |
| `clientId` | 用于获取刷新 [!DNL Google] 令牌的应用程序的客户端ID。 |
| `clientSecret` | 用于获取刷新 [!DNL Google] 令牌的应用程序的客户端机密。 |

有关快速入门的详细信息，请参阅此 [[!DNL Google AdWords] 文档](https://developers.google.com/adwords/api/docs/guides/authentication)。

## 连接帐 [!DNL Google AdWords] 户

收集所需凭据后，您可以按照以下步骤将帐户链 [!DNL Google AdWords] 接到 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 **[!UICONTROL “源”以访问]** “源”工作区。 “ **[!UICONTROL 目录]** ”屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“广 **[!UICONTROL 告]** ”类别下， **[!UICONTROL 选择Google AdWords]**。 如果这是您首次使用此连接器，请选择“ **[!UICONTROL 配置]**”。 否则，选择 **[!UICONTROL 添加数据]** ，以创建新连 [!DNL Google AdWords] 接器。

![目录](../../../../images/tutorials/create/ads/catalog.png)

将显 **[!UICONTROL 示“连接到Google AdWords]** ”页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供名称、可选说明和凭 [!DNL Google AdWords] 据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新连接。

![connect](../../../../images/tutorials/create/ads/connect.png)

### 现有帐户

要连接现有帐户，请选 [!DNL Google AdWords] 择要连接的帐户，然后选择 **[!UICONTROL 下一]** 步以继续。

![现有](../../../../images/tutorials/create/ads/existing.png)

## 后续步骤

按照本教程，您已建立了与帐户的 [!DNL Google AdWords] 连接。 您现在可以继续阅读下一个教程， [并配置一个数据流以将广告数据引入 [!DNL Platform]](../../dataflow/advertising.md)。
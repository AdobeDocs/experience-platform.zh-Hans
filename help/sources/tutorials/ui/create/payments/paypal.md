---
keywords: Experience Platform；主页；热门主题；Paypal；Paypal
solution: Experience Platform
title: 在UI中创建PayPal源连接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建PayPal源连接。
exl-id: bbd3f634-cb28-45d8-9b7b-ed3873101882
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# 创建 [!DNL PayPal] UI中的源连接

Adobe Experience Platform中的源连接器提供了按计划摄取外部来源数据的功能。 本教程提供了用于创建 [!DNL PayPal] 源连接器，使用平台用户界面。

## 快速入门

本教程需要深入了解Adobe Experience Platform的以下组件：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md)：用于实现此目标的标准化框架 [!DNL Experience Platform] 组织客户体验数据。
   * [模式组合基础](../../../../../xdm/schema/composition.md)：了解XDM架构的基本构建基块，包括架构构成中的关键原则和最佳实践。
   * [架构编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md)：了解如何使用架构编辑器UI创建自定义架构。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根据来自多个来源的汇总数据提供统一的实时使用者个人资料。

如果您已经拥有有效的 [!DNL PayPal] 连接，您可以跳过本文档的其余部分，并继续阅读以下教程： [配置数据流](../../dataflow/payments.md)

### 收集所需的凭据

要访问您的 [!DNL PayPal] 帐户平台，您必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `host` | 的URL [!DNL PayPal] 实例。 |
| `clientID` | 与您的关联的客户端ID [!DNL PayPal] 应用程序。 |
| `clientSecret` | 与您的关联的客户端密钥 [!DNL PayPal] 应用程序。 |

有关入门的更多信息，请参阅此 [[!DNL PayPal] 文档](https://developer.paypal.com/docs/api/overview/#get-credentials)

## 连接您的 [!DNL PayPal] 帐户

收集所需的凭据后，您可以按照以下步骤链接您的 [!DNL PayPal] Platform帐户。

登录 [Adobe Experience Platform](https://platform.adobe.com) 然后选择 **[!UICONTROL 源]** 以访问 **[!UICONTROL 源]** 工作区。 此 **[!UICONTROL 目录]** 屏幕显示您可以为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择相应的类别。 或者，您可以使用搜索选项查找要使用的特定源。

在 **[!UICONTROL 支付]** 类别，选择 **[!UICONTROL PayPal]**. 如果这是您第一次使用此连接器，请选择 **[!UICONTROL 配置]**. 否则，选择 **[!UICONTROL 添加数据]** 以新建 [!DNL PayPal] 连接器。

![目录](../../../../images/tutorials/create/paypal/catalog.png)

此 **[!UICONTROL 连接到PayPal]** 页面。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用的是新凭据，请选择 **[!UICONTROL 新帐户]**. 在出现的输入表单上，提供名称、可选描述以及 [!DNL PayPal] 凭据。 完成后，选择 **[!UICONTROL Connect]** 然后留出一些时间来建立新连接。

![connect](../../../../images/tutorials/create/paypal/connect.png)

### 现有帐户

要连接现有帐户，请选择 [!DNL PayPal] 要连接的帐户，然后选择 **[!UICONTROL 下一个]** 以继续。

![现有](../../../../images/tutorials/create/paypal/existing.png)

## 后续步骤

按照本教程，您已建立与的连接 [!DNL PayPal] 帐户。 您现在可以继续下一教程和 [配置数据流以将支付数据引入Platform](../../dataflow/payments.md).

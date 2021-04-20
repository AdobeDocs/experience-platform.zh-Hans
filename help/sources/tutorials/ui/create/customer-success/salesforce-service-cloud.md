---
keywords: Experience Platform；主页；热门主题；Salesforce Service Cloud;salesforce服务云
solution: Experience Platform
title: 在UI中创建Salesforce服务云源连接
topic: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI创建Salesforce Service Cloud源连接。
translation-type: tm+mt
source-git-commit: a0b016e8adc519bc79701f9fd850b6ddf7d46127
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 1%

---


# 在UI中创建[!DNL Salesforce Service Cloud]源连接

Adobe Experience Platform中的源连接器提供按计划收集外部源数据的能力。 本教程提供了使用[!DNL Platform]用户界面创建[!DNL Salesforce Service Cloud]（以下称为“SSC”）源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [[!DNL Experience Data Model (XDM)] 系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [模式合成的基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构建基块，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根据来自多个来源的汇总数据提供统一、实时的消费者用户档案。

如果您已有有效的SSC连接，则可以跳过此文档的其余部分，继续学习有关[配置数据流](../../dataflow/customer-success.md)的教程

### 收集所需凭据

要在[!DNL Platform]上访问您的SSC帐户，必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `username` | 用户帐户的用户名。 |
| `password` | 用户帐户的密码。 |
| `securityToken` | 用户帐户的安全令牌。 |

有关快速入门的详细信息，请参阅[this [!DNL Salesforce Service Cloud] 文档](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm)。

## 连接您的[!DNL Salesforce Service Cloud]帐户

收集所需凭据后，您可以按照以下步骤将SSC帐户链接到[!DNL Platform]。

登录到[Adobe Experience Platform](https://platform.adobe.com)，然后从左侧导航栏中选择&#x200B;**[!UICONTROL Sources]**&#x200B;以访问&#x200B;**[!UICONTROL Sources]**&#x200B;工作区。 **[!UICONTROL Catalog]**&#x200B;屏幕显示了可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在&#x200B;**[!UICONTROL Customer Success]**&#x200B;类别下，选择&#x200B;**[!UICONTROL Salesforce Service Cloud]**。 如果这是您首次使用此连接器，请选择&#x200B;**[!UICONTROL Configure]**。 否则，选择&#x200B;**[!UICONTROL Add data]**&#x200B;创建新的SSC连接器。

![目录](../../../../images/tutorials/create/ssc/catalog.png)

将显示&#x200B;**[!UICONTROL Connect to Salesforce Service Cloud]**&#x200B;页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择&#x200B;**[!UICONTROL New account]**。 在显示的输入表单上，提供名称、可选说明和您的SSC凭据。 完成后，选择&#x200B;**[!UICONTROL Connect]**，然后为新连接建立留出一些时间。

![connect](../../../../images/tutorials/create/ssc/connect.png)

### 现有帐户

要连接现有帐户，请选择要连接的SSC帐户，然后选择&#x200B;**[!UICONTROL Next]**&#x200B;继续。

![现有](../../../../images/tutorials/create/ssc/existing.png)

## 后续步骤

通过本教程，您已建立了与SSC帐户的连接。 您现在可以继续下一个教程，并[配置一个数据流，以将客户成功数据导入 [!DNL Platform]](../../dataflow/customer-success.md)。
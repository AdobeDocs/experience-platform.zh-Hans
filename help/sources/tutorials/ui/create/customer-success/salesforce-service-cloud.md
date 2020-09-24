---
keywords: Experience Platform;home;popular topics;Salesforce Service Cloud;salesforce service cloud
solution: Experience Platform
title: 在UI中创建Salesforce Service Cloud源连接器
topic: overview
type: Tutorial
description: 本教程提供了使用平台用户界面创建Salesforce Service Cloud（以下称“SSC”）源连接器的步骤。
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---


# 在UI [!DNL Salesforce Service Cloud] 中创建源连接器

>[!NOTE]
>
>连接 [!DNL Salesforce Service Cloud] 器为测试版。 有关使用 [测试版标记](../../../../home.md#terms-and-conditions) 的连接器的更多信息，请参阅源概述。

Adobe Experience Platform的源连接器提供按计划接收外部源数据的能力。 本教程提供了使用用 [!DNL Salesforce Service Cloud] 户界面创建（下称“SSC”）源连接器 [!DNL Platform] 的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件进行有效的理解：

* [[!DNL Experience Data Model] (XDM)系统](../../../../../xdm/home.md):组织客户体验数 [!DNL Experience Platform] 据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md):了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用模式编辑器UI创建自定义模式。
* [[!DNL实时客户用户档案]](../../../../../profile/home.md):基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有有效的SSC连接，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/customer-success.md)

### 收集所需的凭据

要在上访问您的SSC帐 [!DNL Platform]户，您必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `username` | 用户帐户的用户名。 |
| `password` | 用户帐户的密码。 |
| `securityToken` | 用户帐户的安全令牌。 |

有关快速入门的详细信息，请参 [ [!DNL Salesforce Service Cloud] 阅本文档](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm)。

## 连接帐 [!DNL Salesforce Service Cloud] 户

收集所需凭据后，您可以按照以下步骤将SSC帐户链接到 [!DNL Platform]。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中选择 **[!UICONTROL “源”以访问]** “源”工作区。 “ **[!UICONTROL 目录]** ”屏幕显示可为其创建帐户的各种源。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“客 **[!UICONTROL 户成功]** ”类别下， **[!UICONTROL 选择Salesforce服务云]**。 如果这是您首次使用此连接器，请选择“ **[!UICONTROL 配置]**”。 否则，选 **[!UICONTROL 择“添加数]** 据”以创建新SSC连接器。

![目录](../../../../images/tutorials/create/ssc/catalog.png)

将显 **[!UICONTROL 示“连接到Salesforce服务云]** ”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供名称、可选说明和您的SSC凭据。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新连接。

![connect](../../../../images/tutorials/create/ssc/connect.png)

### 现有帐户

要连接现有帐户，请选择要连接的SSC帐户，然后选择“下 **[!UICONTROL 一步]** ”继续。

![现有](../../../../images/tutorials/create/ssc/existing.png)

## 后续步骤

通过本教程，您已建立了与SSC帐户的连接。 您现在可以继续阅读下一个教程， [并配置一个数据流，将客户成功数据引入 [!DNL Platform]](../../dataflow/customer-success.md)。
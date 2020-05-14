---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Salesforce Service Cloud源连接器
topic: overview
translation-type: tm+mt
source-git-commit: 2162c66b1664ecaaf0b609fe3f7ccf58c4a5d31d
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---


# 在UI中创建Salesforce Service Cloud源连接器

>[!NOTE]
>Salesforce Service Cloud连接器处于测试状态。 功能和文档可能会发生更改。

Adobe Experience Platform中的源连接器提供按计划收集外部源数据的能力。 本教程提供了使用平台用户界面创建Salesforce Service Cloud（以下称“SSC”）源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [体验数据模型(XDM)系统](../../../../../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md): 了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md): 了解如何使用模式编辑器UI创建自定义模式。
* [实时客户用户档案](../../../../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经有有效的SSC连接，您可以跳过此文档的其余部分，继续学习有关配置 [数据流的教程](../../dataflow/customer-success.md)

### 收集所需的凭据

要在平台上访问您的SSC帐户，您必须提供以下值：

| 凭据 | 描述 |
| ---------- | ----------- |
| `username` | 用户帐户的用户名。 |
| `password` | 用户帐户的密码。 |
| `securityToken` | 用户帐户的安全令牌。 |

有关快速入门的详细信息，请 [参阅此Salesforce服务云文档](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm)。

## 连接您的Salesforce服务云帐户

收集所需凭据后，您可以按照以下步骤创建新的SSC帐户以连接到平台。

登录到 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然后从左 **侧导航栏** 中 *选择“源* ”以访问“源”工作区。 “目 *录* ”屏幕显示您可以为其创建入站帐户的各种源，每个源显示与它们关联的现有帐户和数据集流的数量。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“ *客户成功* ”类别下， **选择Salesforce Service Cloud** ，在屏幕右侧显示一个信息栏。 信息栏提供所选源的简短描述以及与源或视图其文档的选项。 要创建新的入站连接，请选择“ **连接源”**。

![目录](../../../../images/tutorials/create/ssc/catalog.png)

将显 *示“连接到Salesforce服务云* ”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **新帐户**”。 在显示的输入表单上，提供名称、可选说明和您的SSC凭据的连接。 完成后，选 **择** Connect，然后允许一段时间建立新帐户。

![connect](../../../../images/tutorials/create/ssc/connect.png)

### 现有帐户

要连接现有帐户，请选择要连接的SSC帐户，然后选择“下 **一步** ”继续。

![现有](../../../../images/tutorials/create/ssc/existing.png)

## 后续步骤

通过本教程，您已建立了与SSC帐户的连接。 您现在可以继续阅读下一个教程， [并配置一个数据流，将客户成功数据引入平台](../../dataflow/customer-success.md)。
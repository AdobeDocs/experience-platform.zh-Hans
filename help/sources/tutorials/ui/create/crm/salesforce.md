---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中创建Salesforce源连接器
topic: overview
translation-type: tm+mt
source-git-commit: 44c43afc653c147fa12e3e962904bfc79ee0fc64
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---


# 在UI中创建Salesforce源连接器

Adobe Experience Platform中的源连接器提供按计划收集外部来源的CRM数据的能力。 本教程提供了使用平台用户界面创建Salesforce源连接器的步骤。

## 入门指南

本教程需要对Adobe Experience Platform的以下组件有充分的了解：

* [体验数据模型(XDM)系统](../../../../../xdm/home.md): Experience Platform组织客户体验数据的标准化框架。
   * [模式合成基础](../../../../../xdm/schema/composition.md): 了解XDM模式的基本构件，包括模式构成的主要原则和最佳做法。
   * [模式编辑器教程](../../../../../xdm/tutorials/create-schema-ui.md): 了解如何使用模式编辑器UI创建自定义模式。
* [实时客户用户档案](../../../../../profile/home.md): 基于来自多个来源的聚集数据提供统一、实时的消费者用户档案。

如果您已经拥有有效的Salesforce帐户，您可以跳过此文档的其余部分，继续学习配置 [数据流的教程](../../dataflow/crm.md)。

### 收集所需的凭据

| 凭据 | 描述 |
| ---------- | ----------- |
| `environmentUrl` | Salesforce源实例的URL。 |
| `username` | Salesforce用户帐户的用户名。 |
| `password` | Salesforce用户帐户的口令。 |
| `securityToken` | Salesforce用户帐户的安全令牌。 |

有关快速入门的详细信息，请访 [问此Salesforce文档](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm)。

## 连接您的Salesforce帐户

收集所需凭据后，您可以按照以下步骤创建新的Salesforce帐户以连接到平台。

登录到 [Adobe Experience Platform](https://platform.adobe.com) ，然后从左 **[!UICONTROL 侧导航栏]** 中 *[!UICONTROL 选择“源]* ”以访问“源”工作区。 “目 *[!UICONTROL 录]* ”屏幕显示可为其创建入站帐户的各种源，每个源显示与它们关联的现有帐户和数据集流的数量。

您可以从屏幕左侧的目录中选择适当的类别。 或者，您也可以使用搜索选项找到要使用的特定源。

在“数 *[!UICONTROL 据库]* ”类别 **[!UICONTROL 下]** ，选择Salesforce **单** 击+图标(+)以创建新的Salesforce连接器。

![目录](../../../../images/tutorials/create/salesforce/catalog.png)

此时 *[!UICONTROL 将显示“连接到]* Salesforce”页。 在此页上，您可以使用新凭据或现有凭据。

### 新帐户

如果您使用新凭据，请选择“ **[!UICONTROL 新帐户]**”。 在显示的输入表单上，提供名称、可选说明和您的Salesforce凭据的连接。 完成后，选 **[!UICONTROL 择]** Connect，然后允许一段时间建立新帐户。

![connect](../../../../images/tutorials/create/salesforce/new.png)

### 现有帐户

要连接现有帐户，请选择要连接的Salesforce帐户，然后 **[!UICONTROL 选择]** 右上角的下一步以继续。

![现有](../../../../images/tutorials/create/salesforce/existing.png)

## 后续步骤

通过遵循本教程，您已建立了与Salesforce帐户的连接。 您现在可以继续阅读下一个教程， [并配置数据流以将数据引入平台](../../dataflow/crm.md)。